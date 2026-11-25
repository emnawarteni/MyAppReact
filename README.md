# MyAppReact – Docker, Docker Compose et Jenkins

## 1. Présentation du projet

Fi hedha projet, 5demna 3la application web basée 3la architecture MERN:

- **Client:** application React.
- **Server:** backend Node.js.
- **Database:** MongoDB.

L'objectif mta3na houwa containeriser les différentes parties du projet avec Docker, utiliser Docker Compose bech nlaunchiw les services, w automatiser la construction des images Docker avec Jenkins.

## 2. Structure du projet

```text
MyAppReact/
│
├── Client/
│   └── Dockerfile
│
├── Server/
│   └── Dockerfile
│
├── screenshots/
│   ├── docker-containers.png
│   ├── dockerhub-repository.png
│   ├── github.png
│   └── jenkins-console.png
│
├── docker-compose.yml
├── Jenkinsfile
├── .gitignore
└── README.md
```

## 3. Docker

### 3.1 Dockerfile du Server

Fi dossier `Server`, 3malna Dockerfile bech nbniw image Docker mta3 backend.

Les instructions utilisées:

- `FROM node:lts-alpine`: nesta3mlou image Node.js basée 3la Alpine Linux.
- `WORKDIR /app`: n7addou dossier de travail.
- `COPY package*.json ./`: ncopiw fichiers package.
- `RUN npm install`: ninstalliw les dépendances.
- `COPY . .`: ncopiw code source.
- `EXPOSE 9000`: n7addou port du serveur.
- `CMD ["npm", "start"]`: nlaunchiw serveur automatiquement.

### 3.2 Dockerfile du Client

Fi dossier `Client`, 3malna Dockerfile bech nbniw image Docker mta3 application React.

Les principales instructions:

- Copier les fichiers `package.json`.
- Installer les dépendances avec `npm install`.
- Copier le code source.
- Construire l'application avec `npm run build`.
- Installer `serve`.
- Lancer l'application sur le port 3000.

## 4. Docker Compose

Sta3melna fichier `docker-compose.yml` bech nconfiguriw les trois services:

- **MongoDB:** container mta3 base de données.
- **Server:** backend Node.js, disponible sur le port 9000.
- **Client:** frontend React, disponible sur le port 3000.

Zedna réseau `mern-network` de type `bridge` bech les containers ynajmou yet3arfou binethom.

### Commandes utilisées

Lancer les services:

```bash
docker compose up -d --build
```

Afficher les containers:

```bash
docker compose ps -a
```

Afficher les images:

```bash
docker images
```

Arrêter les services du projet:

```bash
docker compose down
```

### Résultat Docker Compose

Cette capture montre les containers du projet après leur lancement.

![Docker Containers](Capture%20d%27%C3%A9cran/docker-containers.png)

**Remarque:** MongoDB container est lancé, ama backend actuel mazal ma fihch connexion effective m3a MongoDB. Donc ma najjmouch n9oulou elli l'application connectée à la base de données.

## 5. Jenkins et Jenkinsfile

### 5.1 Pourquoi avons-nous utilisé Jenkins?

Sta3melna Jenkins bech nautomatisiw les étapes de construction des images Docker.

Jenkins permet d'exécuter automatiquement les commandes définies dans un Pipeline.

### 5.2 Jenkinsfile

Zedna fichier `Jenkinsfile` fi root mta3 projet bech n7afthou 3la configuration du Pipeline directement dans GitHub.

Le fichier contient les étapes suivantes:

1. **Checkout GitHub:** récupérer le code source du projet depuis GitHub.
2. **Build Server Image:** construire l'image Docker du serveur à partir du Dockerfile du dossier `Server`.
3. **Build Client Image:** construire l'image Docker du client à partir du Dockerfile du dossier `Client`.

### 5.3 Configuration de Jenkins

Fi Jenkins, 5tarna:

- Definition: `Pipeline script from SCM`.
- SCM: `Git`.
- Repository URL: `https://github.com/emnawarteni/MyAppReact.git`.
- Branch: `*/main`.
- Script Path: `Jenkinsfile`.

Hakka Jenkins ya9ra `Jenkinsfile` directement men GitHub.

### 5.4 Résultat du Pipeline

Ba3d ma configurina Jenkins, 3malna build numéro 4.

Jenkins récupéra le Jenkinsfile depuis GitHub, puis exécuta les étapes du Pipeline:

- Checkout GitHub.
- Build Server Image.
- Build Client Image.

Le résultat final était:

```text
Finished: SUCCESS
```

Les trois étapes ont été exécutées avec succès.

### Capture Console Output

![Jenkins Console](Capture%20d%27%C3%A9cran/jenkins-console.png)

## 6. Docker Hub

