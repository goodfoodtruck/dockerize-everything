# Créer un Dockerfile pour cette application en mode production

FROM node:18-alpine as builder

WORKDIR /client-tv

COPY . .

RUN npm install

ARG API_BASE_URL
ARG CLIENT_PORT
ARG SERVER_PORT

ENV API_BASE_URL=http://tv-shows-catalog-server-1:$SERVER_PORT

RUN npm run build

# build

FROM node:18-alpine

COPY --from=builder /client-tv/package*.json .

COPY --from=builder /client-tv/node_modules ./node_modules

COPY --from=builder /client-tv/build ./build

EXPOSE $CLIENT_PORT

CMD ["node", "build/index.js"]