# Dossier de Conception Technique

<div style="display: flex; align-items: center; gap: 50px; justify-content: center;">
    <img src="../assets/images/logo_taskforce_tp.png" alt="TaskForce Logo" width="200"/>
    <img src="../assets/images/logo_metz_numeric_school.svg" alt="Metz Numeric School Logo" width="230"/>
</div>

## Sommaire
- [1. Architecture Détaillée](#1-architecture-détaillée)
- [2. Modélisation des Données](#2-modélisation-des-données)
- [3. Diagrammes UML](#3-diagrammes-uml)
- [4. Algorithme de Matching](#4-algorithme-de-matching)
- [5. Patterns et Principes](#5-patterns-et-principes)
- [6. Gestion des Fichiers](#6-gestion-des-fichiers)
- [7. Notifications Temps Réel](#7-notifications-temps-réel)

---

## 1. Architecture Détaillée

### 1.1 Architecture Hexagonale (Ports & Adapters)

```
┌─────────────────────────────────────────────────────┐
│                    FRONTEND (Next.js)                │
│  ┌─────────┐  ┌──────────┐  ┌─────────────────┐    │
│  │  Pages  │  │ Components│  │ State Management│    │
│  └─────────┘  └──────────┘  └─────────────────┘    │
└───────────────────┬─────────────────────────────────┘
                    │ HTTP/REST + WebSocket
┌───────────────────┴─────────────────────────────────┐
│               BACKEND (Spring Boot)                  │
│  ┌─────────────────────────────────────────────┐    │
│  │         API Layer (Controllers)             │    │
│  │  /api/auth  /api/tasks  /api/projects       │    │
│  └──────────────────┬──────────────────────────┘    │
│                     │                                │
│  ┌──────────────────┴──────────────────────────┐    │
│  │        Application Layer (Use Cases)        │    │
│  │  - CreateTask  - AssignTask                 │    │
│  │  - SuggestAssignees  - AddComment           │    │
│  └──────────────────┬──────────────────────────┘    │
│                     │                                │
│  ┌──────────────────┴──────────────────────────┐    │
│  │          Domain Layer (Entities)            │    │
│  │  Task, User, Project, Team, Skill           │    │
│  └──────────────────┬──────────────────────────┘    │
│                     │                                │
│  ┌──────────────────┴──────────────────────────┐    │
│  │    Infrastructure Layer (Repositories)      │    │
│  │  JPA, Flyway, File Storage, WebSocket       │    │
│  └──────────────────┬──────────────────────────┘    │
└────────────────────┬────────────────────────────────┘
                     │
┌────────────────────┴────────────────────────────────┐
│              PostgreSQL Database                     │
└──────────────────────────────────────────────────────┘
```

### 1.2 Structure des Packages (Backend)

```
com.taskforce.tfapi
├── api                     # Couche API (Controllers)
│   ├── auth
│   ├── task
│   ├── project
│   ├── user
│   └── notification
├── application             # Use Cases
│   ├── task
│   │   ├── CreateTaskUseCase.java
│   │   ├── AssignTaskUseCase.java
│   │   └── SuggestAssigneesUseCase.java
│   ├── notification
│   └── user
├── domain                  # Entités métier
│   ├── model
│   │   ├── User.java
│   │   ├── Task.java
│   │   ├── Project.java
│   │   ├── Team.java
│   │   └── Skill.java
│   ├── repository          # Interfaces (Ports)
│   │   ├── TaskRepository.java
│   │   └── UserRepository.java
│   └── service             # Services métier
│       └── MatchingService.java
└── infrastructure          # Adapters
    ├── persistence         # JPA Repositories
    │   ├── entity          # JPA Entities
    │   └── impl            # Repository Implementations
    ├── security            # Spring Security Config
    ├── storage             # File Storage (S3/Local)
    └── websocket           # WebSocket Configuration
```

---

## 2. Modélisation des Données

### 2.1 Modèle Conceptuel de Données (MCD)

#### Entités Principales

**USER (Utilisateur)**
- `id` : UUID (PK)
- `email` : VARCHAR(255) UNIQUE NOT NULL
- `password_hash` : VARCHAR(255) NOT NULL
- `first_name` : VARCHAR(100)
- `last_name` : VARCHAR(100)
- `role` : ENUM('ADMIN', 'MANAGER', 'COLLABORATOR') NOT NULL
- `avatar_url` : VARCHAR(500)
- `bio` : TEXT
- `availability_hours_per_week` : INTEGER
- `is_active` : BOOLEAN DEFAULT TRUE
- `created_at` : TIMESTAMP
- `updated_at` : TIMESTAMP

**SKILL (Compétence)**
- `id` : UUID (PK)
- `name` : VARCHAR(100) UNIQUE NOT NULL
- `category` : VARCHAR(50) (ex: "Backend", "Frontend", "Design", "Management")
- `description` : TEXT
- `created_at` : TIMESTAMP

**USER_SKILL (Compétence Utilisateur)**
- `id` : UUID (PK)
- `user_id` : UUID (FK → USER)
- `skill_id` : UUID (FK → SKILL)
- `level` : INTEGER (1-5) NOT NULL
- `years_experience` : DECIMAL(3,1)
- `last_used_date` : DATE
- `created_at` : TIMESTAMP
- `updated_at` : TIMESTAMP

**TEAM (Équipe)**
- `id` : UUID (PK)
- `name` : VARCHAR(100) NOT NULL
- `description` : TEXT
- `manager_id` : UUID (FK → USER)
- `created_at` : TIMESTAMP
- `updated_at` : TIMESTAMP

**TEAM_MEMBER (Membre d'Équipe)**
- `id` : UUID (PK)
- `team_id` : UUID (FK → TEAM)
- `user_id` : UUID (FK → USER)
- `joined_at` : TIMESTAMP

**PROJECT (Projet)**
- `id` : UUID (PK)
- `name` : VARCHAR(200) NOT NULL
- `description` : TEXT
- `team_id` : UUID (FK → TEAM)
- `manager_id` : UUID (FK → USER)
- `start_date` : DATE
- `end_date` : DATE
- `budget` : DECIMAL(12,2)
- `status` : ENUM('DRAFT', 'ACTIVE', 'ON_HOLD', 'COMPLETED', 'ARCHIVED') DEFAULT 'DRAFT'
- `created_at` : TIMESTAMP
- `updated_at` : TIMESTAMP

**TASK (Tâche)**
- `id` : UUID (PK)
- `project_id` : UUID (FK → PROJECT) NOT NULL
- `title` : VARCHAR(200) NOT NULL
- `description` : TEXT
- `status` : ENUM('TODO', 'IN_PROGRESS', 'IN_REVIEW', 'DONE', 'BLOCKED') DEFAULT 'TODO'
- `priority` : ENUM('LOW', 'MEDIUM', 'HIGH', 'CRITICAL') DEFAULT 'MEDIUM'
- `estimated_hours` : DECIMAL(5,2)
- `actual_hours` : DECIMAL(5,2)
- `assigned_user_id` : UUID (FK → USER) NULL
- `created_by_user_id` : UUID (FK → USER) NOT NULL
- `due_date` : TIMESTAMP
- `completed_at` : TIMESTAMP NULL
- `created_at` : TIMESTAMP
- `updated_at` : TIMESTAMP

**TASK_SKILL_REQUIREMENT (Compétence Requise)**
- `id` : UUID (PK)
- `task_id` : UUID (FK → TASK)
- `skill_id` : UUID (FK → SKILL)
- `min_level` : INTEGER (1-5) NOT NULL
- `is_mandatory` : BOOLEAN DEFAULT TRUE

**COMMENT (Commentaire)**
- `id` : UUID (PK)
- `task_id` : UUID (FK → TASK) NOT NULL
- `user_id` : UUID (FK → USER) NOT NULL
- `content` : TEXT NOT NULL
- `created_at` : TIMESTAMP
- `updated_at` : TIMESTAMP

**ATTACHMENT (Fichier Joint)**
- `id` : UUID (PK)
- `task_id` : UUID (FK → TASK) NOT NULL
- `uploaded_by_user_id` : UUID (FK → USER) NOT NULL
- `file_name` : VARCHAR(255) NOT NULL
- `file_path` : VARCHAR(500) NOT NULL
- `file_size` : BIGINT (en bytes)
- `mime_type` : VARCHAR(100)
- `created_at` : TIMESTAMP

**NOTIFICATION (Notification)**
- `id` : UUID (PK)
- `user_id` : UUID (FK → USER) NOT NULL
- `type` : ENUM('TASK_ASSIGNED', 'TASK_UPDATED', 'COMMENT_ADDED', 'DEADLINE_APPROACHING', 'OVERLOAD_ALERT') NOT NULL
- `title` : VARCHAR(200) NOT NULL
- `message` : TEXT
- `related_task_id` : UUID (FK → TASK) NULL
- `related_project_id` : UUID (FK → PROJECT) NULL
- `is_read` : BOOLEAN DEFAULT FALSE
- `created_at` : TIMESTAMP

**ACTIVITY_LOG (Journal d'Activité)**
- `id` : UUID (PK)
- `user_id` : UUID (FK → USER)
- `action` : VARCHAR(100) NOT NULL (ex: "TASK_CREATED", "USER_LOGIN")
- `entity_type` : VARCHAR(50) (ex: "TASK", "PROJECT", "USER")
- `entity_id` : UUID
- `details` : JSONB (données supplémentaires)
- `ip_address` : VARCHAR(45)
- `created_at` : TIMESTAMP

### 2.2 Index et Optimisations

```sql
-- Performance des requêtes fréquentes
CREATE INDEX idx_task_project ON task(project_id);
CREATE INDEX idx_task_assigned_user ON task(assigned_user_id);
CREATE INDEX idx_task_status ON task(status);
CREATE INDEX idx_notification_user_read ON notification(user_id, is_read);
CREATE INDEX idx_comment_task ON comment(task_id);
CREATE INDEX idx_attachment_task ON attachment(task_id);
CREATE INDEX idx_user_skill_user ON user_skill(user_id);
CREATE INDEX idx_team_member_team ON team_member(team_id);
CREATE INDEX idx_team_member_user ON team_member(user_id);

-- Index composites
CREATE INDEX idx_task_project_status ON task(project_id, status);
CREATE INDEX idx_notification_user_created ON notification(user_id, created_at DESC);
```

---

## 3. Diagrammes UML

### 3.1 Diagramme de Classes (Domain)

```java
// Domain Entity - User
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.UUID)
    private UUID id;
    
    @Column(unique = true, nullable = false)
    private String email;
    
    @Column(nullable = false)
    private String passwordHash;
    
    private String firstName;
    private String lastName;
    
    @Enumerated(EnumType.STRING)
    private UserRole role;
    
    private String avatarUrl;
    private String bio;
    private Integer availabilityHoursPerWeek;
    private Boolean isActive = true;
    
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private Set<UserSkill> skills = new HashSet<>();
    
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
    
    // Methods
    public boolean hasSkill(String skillName, int minLevel) {
        return skills.stream()
            .anyMatch(us -> us.getSkill().getName().equals(skillName) 
                         && us.getLevel() >= minLevel);
    }
}

// Domain Entity - Task
@Entity
@Table(name = "tasks")
public class Task {
    @Id
    @GeneratedValue(strategy = GenerationType.UUID)
    private UUID id;
    
    @ManyToOne(optional = false)
    @JoinColumn(name = "project_id")
    private Project project;
    
    @Column(nullable = false)
    private String title;
    
    @Column(columnDefinition = "TEXT")
    private String description;
    
    @Enumerated(EnumType.STRING)
    private TaskStatus status = TaskStatus.TODO;
    
    @Enumerated(EnumType.STRING)
    private TaskPriority priority = TaskPriority.MEDIUM;
    
    private BigDecimal estimatedHours;
    private BigDecimal actualHours;
    
    @ManyToOne
    @JoinColumn(name = "assigned_user_id")
    private User assignedUser;
    
    @ManyToOne(optional = false)
    @JoinColumn(name = "created_by_user_id")
    private User createdBy;
    
    private LocalDateTime dueDate;
    private LocalDateTime completedAt;
    
    @OneToMany(mappedBy = "task", cascade = CascadeType.ALL)
    private Set<TaskSkillRequirement> skillRequirements = new HashSet<>();
    
    @OneToMany(mappedBy = "task", cascade = CascadeType.ALL)
    private Set<Comment> comments = new HashSet<>();
    
    @OneToMany(mappedBy = "task", cascade = CascadeType.ALL)
    private Set<Attachment> attachments = new HashSet<>();
    
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
    
    // Business methods
    public void assignTo(User user) {
        this.assignedUser = user;
        this.updatedAt = LocalDateTime.now();
    }
    
    public void updateStatus(TaskStatus newStatus) {
        this.status = newStatus;
        if (newStatus == TaskStatus.DONE) {
            this.completedAt = LocalDateTime.now();
        }
        this.updatedAt = LocalDateTime.now();
    }
}
```

### 3.2 Diagramme de Séquence - Création de Tâche avec Matching

```
Manager → TaskController : POST /api/tasks
TaskController → CreateTaskUseCase : execute(command)
CreateTaskUseCase → TaskRepository : save(task)
TaskRepository → Database : INSERT task
CreateTaskUseCase → SuggestAssigneesUseCase : execute(taskId)
SuggestAssigneesUseCase → UserSkillRepository : findUsersWithSkills(requiredSkills)
SuggestAssigneesUseCase → MatchingService : calculateMatchScores(users, task)
MatchingService → SuggestAssigneesUseCase : List<UserMatchScore>
SuggestAssigneesUseCase → CreateTaskUseCase : suggestions
CreateTaskUseCase → TaskController : TaskCreatedResponse + suggestions
TaskController → Manager : 201 Created + suggestions JSON
```

### 3.3 Diagramme de Séquence - Assignation avec Notification

```
Manager → TaskController : PUT /api/tasks/{id}/assign
TaskController → AssignTaskUseCase : execute(taskId, userId)
AssignTaskUseCase → TaskRepository : findById(taskId)
AssignTaskUseCase → UserRepository : findById(userId)
AssignTaskUseCase → Task : assignTo(user)
AssignTaskUseCase → TaskRepository : save(task)
AssignTaskUseCase → CreateNotificationUseCase : execute(TASK_ASSIGNED)
CreateNotificationUseCase → NotificationRepository : save(notification)
CreateNotificationUseCase → WebSocketService : sendRealTimeNotification(userId)
AssignTaskUseCase → TaskController : TaskAssigned
TaskController → Manager : 200 OK
```

### 3.4 Diagramme de Séquence - Ajout de Commentaire

```
User → CommentController : POST /api/tasks/{id}/comments
CommentController → AddCommentUseCase : execute(taskId, content, userId)
AddCommentUseCase → CommentRepository : save(comment)
AddCommentUseCase → TaskRepository : findById(taskId)
AddCommentUseCase → NotificationService : notifyTaskParticipants(comment)
NotificationService → NotificationRepository : saveAll(notifications)
NotificationService → WebSocketService : broadcast(taskId, comment)
AddCommentUseCase → CommentController : CommentCreated
CommentController → User : 201 Created
```

---

## 4. Algorithme de Matching

### 4.1 Logique de Matching Simple (MVP)

```java
@Service
public class SimpleSkillMatchingService {
    
    public List<UserMatchScore> findBestMatches(Task task, List<User> availableUsers) {
        Set<TaskSkillRequirement> requiredSkills = task.getSkillRequirements();
        
        return availableUsers.stream()
            .map(user -> calculateMatchScore(user, requiredSkills))
            .filter(score -> score.getScore() >= 50.0) // Seuil minimum 50%
            .sorted(Comparator.comparingDouble(UserMatchScore::getScore).reversed())
            .limit(3) // Top 3 candidats
            .collect(Collectors.toList());
    }
    
    private UserMatchScore calculateMatchScore(User user, Set<TaskSkillRequirement> requirements) {
        if (requirements.isEmpty()) {
            return new UserMatchScore(user, 100.0, "Aucune compétence requise");
        }
        
        double totalScore = 0.0;
        int mandatorySkillsMatched = 0;
        int mandatorySkillsRequired = (int) requirements.stream()
            .filter(TaskSkillRequirement::isMandatory)
            .count();
        
        for (TaskSkillRequirement req : requirements) {
            Optional<UserSkill> userSkillOpt = user.getSkills().stream()
                .filter(us -> us.getSkill().getId().equals(req.getSkill().getId()))
                .findFirst();
            
            if (userSkillOpt.isPresent()) {
                UserSkill userSkill = userSkillOpt.get();
                
                if (userSkill.getLevel() >= req.getMinLevel()) {
                    double skillScore = (userSkill.getLevel() / 5.0) * 100; // Normalisation sur 100
                    totalScore += req.isMandatory() ? skillScore : skillScore * 0.5;
                    
                    if (req.isMandatory()) {
                        mandatorySkillsMatched++;
                    }
                }
            }
        }
        
        // Pénalité si compétences obligatoires manquantes
        if (mandatorySkillsRequired > 0 && mandatorySkillsMatched < mandatorySkillsRequired) {
            totalScore *= 0.3; // -70% si skills obligatoires manquantes
        }
        
        double finalScore = Math.min(totalScore / requirements.size(), 100.0);
        
        return new UserMatchScore(
            user, 
            Math.round(finalScore * 10.0) / 10.0, 
            generateExplanation(user, requirements, mandatorySkillsMatched, mandatorySkillsRequired)
        );
    }
    
    private String generateExplanation(User user, Set<TaskSkillRequirement> requirements, 
                                      int matched, int required) {
        if (required > 0 && matched < required) {
            return String.format("Compétences obligatoires manquantes (%d/%d)", matched, required);
        }
        
        int totalMatched = (int) requirements.stream()
            .filter(req -> user.hasSkill(req.getSkill().getName(), req.getMinLevel()))
            .count();
        
        return String.format("Possède %d/%d compétences requises", totalMatched, requirements.size());
    }
}
```

### 4.2 Évolution v2 (IA Avancée)
- Prise en compte de l'historique de performance sur tâches similaires
- Machine Learning pour prédire le temps d'exécution
- Analyse de la charge actuelle en temps réel
- Détection des préférences (certains users préfèrent certains types de tâches)

---

## 5. Patterns et Principes

### 5.1 Architecture Hexagonale (Clean Architecture)
- **Domain** : Indépendant de toute infrastructure
- **Application** : Orchestration des use cases
- **Infrastructure** : Implémentations techniques (JPA, REST, etc.)

### 5.2 SOLID Principles
- **Single Responsibility** : Chaque classe a une seule raison de changer
- **Open/Closed** : Ouvert à l'extension, fermé à la modification
- **Liskov Substitution** : Les implémentations respectent les contrats
- **Interface Segregation** : Interfaces spécifiques et cohésives
- **Dependency Inversion** : Dépendance vers les abstractions (interfaces)

### 5.3 Design Patterns Utilisés
- **Repository Pattern** : Abstraction de la persistance
- **Factory Pattern** : Création de notifications
- **Strategy Pattern** : Algorithmes de matching interchangeables (v2)
- **Observer Pattern** : WebSocket pour notifications temps réel
- **DTO Pattern** : Séparation entités domain/API

---

## 6. Gestion des Fichiers

### 6.1 Stratégie de Stockage (MVP)

```java
@Service
public class LocalFileStorageService implements FileStorageService {
    
    private final String uploadDir = "./uploads/attachments/";
    
    @Override
    public FileMetadata store(MultipartFile file, UUID taskId, UUID userId) {
        // Validation
        validateFile(file);
        
        // Génération du nom unique
        String originalFilename = file.getOriginalFilename();
        String extension = getExtension(originalFilename);
        String uniqueFilename = UUID.randomUUID().toString() + extension;
        
        // Structure : uploads/attachments/{taskId}/{uniqueFilename}
        Path taskDir = Paths.get(uploadDir, taskId.toString());
        Files.createDirectories(taskDir);
        
        Path filePath = taskDir.resolve(uniqueFilename);
        Files.copy(file.getInputStream(), filePath);
        
        return FileMetadata.builder()
            .fileName(originalFilename)
            .filePath(filePath.toString())
            .fileSize(file.getSize())
            .mimeType(file.getContentType())
            .build();
    }
    
    private void validateFile(MultipartFile file) {
        // Taille max : 10 MB
        if (file.getSize() > 10 * 1024 * 1024) {
            throw new FileSizeException("File exceeds 10 MB limit");
        }
        
        // Types autorisés
        List<String> allowedMimeTypes = Arrays.asList(
            "image/jpeg", "image/png", "image/gif",
            "application/pdf",
            "application/vnd.ms-excel", 
            "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
            "text/plain"
        );
        
        if (!allowedMimeTypes.contains(file.getContentType())) {
            throw new InvalidFileTypeException("File type not allowed");
        }
    }
}
```

### 6.2 Évolution v2
- Migration vers **S3/MinIO** pour scalabilité
- Génération de **thumbnails** pour images
- **Scan antivirus** avant stockage

---

## 7. Notifications Temps Réel

### 7.1 WebSocket Configuration

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {
    
    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.enableSimpleBroker("/topic", "/queue");
        registry.setApplicationDestinationPrefixes("/app");
    }
    
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/ws")
            .setAllowedOriginPatterns("*")
            .withSockJS();
    }
}

@Service
public class WebSocketNotificationService {
    
    @Autowired
    private SimpMessagingTemplate messagingTemplate;
    
    public void sendNotificationToUser(UUID userId, NotificationDTO notification) {
        messagingTemplate.convertAndSendToUser(
            userId.toString(),
            "/queue/notifications",
            notification
        );
    }
    
    public void broadcastToTask(UUID taskId, CommentDTO comment) {
        messagingTemplate.convertAndSend(
            "/topic/tasks/" + taskId + "/comments",
            comment
        );
    }
}
```

### 7.2 Client (Frontend)

```typescript
// hooks/useWebSocket.ts
import { Client } from '@stomp/stompjs';
import SockJS from 'sockjs-client';

export const useNotifications = (userId: string) => {
  const [notifications, setNotifications] = useState<Notification[]>([]);
  
  useEffect(() => {
    const socket = new SockJS('http://localhost:8080/ws');
    const stompClient = new Client({
      webSocketFactory: () => socket,
      onConnect: () => {
        stompClient.subscribe(`/user/${userId}/queue/notifications`, (message) => {
          const notification = JSON.parse(message.body);
          setNotifications(prev => [notification, ...prev]);
        });
      }
    });
    
    stompClient.activate();
    
    return () => stompClient.deactivate();
  }, [userId]);
  
  return notifications;
};
```

---

## 8. Contraintes et Règles Métier

### 8.1 Règles de Validation
1. **User** : Email unique, mot de passe min 8 caractères
2. **Task** : Titre obligatoire, doit appartenir à un projet
3. **UserSkill** : Level entre 1 et 5
4. **Assignment** : Un utilisateur ne peut être assigné que s'il est membre de l'équipe du projet
5. **Notification** : Suppression automatique après 30 jours si lue
6. **Attachment** : Taille max 10 MB par fichier

### 8.2 Cascade et Suppressions
- **Suppression User** : Soft delete (is_active = FALSE)
- **Suppression Project** : Archivage, pas de suppression physique
- **Suppression Task** : Suppression cascade comments/attachments/notifications
- **Suppression Team** : Impossible si projets actifs

---

**Dernière mise à jour** : Décembre 2025  
**Architecte** : Pierre MICHEL
