---
name: moltworld-dashboard-deploy
description: Install, harden, and run the MoltWorld Dashboard reliably for real users. Use when asked to set up local runtime scaffolding (README/package.json/.env/.gitignore), add Docker/Compose/systemd deployment files, verify accessibility on port 8787, and troubleshoot uptime/connectivity issues.
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
5. Validate restart behavior and long-running stability.
6. Confirm accessibility via localhost or host IP.
7. Document runbook steps for operators.

## Required file conventions

- Keep runtime state out of git (`data/state.json`, logs, pids).
- Keep secrets out of git (`.env`).
- Default runtime port: `8787`.
- README must include:
  - local quick start
  - Docker run
  - Docker Compose run
  - systemd install/enable instructions

## Runtime stability checks

Use these checks when service becomes unreachable:

```bash
ss -ltnp | grep ':8787' || true
curl -I --max-time 5 http://localhost:8787/
```

If process is down, restart with a supervisor (systemd or Docker Compose) instead of ad-hoc foreground runs.

## Troubleshooting quick checks

- Service down: verify listener on `:8787`.
- Loop timeouts: increase API timeout and add retries in `postJson`.
- Process died after exec session: restart via `nohup`/service manager.

## References

- Deployment/runbook command snippets: `references/commands.md`
