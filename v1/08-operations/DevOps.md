# DevOps & Exploitation — TaskForce (prod 2 VM)

> Runbooks d'exploitation de la prod (2 VM école, pilotées en SSH via **Tailscale**). Complète
> [[Plan_Deploiement_2VM]] (déploiement) et [[Pipeline_CICD]] (CI). Tout ce qui suit est **live et
> vérifié**, mais **hors du flux PR** : changements appliqués directement (kcadm / SSH), stockés dans
> l'état des conteneurs (base `keycloak_prod`, disques VM) — à **rejouer via script** si les VM ou le
> realm sont recréés.

- **VM1** (backend) — Tailscale `100.122.50.25` : postgres, keycloak, backend, ai-service, minio, redis, cloudflared.
- **VM2** (frontend) — Tailscale `100.120.222.10` : frontend, cloudflared.
- Public via **Cloudflare Tunnel** : `app.` / `api.` / `auth.` / `www.` `taskforce-project.fr`.

## 1. Supervision (Prometheus + Grafana) — sur VM2  [statut:: done]

Placée sur la **VM2** (RAM libre) car la **VM1 est saturée** (~175 Mio libres).

- **Grafana** : `http://100.120.222.10:3001` (Tailscale uniquement — rien de public). Menu de dashboards :
  *TaskForce — Overview* (maison : CPU/RAM/disque par VM, top conteneurs, débit HTTP + heap JVM du backend),
  *Node Exporter Full*, *cAdvisor*.
- **Prometheus** (VM2) gratte, via Tailscale, les exporters des DEUX VM : node-exporter (hôte), cAdvisor
  (conteneurs), + le backend `/actuator/prometheus` (Micrometer) relayé par un `socat` sur VM1 (le backend
  ne publie pas 8080 sur l'hôte). **6 cibles UP**.
- **Fichiers** (repo) : `monitoring/vm2/` (compose + prometheus + grafana provisioning) et
  `monitoring/vm1/docker-compose.exporters.yml`. Déployés **hors arbre git** dans `~/monitoring/` sur chaque
  VM (pour ne pas gêner l'auto-deploy). [ref:: monitoring/README.md]

## 2. Sauvegardes Postgres (cluster complet) — sur VM1  [statut:: done]

Filet pour **reseed / expérimenter sur la prod sans risque**.

- **`pg_dumpall`** (cluster COMPLET) : bases `taskforce` (app) + **`keycloak_prod`** (auth : users + IdP +
  secrets + flows) + `umami` + rôles. ⚠️ Keycloak = base **séparée** → un dump mono-base serait un faux filet.
- **Automatique** : systemd `tf-backup.timer` (quotidien 03:00, `Persistent`), rotation `KEEP=14`, sortie
  `~/backups/taskforce-cluster-*.sql.gz` (~90 Kio gz).
- **Manuel** : `~/ops/backup/pg_backup.sh` (avant un reseed). **Restaurer** : `~/ops/backup/pg_restore.sh
  <fichier>` (arrête backend+keycloak+ai-service, importe, redémarre).
- **Fichiers** : `ops/backup/` (repo). [ref:: ops/backup/README.md]

## 3. Connexion sociale Keycloak (GitHub + Google)  [statut:: done]

Backend + front **déjà implémentés** ([[Backend]] `BE-SEC-OAUTH`) ; il ne manquait que la **config Keycloak**,
appliquée live et **rejouable** par **`ops/kc-setup.sh`** (idempotent, secrets par variable d'env).

- **IdPs** `github` + `google` (realm `taskforce-prod`), `trustEmail=true`, liés au flow custom
  **`first broker login autolink`**.
- **Flow seamless** : on NE PEUT PAS éditer le flow **built-in** `first broker login` → on le **copie** et on y
  désactive *Review Profile* / *Confirm link existing account* / *Account verification options*, puis on ajoute
  l'authenticator **`idp-auto-link`** (« Automatically set existing user ») en `REQUIRED`. Résultat : **aucune
  page Keycloak** (nouvel email → compte créé ; email existant → auto-lié, sûr car emails vérifiés fournisseur).
- **Callbacks** (à déclarer chez le fournisseur) :
  `https://auth.taskforce-project.fr/realms/taskforce-prod/broker/{github|google}/endpoint`
- **Front** : boutons actifs via build-arg `NEXT_PUBLIC_AUTH_SOCIAL_READY=github,google` (VM2 `.env` + rebuild).
- ⚠️ **Google** : écran de consentement en mode **Test** → seuls les *test users* déclarés peuvent se connecter
  (sinon `access_denied`), ou publier l'app.
- **Rejeu complet** (si realm recréé) : exporter `GITHUB_IDP_CLIENT_ID/SECRET` + `GOOGLE_IDP_CLIENT_ID/SECRET`,
  puis `bash ops/kc-setup.sh`. [ref:: ops/kc-setup.sh]

## Pièges connus (kcadm / Keycloak prod)
- Mettre à jour une **exécution de flow** = `-b '{"id":…,"requirement":…}'` (le `-s id=… -s requirement=…`
  échoue : le GET renvoie un array). Un flow **built-in** n'est pas éditable → **copier** d'abord.
- Dans une **copie de flow**, les **sous-flows** sont préfixés par le nom du flow ; pas les feuilles.
- Console admin Keycloak **non routée publiquement** (404 sur `/admin/`) — config via kcadm sur la VM.
- Login ROPC refusé (`resolve_required_actions`) si une action requise (`VERIFY_EMAIL`) traîne malgré
  `emailVerified=true` → `kcadm ... -s 'requiredActions=[]'`.

## Déploiement continu (rappel)
Push sur `main` → `tf-autodeploy.timer` (poll 3 min) sur chaque VM : `git pull --ff-only` + rebuild du service
concerné (frontend / backend). Détail : [[Plan_Deploiement_2VM]].
