# 41-Eridani — posts API

The Express/MongoDB backend for [40-Eridani](https://github.com/TheArchitect71/40-Eridani), an image-post publishing app. It stores user accounts and posts, authenticates requests with JWTs, and saves uploaded images locally. This repository is API-only; use 40-Eridani for the frontend.

## API

- `POST /user/signup` and `POST /user/login`: registration and authentication.
- `GET /posts`: paginated posts.
- `POST /posts`, `PUT /posts/:id`, and `DELETE /posts/:id`: authenticated post management with image uploads.

## Run locally

Prerequisites: the Node version in `.nvmrc` (currently 26.10.0), npm, and MongoDB Community 9.0.2. From the repository root:

```sh
npm ci
npm run setup:local
```

Start MongoDB in a foreground terminal:

```sh
mkdir -p .local/mongodb
mongod --dbpath .local/mongodb --bind_ip 127.0.0.1 --port 27018 --replSet offline-rs
```

If that local replica set already runs on port 27018, reuse it rather than starting a second instance. In another terminal at the repository root:

```sh
npm run db:init
npm start
```

Open [http://127.0.0.1:3000](http://127.0.0.1:3000). Keep both processes in the foreground and stop them with **Ctrl+C**. Setup creates a private, ignored `.env.local` without overwriting an existing file. Database initialization creates no application records. These defaults use local MongoDB; no Atlas account is required.

Uploaded files are stored in `images/`. A fresh database starts empty; create an account and posts through the frontend.

## Development

`npm run dev` starts watch mode. `npm test` runs integration tests against a separate local database and removes that test database afterwards. MongoDB must be running.
