# 41-Eridani offline backend

Express backend for 40-Eridani, upgraded with the existing API preserved.

## Local setup

Use Node 26.10.0 (`.nvmrc`) and MongoDB Community 9.0.2. Run `npm ci` and `npm run setup:local`; the setup creates an ignored private `.env.local` with a random JWT key and preserves an existing file.

In a foreground terminal:

```sh
mkdir -p .local/mongodb
mongod --dbpath .local/mongodb --bind_ip 127.0.0.1 --port 27018 --replSet offline-rs
```

In a second terminal run `npm run db:init` and `npm start`. Skip the MongoDB launch if the matching local `offline-rs` already runs on 27018. The initializer creates no application records. Stop foreground processes with Ctrl+C. No Atlas account or network is required after installation. Uploaded files remain local in `images/`.

The API remains `/user/signup`, `/user/login`, and `/posts` (GET/POST/PUT/DELETE), including authenticated image uploads and pagination. Uploaded files remain local in `images/`.

## Validation

`npm test` exercises a real offline MongoDB database and an ephemeral HTTP server: signup, valid and missing-user login, image upload, pagination, edit, unauthorized deletion, authorized deletion, and 404 after deletion. It deletes only its isolated process-specific test database. Current dependency versions are pinned in package.json and package-lock.json.

Official package metadata: https://registry.npmjs.org/express/latest, https://registry.npmjs.org/mongoose/latest, https://registry.npmjs.org/mongoose-unique-validator/latest. MongoDB release: https://www.mongodb.com/docs/manual/release-notes/9.0/. Node release manifest: https://nodejs.org/dist/index.json.
