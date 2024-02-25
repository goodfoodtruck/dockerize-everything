# Créer un Dockerfile pour cette application en mode production

# Créer un Dockerfile pour cette application en mode production

FROM node:18-alpine as builder

WORKDIR /usr/src/server-tv

COPY package*.json .

RUN npm install

ARG SERVER_PORT

COPY . .

RUN npm run build

FROM node:lts

COPY --from=builder /usr/src/server-tv/package*.json .

COPY --from=builder /usr/src/server-tv/node_modules ./node_modules

COPY --from=builder /usr/src/server-tv/dist ./dist

EXPOSE $SERVER_PORT

CMD ["npm", "run", "start:prod"]