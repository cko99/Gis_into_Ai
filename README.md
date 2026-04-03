# GIS into AI — Geospatial Intelligence Dashboard

Production-ready Geospatial Intelligence Dashboard for Malaysia. Collects, manages, and visualises engineering, drone, and geospatial company data using React, Express, PostgreSQL, and AI integration for decision-making.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, Vite 7, Tailwind CSS v4, shadcn/ui |
| Backend | Express 5, Node.js 20 |
| Database | PostgreSQL 16, Drizzle ORM |
| Maps | React-Leaflet, Leaflet |
| Charts | Recharts |
| Auth | Passport.js (local), express-session |
| Language | TypeScript |

---

## Prerequisites

Before running locally, make sure you have these installed:

- **Node.js 20+** — [https://nodejs.org](https://nodejs.org)
- **PostgreSQL 16** — [https://www.postgresql.org/download](https://www.postgresql.org/download)
- **npm** (comes with Node.js)

Verify your versions:

```bash
node -v     # should be v20.x.x or higher
psql --version
npm -v
```

---

## Local Setup

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd <project-folder>
```

### 2. Install dependencies

```bash
npm install
```

### 3. Create a PostgreSQL database

Open your PostgreSQL shell and run:

```sql
CREATE DATABASE gis_dashboard;
```

If you have a custom PostgreSQL user/password, note them down — you'll need them in the next step.

### 4. Configure environment variables

Create a `.env` file in the project root:

```bash
touch .env
```

Add the following inside `.env`:

```env
DATABASE_URL=postgresql://<username>:<password>@localhost:5432/gis_dashboard
SESSION_SECRET=your_random_secret_string_here
PORT=5000
NODE_ENV=development
```

Replace `<username>` and `<password>` with your PostgreSQL credentials.

**Example for default PostgreSQL setup:**

```env
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/gis_dashboard
SESSION_SECRET=super_secret_dev_key_change_this
PORT=5000
NODE_ENV=development
```

### 5. Push the database schema

This creates all the tables defined in `shared/schema.ts`:

```bash
npm run db:push
```

### 6. Run the development server

```bash
npm run dev
```

The app will be available at: **[http://localhost:5000](http://localhost:5000)**

> The Express backend and Vite dev server both run on port 5000. The backend serves the frontend in development.

---

## Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start full-stack dev server (backend + frontend) |
| `npm run dev:client` | Start Vite frontend only (port 5000) |
| `npm run build` | Build for production (output: `dist/public`) |
| `npm start` | Run production build |
| `npm run db:push` | Push schema changes to PostgreSQL |
| `npm run check` | TypeScript type check |

---

## Project Structure

```
├── client/              # React frontend (Vite)
│   └── src/
│       ├── components/  # UI components (shadcn/ui)
│       ├── hooks/       # Custom React hooks
│       └── lib/         # Utilities
├── server/              # Express backend
│   └── index.ts         # Server entry point
├── shared/              # Shared types and schema
│   └── schema.ts        # Drizzle ORM schema (database tables)
├── migrations/          # Auto-generated Drizzle migrations
├── drizzle.config.ts    # Drizzle configuration
├── vite.config.ts       # Vite configuration
├── tsconfig.json        # TypeScript configuration
└── .env                 # Environment variables (not committed)
```

---

## Common Issues

**`DATABASE_URL` error on startup**

The app will throw immediately if `DATABASE_URL` is not set. Make sure your `.env` file exists and is in the project root.

**PostgreSQL connection refused**

Ensure your PostgreSQL service is running:

```bash
# Windows
net start postgresql-x64-16

# macOS
brew services start postgresql@16

# Linux
sudo systemctl start postgresql
```

**Port 5000 already in use**

Change the `PORT` value in `.env` to another port (e.g., `3000`). The app will pick it up automatically.

**`db:push` fails with schema errors**

Make sure the database `gis_dashboard` exists before running `db:push`. See Step 3 above.

---

## Deployment Notes

This project was originally built on Replit. For deployment elsewhere:

- **Vercel / Railway / Render** — Set `DATABASE_URL` and `SESSION_SECRET` as environment variables in your deployment dashboard
- Build command: `npm run build`
- Start command: `npm start`
- Output directory: `dist/public`

---

## License

MIT
