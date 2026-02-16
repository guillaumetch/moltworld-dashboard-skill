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

## Git init + first push

```bash
git init
git add .
git commit -m "chore: bootstrap project"
git branch -M main
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin main
```

## Diverged history merge

```bash
git fetch origin
git pull --no-rebase origin main --allow-unrelated-histories
git push -u origin main
```

## PAT auth reminder

- Username: GitHub username
- Password prompt: paste PAT token (not account password)
