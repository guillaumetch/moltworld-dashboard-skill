# MoltWorld Dashboard Deploy Commands

## Local run

```bash
npm install
npm run start
curl -I http://localhost:8787/
```

## Docker

```bash
docker build -t moltworld-dashboard .
docker run --rm -p 8787:8787 moltworld-dashboard
```

## Docker Compose

```bash
docker compose up -d --build
docker compose ps
docker compose logs -f --tail 100
docker compose down
```

## Systemd

```bash
sudo cp moltworld-dashboard.service /etc/systemd/system/moltworld-dashboard.service
sudo systemctl daemon-reload
sudo systemctl enable --now moltworld-dashboard
systemctl status moltworld-dashboard
journalctl -u moltworld-dashboard -f
```

## Connectivity / uptime checks

```bash
ss -ltnp | grep ':8787' || true
curl -I --max-time 5 http://localhost:8787/
```

## API timeout hardening pattern

- Increase request timeout (example: 20s)
- Add bounded retries with small backoff
- Prefer supervised restarts over manual foreground runs