Ba3d ma bnin les images Docker localement, 3malna tags w push lel Docker Hub bech nwaliw najjmou naccédiw lel images publiées.

### Commandes utilisées

```bash
docker tag mern-server:latest emna120/mern-server:latest
docker tag mern-client:latest emna120/mern-client:latest

docker push emna120/mern-server:latest
docker push emna120/mern-client:latest
```

Les deux images ont été envoyées avec succès vers Docker Hub.

### Liens des images

- **Server:** https://hub.docker.com/r/emna120/mern-server
- **Client:** https://hub.docker.com/r/emna120/mern-client

### Capture Docker Hub

![Docker Hub](Capture%20d%27%C3%A9cran/dockerhub-server.png)

**Remarque:** push lel Docker Hub 3malneh manuellement avec PowerShell. Pipeline Jenkins actuel ya3mel checkout w build, ama mazal ma fihch étape automatique lel push.

## 7. Git, GitHub et .gitignore

### 7.1 Git et GitHub

Sta3melna Git bech nversioniw projet, w GitHub bech n7afthou 3la code source w les fichiers de configuration.

Lien du repository:

https://github.com/emnawarteni/MyAppReact

### 7.2 Pourquoi avons-nous utilisé .gitignore?

Créina fichier `.gitignore` bech Git yetjannab certains fichiers eli ma يلزمouch yetpushaw lel GitHub.

Les fichiers ignorés dans notre configuration:

- `node_modules/`: dépendances Node.js, ynajmou ykounou volumineux w najjmou n3awdou ninstalliw-hom.
- `.env` et `.env.*`: fichiers contenant des informations confidentielles comme passwords et clés API.
- `dist/` et `build/`: fichiers générés automatiquement pendant le build.
- `*.log`: fichiers logs.
- `.vscode/` et `.idea/`: fichiers de configuration des éditeurs.
- `Thumbs.db` et `.DS_Store`: fichiers système.

**Important:** ma 7attinech `Jenkinsfile` fi `.gitignore`, khater n7ebbouh yetpush lel GitHub bech Jenkins ya9ra configuration mta3 Pipeline menou.

### Commandes utilisées

```bash
git add .gitignore
git commit -m "Add gitignore file"
git push
```

Ba3d push, `git status` 3tana:

```text
nothing to commit, working tree clean
```

### Capture du repository GitHub

![GitHub Repository](Capture%20d%27%C3%A9cran/github.png)

## 8. Les problèmes rencontrés et leurs solutions

### Problème 1: Mauvaise adresse du repository GitHub

Au début, l'adresse remote Git kenet pointée vers un ancien repository.

**Solution:** badalna URL mta3 remote avec:

```bash
git remote set-url origin https://github.com/emnawarteni/MyAppReact.git
```

### Problème 2: Problème du compte de service Jenkins

Jenkins ma najjemch ykhdem correctement avec le compte Windows initial à cause d'un problème d'authentification.

**Solution:** badalna le compte du service Jenkins vers `Local System`.

### Problème 3: Jenkins ne trouvait pas Docker

Jenkins ma kench yal9a Docker automatiquement dans son environnement Windows.

**Solution:** sta3melna chemin complet du fichier `docker.exe` dans le Jenkinsfile:

```text
C:\Users\LENOVO\AppData\Local\Programs\DockerDesktop\resources\bin\docker.exe
```

### Problème 4: Git installation non configurée dans Jenkins

Jenkins affichait le message:

```text
Selected Git installation does not exist. Using Default
```

**Solution:** Jenkins sta3mel Git installé par défaut w kammel l'exécution sans problème.

### Problème 5: Warning Docker Legacy Builder

Pendant la construction des images, Docker affichait un avertissement indiquant que Legacy Builder est déprécié.

**Solution:** malgré cet avertissement, les deux images ont été construites correctement. BuildKit est une alternative pour les futures constructions.

### Problème 6: Fichier .gitignore non suivi par Git

Ba3d création du fichier `.gitignore`, `git status` affichait:

```text
Untracked files:
    .gitignore
```

**Solution:** zedneh lel suivi Git avec:

```bash
git add .gitignore
git commit -m "Add gitignore file"
git push
```

Ba3d, Git a affiché:

```text
nothing to commit, working tree clean
```

## 9. Conclusion

Fi hedha projet, ta3allamna kifach ncontainerisiw application avec Docker, nlaunchiw plusieurs services avec Docker Compose, nbniw les images Docker, w npushiwhom vers Docker Hub.

Zeda 5demna avec Jenkins bech nautomatisiw construction des images, w sta3melna Git et GitHub pour gérer le code source.

Enfin, 5demna avec `Jenkinsfile` pour conserver la configuration du Pipeline et `.gitignore` pour éviter l'envoi des fichiers inutiles ou confidentiels.
