
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

# 6. Exposer le port
EXPOSE 9000

# 7. Démarrer le serveur
CMD ["npm", "start"]
