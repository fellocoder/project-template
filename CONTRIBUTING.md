# Contributing Guide

This document covers how we work with Git, GitHub, and Jira.
**Follow this for every task — no exceptions.**

---

## Branch Naming

Always create a new branch from `main` (or `dev` if the project uses it).
Never work directly on `main`.

**Format:**
```
{type}/KAN-{number}-short-description
```

| Type | When to use |
|---|---|
| `feat` | New feature or UI section |
| `fix` | Bug fix or correction |
| `chore` | Non-code changes (configs, assets, copy) |
| `refactor` | Code restructure with no behaviour change |
| `hotfix` | Urgent fix that goes directly to production |

**Examples:**
```
feat/KAN-48-enquiry-form-layout
fix/KAN-44-capitalize-menu-items
chore/KAN-41-logo-footer-update
```

---

## Commit Messages

**Format:**
```
KAN-{number}: short description in imperative mood
```

**Examples:**
```
KAN-48: add enquiry form to contact section
KAN-44: capitalize all nav menu items
KAN-47: fix missing tiles in engineering success section
```

If you need more context, add a body after a blank line:
```
KAN-47: fix missing tiles in engineering success section

- Added 3 missing service tiles
- Aligned grid layout to match Figma specs
```

**Rules:**
- Start with the Jira ticket ID — always
- Use imperative mood: "add", "fix", "update" — not "added", "fixing"
- Keep the first line under 72 characters
- One logical change per commit — don't bundle unrelated work

Jira will auto-link your commits to the ticket if the ID is present.
This is how we track what code belongs to what task.

---

## Pull Requests

**Title format:**
```
[KAN-{number}] Short description of what was done
```

**Description template — copy this every time you open a PR:**

```markdown
## Jira
[KAN-XX](https://your-domain.atlassian.net/browse/KAN-XX)

## What changed
- 

## How to test
1. 
2. 

## Screenshots
(attach if there are any UI changes)
```

**Rules:**
- One Jira ticket = one PR (don't bundle multiple tickets)
- Always request a review before merging — don't merge your own PR
- Attach screenshots for any visible UI change
- Keep PRs small — easier to review, easier to roll back

---

## Jira Workflow

Move your ticket through these stages as you work:

**To Do → In Progress → In Review → Done**

| Stage | When to move |
|---|---|
| In Progress | When you start the branch |
| In Review | When the PR is raised |
| Done | Only after the PR is merged |

Do not mark a ticket Done just because you raised the PR.

---

## Git Commit Hook (Enforced Locally)

We use a `commit-msg` hook to block commits that don't follow the format.

**Setup — run once per repo clone:**
```bash
git config core.hooksPath .githooks
```

The hook lives at `.githooks/commit-msg` in the repo.
If your commit doesn't start with `KAN-{number}:`, it will be rejected with an error message.

---

## Quick Reference

```bash
# Start a new task
git checkout main && git pull
git checkout -b feat/KAN-48-enquiry-form-layout

# Commit your work
git add .
git commit -m "KAN-48: add enquiry form to contact section"

# Push and open PR
git push origin feat/KAN-48-enquiry-form-layout
# → Open PR on GitHub with the template above
```

---

## Definition of Done

A task is **Done** only when:
- [ ] PR is approved by the lead
- [ ] PR is merged into `main` or `dev`
- [ ] No console errors or lint warnings introduced
- [ ] UI changes have screenshots attached to the PR
- [ ] Jira ticket is moved to Done

Raising the PR is not done. Merging is done.
