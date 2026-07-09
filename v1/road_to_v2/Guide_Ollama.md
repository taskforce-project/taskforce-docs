---
id: guide-ollama
title: Guide setup — Ollama (LLM local gratuit)
doc_type: runbook
statut: active
version: 1.0
date: "07/07/2026"
auteur: Pierre MICHEL
tags: [ollama, llm, local, setup, ia, road-to-v2]
related:
  - "README.md"
  - "Benchmark_Modeles_IA.md"
  - "Contrat_API_et_Donnees.md"
---

# 📘 Guide setup — Ollama (LLM local, gratuit)

> **But** : faire tourner le cerveau IA **en local sur la RTX 5070**, gratuit, privé — via Ollama (API OpenAI-compat) appelé par l'AI Gateway ([[Contrat_API_et_Donnees]]).
> ⚠️ **À faire sur un réseau propre** (wifi maison / partage de connexion) : le réseau du poste corrompt les gros téléchargements (même cause que le « 403 Groq »). Après le setup, **tout tourne offline**.
> Matériel cible : RTX 5070 Laptop **8 Go VRAM** + **32 Go RAM** → un modèle **14B** passe (voir [[Benchmark_Modeles_IA]] §4bis).

---

## 1. Installer Ollama
- https://ollama.com/download → **Download for Windows** → lancer `OllamaSetup.exe`.
- S'installe comme **service auto-démarré** (icône barre des tâches) et **détecte la RTX 5070**.
- Vérifier : `ollama --version`.

## 2. Rendre Ollama joignable par le backend Docker ⚠️
Le backend (conteneur) appelle Ollama sur l'hôte via `host.docker.internal`. Par défaut Ollama n'écoute que sur `localhost` → il faut écouter sur toutes les interfaces :
- **Windows → Variables d'environnement système** → ajouter `OLLAMA_HOST = 0.0.0.0:11434`
- **Quitter** Ollama (clic droit icône → Quit) puis **relancer**.

## 3. Télécharger les modèles (réseau propre)
```bash
ollama pull qwen2.5:14b-instruct    # cerveau principal (~9 Go) — FR + JSON structuré
ollama pull qwen2.5:7b-instruct     # fallback rapide (~4.7 Go) si le 14B est trop lent
ollama pull bge-m3                  # embeddings 1024d (recherche sémantique)
```

## 4. Vérifier + confirmer l'usage GPU
```bash
ollama run qwen2.5:14b-instruct "Réponds en une phrase : c'est quoi une bonne user story ?"
```
- Réponse en quelques secondes.
- Dans un autre terminal : `nvidia-smi` → un process `ollama` doit apparaître sur le GPU (VRAM utilisée) = ✅ accéléré.

## 5. Vérifier l'API OpenAI-compat (ce que le Gateway appelle)
```bash
curl http://localhost:11434/v1/chat/completions -H "Content-Type: application/json" ^
  -d "{\"model\":\"qwen2.5:14b-instruct\",\"messages\":[{\"role\":\"user\",\"content\":\"ping\"}]}"
```
→ JSON avec `choices[0].message.content`. **Le moteur est prêt.**

---

## 6. Ensuite (côté TaskForce)
Quand c'est bon → dire **« ollama ok »**. Le backend est alors activé :
1. `AI_OLLAMA_ENABLED=true` + `AI_PROVIDER=ollama` dans `.env.dev`,
2. Gateway `/v1/chat` (déjà codé) route vers Ollama ; `AiGatewayClient` Java branché dans `AgentService`,
3. rebuild backend → test **« Ask AI »** : réponse + sources (RAG) + write-back node dans le graphe, **sur GPU, 0 €**.

## Dépannage
- **Le backend ne joint pas Ollama** → vérifier `OLLAMA_HOST=0.0.0.0` (étape 2) + qu'Ollama tourne (`curl localhost:11434`).
- **Lent** → basculer `AI_OLLAMA_MODEL=qwen2.5:7b-instruct` (fallback).
- **Download corrompu** → recommencer le `pull` sur un réseau propre (le proxy du poste corrompt les gros fichiers).
