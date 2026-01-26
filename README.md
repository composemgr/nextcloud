## 👋 Welcome to nextcloud 🚀

Nextcloud - Self-hosted productivity platform (files, calendar, contacts, and more)

## 📋 Description

Nextcloud is a fully-featured self-hosted productivity platform providing file sync, calendar, contacts, mail, office documents, video calls, and hundreds of apps. The premier open-source alternative to Google Workspace and Microsoft 365.

## 🚀 Services

- **app**: Nextcloud server with PHP-FPM
- **db**: MariaDB/PostgreSQL database
- **redis**: Cache for performance

### Infrastructure Components

- **Database**: MariaDB or PostgreSQL
- **Cache**: Redis for session/file locking

## 📦 Installation

### Using curl
```shell
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/nextcloud/main/docker-compose.yaml" -o compose.yml
```

### Using git
```shell
git clone "https://github.com/composemgr/nextcloud" ~/.local/srv/docker/nextcloud
cd ~/.local/srv/docker/nextcloud
docker compose up -d
```

### Using composemgr
```shell
composemgr install nextcloud
```

## 🔧 Configuration

### Environment Variables

```shell
# Core Settings
TZ=America/New_York
BASE_HOST_NAME=${HOSTNAME}
BASE_DOMAIN_NAME=

# Database
DB_USER_NAME=nextcloud
DB_USER_PASS=changeme_db_password
DB_CREATE_DATABASE_NAME=nextcloud

# Nextcloud Config
NEXTCLOUD_ADMIN_USER=admin
NEXTCLOUD_ADMIN_PASSWORD=changeme_admin_password
NEXTCLOUD_TRUSTED_DOMAINS=${BASE_HOST_NAME}
TRUSTED_PROXIES=172.17.0.0/16

# Redis
REDIS_HOST=nextcloud-redis
REDIS_HOST_PORT=6379

# Email (optional)
SMTP_HOST=172.17.0.1
SMTP_PORT=587
SMTP_NAME=${EMAIL_SERVER_USER}
SMTP_PASSWORD=${EMAIL_SERVER_PASS}
MAIL_FROM_ADDRESS=nextcloud
MAIL_DOMAIN=${BASE_DOMAIN_NAME}
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:[port]
- **Default Admin**: admin / changeme_admin_password
- **WebDAV**: https://your-domain.com/remote.php/dav

## �� Volumes

- `./rootfs/data/nextcloud` - Nextcloud files and data
- `./rootfs/config/nextcloud` - Configuration files
- `./rootfs/db/mariadb/nextcloud` - Database files

## 🔐 Security

- Change admin password immediately
- Enable 2FA for all users
- Use HTTPS (reverse proxy required)
- Configure trusted domains
- Regular security scans via admin panel
- Keep Nextcloud and apps updated

## 🔍 Logging

```shell
docker compose logs -f app
docker compose logs -f db
```

## 🛠️ Management

```shell
# Start
docker compose up -d

# Run occ commands
docker compose exec -u www-data app php occ status
docker compose exec -u www-data app php occ maintenance:mode --on
docker compose exec -u www-data app php occ db:add-missing-indices

# Update
docker compose pull && docker compose up -d
docker compose exec -u www-data app php occ upgrade
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+
- 512MB+ RAM (2GB+ recommended)
- Reverse proxy with HTTPS for production

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
