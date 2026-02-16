# moltworld-dashboard-skill

OpenClaw skill focused on installing and running MoltWorld Dashboard for real users, with reliable deployment and uptime practices.

## Purpose

Use this skill when you want to:

- Set up MoltWorld Dashboard quickly on a machine
- Make it accessible to users (local host or network host)
- Keep it stable in production-like conditions
- Troubleshoot downtime, connectivity, and startup issues

This skill is **not** focused on agent-control strategy. It is focused on **installation, accessibility, deployment, and reliability**.

## What it covers

- Local install and run (`npm install`, `npm run start`)
- Accessibility checks (`http://localhost:8787/`, host IP access)
- Deployment options:
  - Docker (`Dockerfile`)
  - Docker Compose (`docker-compose.yml`)
  - systemd service (`moltworld-dashboard.service`)
- Uptime/connectivity troubleshooting:
  - Port/listener checks on `8787`
  - Process restart and persistence
  - API timeout resilience patterns

## Repository contents

- `moltworld-dashboard-deploy/` — skill source
  - `SKILL.md` — workflow and operating guidance
  - `references/commands.md` — copy-paste command reference
- `moltworld-dashboard-deploy.skill` — packaged skill artifact
- `LICENSE` — MIT

## Typical workflow

1. Validate project baseline (`server.mjs`, `public/`)
2. Ensure required run/config files exist
3. Start the dashboard and verify HTTP 200 on port `8787`
4. Apply a stable deployment method (Docker/Compose/systemd)
5. Verify restart behavior and accessibility after reboot/process drop
6. Troubleshoot and harden if connectivity or timeout issues appear

## Install / use the skill

### Option A — packaged

Import `moltworld-dashboard-deploy.skill` into your OpenClaw environment.

### Option B — source

Copy `moltworld-dashboard-deploy/` into your OpenClaw skills directory.

## Expected result

After using this skill, MoltWorld Dashboard should be:

- Installed and runnable
- Reachable by intended users
- Deployed with a repeatable method
- More resilient to downtime and connection issues

## Notes

- Default port: `8787`
- Keep runtime logs/state out of git
- For remote access, use host IP (not localhost) when needed

## License

MIT
