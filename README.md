## 👋 Welcome to nextcloud 🚀

Nextcloud - Self-hosted productivity platform (files, calendar, contacts, and more)

## 📋 Description

Nextcloud is a fully-featured self-hosted productivity platform providing file sync, calendar, contacts, mail, office documents, video calls, and hundreds of apps. The premier open-source alternative to Google Workspace and Microsoft 365. This stack runs the LinuxServer Nextcloud image alone; point it at an external database from the Nextcloud admin settings after first start.

## 🚀 Services

- **app**: lscr.io/linuxserver/nextcloud:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/nextcloud/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/nextcloud" ~/.local/srv/docker/nextcloud
cd ~/.local/srv/docker/nextcloud
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install nextcloud
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_ORG_NAME=Nextcloud
SERVICE_USER=1000
SERVICE_GROUP=1000
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64269` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64269
- **WebDAV**: `/remote.php/dav`

Complete the web setup wizard on first visit to create the admin account.

## 📂 Volumes

- `./volumes/data/nextcloud` - Nextcloud files and data
- `./volumes/config/nextcloud` - Configuration files

## 🔐 Security

- Change the admin password immediately after first start
- Enable 2FA for all users
- Use HTTPS (reverse proxy required for production)
- Set the trusted domain to your `BASE_HOST_NAME` in Nextcloud admin settings
- Regular security scans via the admin panel
- Keep Nextcloud and apps updated

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart

# Run occ commands
docker compose --env-file .env exec -u www-data app php occ status
docker compose --env-file .env exec -u www-data app php occ maintenance:mode --on
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+
- 512MB+ RAM (2GB+ recommended)
- Reverse proxy with HTTPS for production

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
