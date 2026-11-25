
# 1. Image de base
FROM node:lts-alpine

# 2. Répertoire de travail
WORKDIR /app

# 3. Copier les fichiers package
COPY package*.json ./

# 4. Installer les dépendances
RUN npm install

# 5. Copier le reste du projet
COPY . .

# 6. Construire l'application React
RUN npm run build

# 7. Installer le serveur HTTP
RUN npm install -g serve

# 8. Exposer le port
EXPOSE 3000

# 9. Démarrer le serveur HTTP
CMD ["serve", "-s", "dist", "-l", "3000"]
