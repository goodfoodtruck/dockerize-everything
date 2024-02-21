# Créer un Dockerfile pour cette application en mode production

FROM node:18

WORKDIR usr/src/client-tv

COPY . .

COPY .env.example .env

RUN npm install