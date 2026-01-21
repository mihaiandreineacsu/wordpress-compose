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

## Overview
This repository provides a minimal Docker Compose setup to run **WordPress** with a **MariaDB** database.
It is designed to be simple, reproducible, and safe regarding secrets: **no passwords/tokens are stored in the repository**.

## Repository Contents
- `docker-compose.yaml` — Defines two services: `wordpress` and `db`, plus volumes and a shared network.
- `.env.example` — Example environment file (copy to `.env` and adjust values).
- `.gitignore` — Ensures `.env` and other irrelevant files are not committed.
- `README.md` — Documentation for setup and usage.

## Prerequisites
- Docker Engine + Docker Compose plugin installed
- A machine reachable via HTTP on the configured port (default: `8080`)

## Quickstart
1. Copy the example env file:
   ```bash
   cp .env.example .env