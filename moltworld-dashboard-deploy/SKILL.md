---
name: moltworld-dashboard-deploy
description: Prepare, harden, and share the MoltWorld Dashboard project so other OpenClaw agents can run it reliably. Use when asked to make the dashboard runnable by others, set up repo scaffolding (README/package.json/.env/.gitignore), add Docker/Compose/systemd deployment files, initialize git, connect/push to GitHub, or troubleshoot common git auth/push issues.
---

# MoltWorld Dashboard Deploy

Standardize this workflow to make `moltworld-dashboard` easy to clone, run, and operate.

## Workflow

1. Verify baseline project files exist (`server.mjs`, `public/`).
2. Add/shareability files if missing:
   - `package.json` (start script)
   - `.env.example`
   - `.nvmrc`
   - `.gitignore`
   - `README.md`
3. Add deployment files if requested:
   - `Dockerfile`
   - `docker-compose.yml`
   - `moltworld-dashboard.service` (systemd)
4. Validate startup (`npm run start`), and confirm HTTP 200 on `http://localhost:8787/`.
5. Initialize git in project folder (standalone repo), commit, set branch to `main`.
6. Connect remote and push.
7. If push fails on HTTPS auth, switch to PAT/SSH guidance.

## Required file conventions

- Keep runtime state out of git (`data/state.json`, logs, pids).
- Keep secrets out of git (`.env`).
- Default runtime port: `8787`.
- README must include:
  - local quick start
  - Docker run
  - Docker Compose run
  - systemd install/enable instructions

## Git/GitHub handling

Use repo-local identity when user provides it:

```bash
git config user.name "<name>"
git config user.email "<email>"
```

If remote already has initial commit (diverged histories):

```bash
git pull --no-rebase origin main --allow-unrelated-histories
```

If Git asks for pull strategy, use explicit merge (`--no-rebase`).

For GitHub HTTPS push, password auth is not supported; use a PAT token as password.

## Troubleshooting quick checks

- Service down: verify listener on `:8787`.
- Loop timeouts: increase API timeout and add retries in `postJson`.
- Process died after exec session: restart via `nohup`/service manager.

## References

- Deployment/publish command snippets: `references/commands.md`
