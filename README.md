Ce projet contient deux parties principales :

- **Backend (Laravel + Docker)**
- **Frontend (Docker / React ou autre framework)**

L’application utilise **Docker Compose** pour lancer l’environnement complet facilement.

---

## 🚀 Lancement du projet

### 1. Cloner le projet
\`\`\`
git clone https://github.com/TNdria/el_pirata.git
cd el_pirata
\`\`\`

### 2. Lancer les containers Docker
\`\`\`
docker-compose up -d
\`\`\`

### 3. Vérifier que le backend fonctionne
\`\`\`
docker logs backend
\`\`\`

Tu dois voir :
\`\`\`
INFO  Server running on http://0.0.0.0:8000
\`\`\`

---

## 🔧 Configuration Backend (Laravel)

### Installer les dépendances (si hors docker)
\`\`\`
composer install
\`\`\`

### Copier l’environnement
\`\`\`
cp .env.example .env
\`\`\`

### Générer la clé d’application
\`\`\`
php artisan key:generate
\`\`\`

### Lancer les migrations
\`\`\`
php artisan migrate --seed
\`\`\`

---

## 🐳 Docker – Commandes utiles

### Arrêter tous les containers
\`\`\`
docker-compose down
\`\`\`

### Redémarrer le projet
\`\`\`
docker-compose restart
\`\`\`

### Voir les logs
\`\`\`
docker logs backend
docker logs frontend
\`\`\`

---

## 🔑 Sécurité – Suppression des secrets

Les clés API ont été supprimées du dépôt grâce à :

\`\`\`
git filter-repo --force --invert-paths --path frontend/docker-compose.yml
\`\`\`

---

## 📁 Structure du projet

\`\`\`
el_pirata/
│── backend/        # Code Frontend
│── el_pirata_api/       # Code Laravel
│── docker-compose.yml
└── README.md
\`\`\`

---

## 