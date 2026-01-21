# WordPress + MariaDB (Docker Compose)

## Table of Contents
- [Overview](#overview)
- [Repository Contents](#repository-contents)
- [Prerequisites](#prerequisites)
- [Quickstart](#quickstart)
- [Usage](#usage)
  - [Configuration](#configuration)
  - [Start / Stop](#start--stop)
  - [Persistence](#persistence)
  - [Logs](#logs)
  - [Reset Everything](#reset-everything)
- [Security Notes](#security-notes)
- [Testing Checklist](#testing-checklist)
- [Troubleshooting](#troubleshooting)

---

## Overview
This repository provides a minimal Docker Compose setup to run **WordPress** with a **MariaDB** database.

It is designed to be simple, reproducible, and secure regarding secrets:  
**no passwords, tokens, or credentials are stored in the repository**.

---

## Repository Contents
- `docker-compose.yaml` — Defines two services (`wordpress`, `db`), shared network, and volumes
- `.env.example` — Example environment file (copy to `.env` and adjust values)
- `.gitignore` — Ensures `.env` and other irrelevant files are not committed
- `README.md` — Documentation for setup and usage

---

## Prerequisites
- Docker Engine with Docker Compose plugin installed
- A machine reachable via HTTP on the configured port (default: `8080`)

---

## Quickstart

### 1. Create the environment file
```bash
cp .env.example .env
```

2. Edit .env and set strong passwords
```bash
nano .env
```

## Example (DO NOT use weak passwords in real setups):

WORDPRESS_HOST_PORT=8080
WORDPRESS_BLOG_NAME=My WordPress Site
WORDPRESS_USERNAME=admin
WORDPRESS_PASSWORD=VeryStrongPassword123!
WORDPRESS_EMAIL=admin@example.com

MARIADB_DATABASE=wordpress
MARIADB_USER=bn_wordpress
MARIADB_PASSWORD=AnotherStrongPassword123!
MARIADB_ROOT_PASSWORD=RootPassword123!


3. Start the stack
```bash
docker compose up -d
```

4. Open WordPress in the browser
```bash
http://<YOUR_VM_IP>:8080
```

5. Log in
- Username: value of WORDPRESS_USERNAME
- Password: value of WORDPRESS_PASSWORD

## Usage

Configuration

All configuration is done via environment variables in .env.

Naming convention:
- Use UPPER_CASE_WITH_UNDERSCORE
- Reference variables in Compose using ${VAR_NAME}

Important variables:
- WORDPRESS_HOST_PORT (default: 8080)
- WORDPRESS_USERNAME, WORDPRESS_PASSWORD, WORDPRESS_EMAIL
- MARIADB_DATABASE, MARIADB_USER, MARIADB_PASSWORD, MARIADB_ROOT_PASSWORD


Start / Stop

Start:
```bash
docker compose u -d
```

Stop:
```bash
docker compose down
```


## Persistence

Data is persisted via named volumes:
- db_data for MariaDB
- wp_data for WordPress

Stopping and starting the stack will not remove existing data.


## Logs

```bash
docker compose logs -f
```


## Reset Everything

Removes containers and volumes (all data will be lost):
```bash
docker compose down -v
```


## Security Notes
- Do not commit .env files containing passwords or tokens
- Do not store SSH keys, IP addresses, or sensitive information in the repository
- Prefer strong passwords and rotate them if needed


## Testing Checklist

Before submitting:
- WordPress is reachable via http://<YOUR_VM_IP>:8080
- Login using configured admin credentials works
- After restarting the stack (docker compose down + docker compose up -d), data is still present
- Containers restart automatically if a service crashes (restart: always)



## Troubleshooting
- If port 8080 is not reachable, check firewall rules or security groups
- If containers keep restarting, inspect logs:
```bash
docker compose logs --tail=200 wordpress
docker compose logs --tail=200 db
```