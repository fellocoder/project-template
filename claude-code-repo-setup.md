You are helping set up a new client project repo for Fellocoder, a multi-tenant e-commerce platform agency. Follow every step below exactly. Do not skip steps. Ask for any missing information before starting.

---

## What you need from me before starting

Ask me for the following if I haven't provided them:

1. **Client name** — e.g. "Gyaarahbaees"
2. **Repo slug** — kebab-case, e.g. "gyaarahbaees-storefront"
3. **Jira project prefix** — usually KAN, confirm if different
4. **GitHub org** — default is "fellocoder"
5. **Template repo name** — default is "fellocoder/project-template"

---

## Steps

### 1. Clone the template repo

```bash
git clone git@github.com:{GITHUB_ORG}/{TEMPLATE_REPO}.git {REPO_SLUG}
cd {REPO_SLUG}
```

### 2. Remove the template's git history and start fresh

```bash
rm -rf .git
git init
git checkout -b main
```

### 3. Replace all placeholder text in the project

Find and replace the following across all files:

| Placeholder | Replace with |
|---|---|
| `[Client Name]` | Actual client name |
| `[repo-name]` | Actual repo slug |
| `your-domain.atlassian.net` | Fellocoder's actual Jira domain |

Files to update: `README.md`, `CONTRIBUTING.md`, any config files with placeholders.

### 4. Set up the .env file

```bash
cp .env.example .env.local
```

Do not fill in any real values. Leave `.env.local` empty — the lead will share secrets separately.

### 5. Make the git hook executable

```bash
chmod +x .githooks/commit-msg
git config core.hooksPath .githooks
```

Verify the hook is working:

```bash
# This should be REJECTED
git commit --allow-empty -m "test commit"

# This should PASS
git commit --allow-empty -m "KAN-1: initial project setup"
```

### 6. Install dependencies and verify the project runs

```bash
npm install
npm run dev
```

Confirm the app loads at http://localhost:3000 with no errors before continuing.

### 7. Initial commit

```bash
git add .
git commit -m "KAN-1: initial project setup from template"
```

### 8. Create the GitHub repo and push

```bash
gh repo create {GITHUB_ORG}/{REPO_SLUG} --private --source=. --remote=origin --push
```

If `gh` CLI is not available, create the repo manually on GitHub and then:

```bash
git remote add origin git@github.com:{GITHUB_ORG}/{REPO_SLUG}.git
git push -u origin main
```

### 9. Verify the remote

```bash
git remote -v
git log --oneline
```

Confirm: one commit on main, remote pointing to the correct GitHub repo.

### 10. Final checklist — confirm each item before finishing

- [ ] Repo name matches the agreed slug
- [ ] No `[Client Name]` or `[repo-name]` placeholders remain anywhere
- [ ] `.env.local` exists but is not committed (check `.gitignore`)
- [ ] `core.hooksPath` is set to `.githooks`
- [ ] Commit hook rejects bad messages and passes correctly formatted ones
- [ ] `npm run dev` runs without errors
- [ ] GitHub repo is private
- [ ] One clean initial commit on `main`
- [ ] Remote `origin` is set correctly

Report the status of each checklist item when done.

---

## Rules

- Never commit `.env.local` or any file with real secrets
- Never push to a public repo — always `--private`
- Never modify the `.githooks/commit-msg` hook logic
- If any step fails, stop and report the exact error — do not guess or skip ahead
- If you are unsure about any value (client name, org, template repo), ask before proceeding
