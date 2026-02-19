# Render hosting setup

Use these settings in the Render dashboard so the app builds and runs correctly.

## Root directory

- **Root Directory:** Leave **empty** (use repo root), or set to the folder that contains both `Backend` and `Frontend` (e.g. if your repo root is `uvc`, use empty so paths like `../Frontend` work from Backend).

If your Render service is created from the **Backend** folder only (no Frontend in the same repo), set:
- **Root Directory:** `Backend`

Then change the build command to build the frontend from wherever it lives (e.g. a separate repo or subpath).

## Build & start (repo with Backend + Frontend)

- **Build Command:** `cd Backend && npm install && npm run build`
- **Start Command:** `cd Backend && npm start`

If **Root Directory** is set to `Backend`:
- **Build Command:** `npm install && npm run build`
- **Start Command:** `npm start`

## Environment variables

In Render: **Environment** tab → add:

| Key        | Value                    | Notes                          |
|-----------|---------------------------|--------------------------------|
| `MONGO_URI` | your MongoDB connection string | **Required** for DB connection |
| `PORT`      | (optional)                | Render sets this automatically |

Copy from `.env.example` and set real values in the Render dashboard (do not commit `.env`).

## Summary

- **Entry file:** `server.js` (see `main` in `package.json`).
- **Build:** Installs Frontend deps, builds Frontend, copies `Frontend/dist` → `Backend/public/dist`.
- **Start:** `node server.js` (uses `process.env.PORT` on Render).
