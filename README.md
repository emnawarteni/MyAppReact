# MyAppReact - Déploiement avec Docker et Docker Compose

## 1. Présentation du projet

Ce projet consiste à conteneuriser une application web composée de trois services :

- **Client :** application Frontend développée avec React.
- **Server :** API Backend développée avec Node.js et Express.
- **MongoDB :** base de données NoSQL.

## 2. Technologies utilisées

- Docker
- Docker Compose
- Node.js
- React
- Express.js
- MongoDB

## 3. Structure du projet

```text
MyAppReact/
├── Client/
│   └── Dockerfile
├── Server/
│   └── Dockerfile
├── docker-compose.yml
└── README.md
```

## 4. Construction et lancement

Pour construire les images et démarrer les services :

```bash
docker compose up --build
```

## 5. Accès à l'application

- Frontend : http://localhost:3000
- Backend API : http://localhost:9000/api/health

## 6. Vérification des conteneurs

Pour afficher les conteneurs en cours d'exécution :

```bash
docker ps
```

Pour arrêter et supprimer les conteneurs du projet :

```bash
docker compose down
```

## 7. Résultat

Les trois services Client, Server et MongoDB sont exécutés dans des conteneurs Docker et orchestrés avec Docker Compose.
