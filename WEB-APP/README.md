# WEB-APP

Ce dossier contient l’application web Node.js (API REST, WebSocket et bridge MQTT) ainsi que le front-end statique.

## Contenu

- `server.js` : serveur Express + Socket.IO + MQTT + accès PostgreSQL/InfluxDB
- `package.json` : scripts et dépendances Node.js
- `Dockerfile` : image de production (Node 18, utilisateur non-root)
- `public/` : interface web (`index.html`, `style.css`, `app.js`, PWA)

## Prérequis

- Node.js `>= 18`
- npm `>= 9`

## Variables d’environnement

Principales variables consommées par `server.js` :

- `PORT` (défaut: `3000`)
- `MQTT_BROKER`
- `JWT_SECRET`
- `ADMIN_SECRET_TOKEN`
- `POSTGRES_HOST`
- `POSTGRES_PORT`
- `POSTGRES_DATABASE`
- `POSTGRES_USER`
- `POSTGRES_PASSWORD`
- `INFLUX_URL`
- `INFLUX_TOKEN`
- `INFLUX_ORG`
- `INFLUX_BUCKET`
- `SETTINGS_FILE` (optionnel, défaut `./settings.json`)

## Démarrage local (hors Docker)

Depuis ce dossier :

```bash
npm install
npm run dev
```

Ou en mode normal :

```bash
npm start
```

## Démarrage via Docker Compose (recommandé)

Depuis la racine du projet :

```bash
docker compose up -d --build web
```

L’application écoute sur `http://localhost:3000`.

## Endpoints utiles

- `GET /health` : état du serveur
- `GET /api/history?limit=100` : historique des mesures
- `GET /api/stats` : stats agrégées
- `GET/POST /api/settings` : configuration des seuils (JWT requis)
- `GET /api/users` : liste des utilisateurs
- `GET/POST/DELETE /api/admin/users` : gestion admin (header `x-admin-token`)

## Notes

- Le front est servi depuis `public/` par Express.
- L’authentification utilisateur est basée sur JWT.
- Les données capteurs temps réel passent par MQTT puis sont relayées en WebSocket.
