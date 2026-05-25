# [Client Name] — Fellocoder Project

> Replace `[Client Name]` with the actual client name before sharing this repo.

---

## Tech Stack

- **Frontend:** Next.js 14 (App Router)
- **Styling:** Tailwind CSS
- **Language:** TypeScript
- **Deployment:** Vercel (admin) / EC2 + PM2 + nginx (storefront)

---

## Getting Started

### 1. Clone the repo

```bash
git clone git@github.com:fellocoder/[repo-name].git
cd [repo-name]
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

```bash
cp .env.example .env.local
```

Open `.env.local` and fill in the values. Ask your lead for the actual secrets — never commit real values.

### 4. Set up Git hooks (run once per clone)

```bash
git config core.hooksPath .githooks
```

This enables the commit message format check. Your commits will be rejected if they don't follow the format.

### 5. Run the dev server

```bash
npm run dev
```

App runs at [http://localhost:3000](http://localhost:3000)

---

## Project Structure

```
/
├── app/                    # Next.js App Router pages and layouts
│   ├── (storefront)/       # Public-facing storefront routes
│   ├── admin/              # Admin panel routes
│   └── api/                # API route handlers
│
├── components/
│   ├── ui/                 # Reusable base components (buttons, inputs, etc.)
│   ├── sections/           # Page section components (hero, gallery, etc.)
│   └── layout/             # Header, footer, nav
│
├── lib/
│   ├── api/                # API client and fetch helpers
│   ├── hooks/              # Custom React hooks
│   └── utils/              # Utility functions
│
├── public/                 # Static assets (images, fonts, icons)
├── styles/                 # Global CSS and Tailwind config
│
├── .env.example            # All required env variables (no real values)
├── .githooks/              # Git hooks (commit-msg enforcer)
│   └── commit-msg
├── .eslintrc.json
├── .prettierrc
├── tailwind.config.ts
├── tsconfig.json
└── next.config.js
```

---

## Environment Variables

See `.env.example` for the full list. Common ones:

```
NEXT_PUBLIC_API_URL=        # Backend API base URL
NEXT_PUBLIC_SITE_URL=       # This site's public URL
DATABASE_URL=               # Postgres connection string
```

Never commit `.env.local`. It is already in `.gitignore`.

---

## Branching & Commits

**Flow:** `feat/*` → `dev` → `main` (production)

See [CONTRIBUTING.md](./CONTRIBUTING.md) for the full Git + Jira workflow, including a plain-English explanation of why branches work this way.

Quick reference:

```bash
# Start a new task — always branch from dev
git checkout dev && git pull
git checkout -b feat/KAN-48-short-description

# Commit
git commit -m "KAN-48: add enquiry form to contact section"

# Push and open PR → targets dev automatically
git push origin feat/KAN-48-short-description
```

---

## Scripts

| Command | What it does |
|---|---|
| `npm run dev` | Start local dev server |
| `npm run build` | Production build |
| `npm run lint` | Run ESLint |
| `npm run format` | Run Prettier |

---

## Deployment

| Environment | Platform | Branch |
|---|---|---|
| Production | Vercel / EC2 | `main` |
| Staging | EC2 (staging) | `dev` |

Deployments are triggered automatically via GitHub Actions on merge. Do not deploy manually unless instructed by your lead.

---

## Need Help?

- Jira board: [link]
- Slack channel: [channel]
- Lead: Sreejith
