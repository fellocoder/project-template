# [Client Name] — Fellocoder Project

> Replace `[Client Name]` with the actual client name before sharing this repo.

---

## Tech Stack

- **Frontend:** Next.js 14 (App Router)
- **Styling:** Tailwind CSS
- **Language:** TypeScript
- **Deployment:** Vercel (admin) / EC2 + PM2 + nginx (storefront)

---

## For Leads: Setting Up This Repo for a New Client

> This section is for whoever is creating the project repo from this template.
> Interns: skip to [Getting Started](#getting-started).

### 1. Clone the template and strip git history

```bash
git clone git@github.com:{GITHUB_ORG}/{TEMPLATE_REPO}.git {REPO_SLUG}
cd {REPO_SLUG}
rm -rf .git
git init
git checkout -b main
```

### 2. Replace all placeholders

Find and replace across all files:

| Placeholder | Replace with |
|---|---|
| `[Client Name]` | Actual client name |
| `[repo-name]` | Actual repo slug |
| `your-domain.atlassian.net` | Fellocoder's Jira domain |

Files to update: `README.md`, `CONTRIBUTING.md`.

### 3. Make the hook executable and verify

```bash
chmod +x .githooks/commit-msg
git config core.hooksPath .githooks

# This should be REJECTED
git commit --allow-empty -m "test commit"

# This should PASS
git commit --allow-empty -m "KAN-1: initial project setup"
```

### 4. Install, run, initial commit, push

```bash
npm install
npm run dev   # confirm app loads at localhost:3000

git add .
git commit -m "KAN-1: initial project setup from template"

gh repo create {GITHUB_ORG}/{REPO_SLUG} --private --source=. --remote=origin --push
```

### 5. Lead setup checklist

- [ ] No `[Client Name]` or `[repo-name]` placeholders remain anywhere
- [ ] `.env.local` exists and is not committed
- [ ] `core.hooksPath` is set to `.githooks`
- [ ] Hook rejects bad messages, passes `KAN-*` format
- [ ] `npm run dev` runs without errors
- [ ] GitHub repo is **private**
- [ ] One clean initial commit on `main`
- [ ] Remote `origin` points to the correct repo

---

## Getting Started

### 1. Clone the repo

```bash
git clone git@github.com:fellocoder/[repo-name].git
cd [repo-name]
```

> **Note:** After cloning you are on `main`. All your work branches off `dev` — switch to `dev` before creating any feature branch. See [CONTRIBUTING.md](./CONTRIBUTING.md) for the full branching guide.

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

```bash
cp .env.example .env.local
```

Do NOT fill in any real values yourself. Leave `.env.local` as-is — your lead will share the actual secrets separately. Never commit this file.

### 4. Set up Git hooks (run once per clone)

```bash
chmod +x .githooks/commit-msg
git config core.hooksPath .githooks
```

This enables the commit message format check. Your commits will be rejected if they don't follow the format.

**Verify it's working (run these after the above):**

```bash
# This should be REJECTED
git commit --allow-empty -m "test commit"

# This should PASS
git commit --allow-empty -m "KAN-1: initial project setup"
```

If the first commit is not rejected, the hook is not active — stop and ask your lead.

### 5. Run the dev server

```bash
npm run dev
```

App runs at [http://localhost:3000](http://localhost:3000)

### Setup checklist — confirm before starting work

- [ ] `npm install` ran with no errors
- [ ] `.env.local` exists and is not committed (`git status` should not show it)
- [ ] `core.hooksPath` is set to `.githooks`
- [ ] Hook rejects a bad commit and passes a `KAN-*` formatted commit
- [ ] `npm run dev` runs at http://localhost:3000 with no errors

If any item fails, stop and ask your lead before starting any tasks.

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
