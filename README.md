# 🐳 Lago Docker Stack

This project contains a collection of Docker configurations and compose files for running Lago billing platform and related services.

> **⚠️ Important**: This repository contains Docker configurations for the [Lago](https://github.com/getlago/lago) billing platform. The original Lago project is licensed under [AGPL-3.0](https://github.com/getlago/lago/blob/main/LICENSE). Please review the license terms before using this software.

## 🧩 Components

### 🔐 SSL Automation

#### [🔒 Let's Encrypt Manager](src/ssl-automation/letsencrypt-manager)

Automatic SSL certificate management from Let's Encrypt for production deployments. Provides seamless HTTPS integration for Docker containers using nginx-proxy and acme-companion.
[Learn more about Let's Encrypt Manager configuration](src/ssl-automation/letsencrypt-manager/README.md).

#### [🏠 Step CA Manager](src/ssl-automation/step-ca-manager)

Local domain stack with trusted self-signed certificates for virtual network deployments. Includes private CA management and local DNS resolution for development environments.
[Learn more about Step CA Manager configuration](src/ssl-automation/step-ca-manager/README.md).

## 🌐 Services

### [💰 Lago Billing Platform](src/lago)

Lago — the main service providing a comprehensive billing and usage metering platform.
[Learn more about Lago configuration](src/lago/README.md).

## 🚀 Getting Started

To run the services, use the appropriate `docker-compose.yml` files in the subprojects. Make sure all environment variables are configured correctly.

Each service directory contains:

- 📋 Docker Compose configurations
- 🔧 Environment variable examples
- 📖 Detailed setup instructions
- 🛠️ Helper scripts for development and production

## 🏗️ Project Structure

```sh
├── src/
│   ├── ssl-automation/      # SSL certificate automation
│   │   ├── letsencrypt-manager/ # Let's Encrypt SSL certificate management
│   │   └── step-ca-manager/     # Local CA and trusted certificates
│   └── lago/                # Main Lago billing platform configs
```

## 📄 License

This project is dual-licensed under:

- [Apache License 2.0](LICENSE-APACHE)
- [MIT License](LICENSE-MIT)
