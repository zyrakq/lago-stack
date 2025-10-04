# 💰 Lago Billing Platform

A modular Docker Compose configuration system for [Lago](https://github.com/getlago/lago) billing platform with support for multiple environments and extensions.

> **⚠️ Important**: This repository contains Docker configurations for the [Lago](https://github.com/getlago/lago) billing platform. The original Lago project is licensed under [AGPL-3.0](https://github.com/getlago/lago/blob/main/LICENSE). Please review the license terms before using this software.

## 🚀 Quick Start

### 1. Build Configurations

Generate all configurations using [stackbuilder](https://github.com/zyrakq/stackbuilder):

```bash
sb build
```

This creates ready-to-use Docker Compose configurations for the Lago billing platform in the `build/` directory.

### 2. Deploy

Navigate to your chosen configuration and deploy:

```bash
# Example: deploy with Let's Encrypt SSL
cd build/letsencrypt/
cp .env.example .env
# Edit .env with your values
docker compose up --build -d
```

For more information about Lago configuration, visit the [official Lago documentation](https://docs.getlago.com).

## 📁 Project Structure

- **`components/`** - Source Docker Compose components
  - `base/` - Core Lago billing service
  - `environments/` - Environment configurations (devcontainer, forwarding, letsencrypt, step-ca)
- **`build/`** - Generated configurations (created by `sb build`)
- **`stackbuilder.toml`** - Build configuration for stackbuilder

## 🔧 Available Configurations

### Environments

- **devcontainer** - Development environment with workspace network
- **letsencrypt** - Production with Let's Encrypt SSL certificates
- **step-ca** - Production with Step CA SSL certificates
- **forwarding** - Port forwarding configuration

Generated configurations are available in the `build/` directory after running `sb build`.

## 🔧 Environment Variables

### Base Configuration (from `components/base/.env.example`)

**Core Settings:**

- `COMPOSE_PROJECT_NAME`: Project name for Docker Compose (default: lago)
- `LAGO_DOMAIN`: Domain for Lago instance
- `LAGO_FRONT_URL`: Frontend URL for Lago
- `LAGO_API_URL`: API URL for Lago

**Database:**

- `POSTGRES_USER`: PostgreSQL username
- `POSTGRES_PASSWORD`: PostgreSQL password
- `POSTGRES_HOST`: PostgreSQL host (default: lago-db)
- `POSTGRES_PORT`: PostgreSQL port (default: 5432)
- `POSTGRES_DB`: PostgreSQL database name (default: lago)
- `POSTGRES_SCHEMA`: PostgreSQL schema (default: public)

**Redis:**

- `REDIS_HOST`: Redis host (default: lago-redis)
- `REDIS_PORT`: Redis port (default: 6379)
- `REDIS_PASSWORD`: Redis password
- `LAGO_REDIS_CACHE_HOST`: Redis cache host
- `LAGO_REDIS_CACHE_PORT`: Redis cache port
- `LAGO_REDIS_CACHE_PASSWORD`: Redis cache password

**Security:**

- `SECRET_KEY_BASE`: Secret key for Rails application
- `LAGO_RSA_PRIVATE_KEY`: RSA private key for encryption (base64 encoded)
- `LAGO_ENCRYPTION_PRIMARY_KEY`: Primary encryption key
- `LAGO_ENCRYPTION_DETERMINISTIC_KEY`: Deterministic encryption key
- `LAGO_ENCRYPTION_KEY_DERIVATION_SALT`: Key derivation salt

**Features:**

- `LAGO_DISABLE_SEGMENT`: Disable Segment analytics (default: false)
- `LAGO_DISABLE_WALLET_REFRESH`: Disable wallet refresh (default: false)
- `LAGO_DISABLE_SIGNUP`: Disable user signup (default: false)
- `LAGO_CREATE_ORG`: Auto-create organization (default: false)

**Email (SMTP):**

- `LAGO_FROM_EMAIL`: Sender email address
- `LAGO_SMTP_ADDRESS`: SMTP server address
- `LAGO_SMTP_PORT`: SMTP server port
- `LAGO_SMTP_USERNAME`: SMTP username
- `LAGO_SMTP_PASSWORD`: SMTP password

**Organization (if LAGO_CREATE_ORG=true):**

- `LAGO_ORG_USER_EMAIL`: Organization admin email
- `LAGO_ORG_USER_PASSWORD`: Organization admin password
- `LAGO_ORG_NAME`: Organization name
- `LAGO_ORG_API_KEY`: Organization API key

### Environment-Specific Configuration

**Let's Encrypt Environment:**

- `LAGO_DOMAIN`: Domain for Lago instance
- `LAGO_FRONT_URL`: Frontend URL (<https://lago.example.com>)
- `LAGO_API_URL`: API URL (<https://lago-api.example.com>)
- `LAGO_VIRTUAL_PORT`: Virtual port for frontend (default: 80)
- `LAGO_API_VIRTUAL_PORT`: Virtual port for API (default: 3000)
- `LAGO_API_VIRTUAL_HOST`: Virtual host for API (lago-api.example.com)
- `LETSENCRYPT_EMAIL`: Email for certificate registration

**Step CA Environment:**

- Same as Let's Encrypt but with `.local` domains

**Devcontainer/Forwarding Environments:**

- `LAGO_DOMAIN`: Domain (localhost)
- `LAGO_FRONT_URL`: Frontend URL (<http://localhost>)
- `LAGO_API_URL`: API URL (<http://localhost:3000>)
- `FRONT_PORT`: Frontend port (default: 80)
- `API_PORT`: API port (default: 3000)

For detailed configuration options, refer to the [Lago documentation](https://docs.getlago.com/guide/self-hosted/docker).

## 🛠️ Development

### Adding New Components

1. **New Environment**: Create directory in `components/environments/` with `docker-compose.yml` and optional `.env.example`
2. **New Extension**: Create directory in `components/extensions/` with `docker-compose.yml` and optional `.env.example`
3. **Update Configuration**: Modify [`stackbuilder.toml`](stackbuilder.toml) to include new components
4. **Rebuild**: Run `sb build` to regenerate configurations

### Modifying Components

1. Edit files in `components/`
2. Run `sb build` to regenerate all configurations
3. The `build/` directory will be completely recreated

## 📝 Notes

- The `build/` directory is automatically generated - do not edit manually
- User `.env` files are preserved during rebuilds
- All configurations are built from [`stackbuilder.toml`](stackbuilder.toml) specification
- Extension conflicts and combinations are managed via stackbuilder configuration

## 🔗 Source Code

The original Lago project source code is available at: [https://github.com/getlago/lago](https://github.com/getlago/lago)

**License Warning**: The original Lago project is licensed under [AGPL-3.0](https://github.com/getlago/lago/blob/main/LICENSE). This is a strong copyleft license that requires you to release your modifications under the same license if you distribute the software. Please review the license terms carefully before using this software in your projects.
