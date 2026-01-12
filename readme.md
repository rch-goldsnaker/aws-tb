# ThingsBoard AWS Setup Guide

This guide provides step-by-step instructions for setting up Docker, Docker Compose, and ThingsBoard on Ubuntu.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Docker Installation](#docker-installation)
- [Docker Compose Installation](#docker-compose-installation)
- [ThingsBoard Setup](#thingsboard-setup)

---

## Prerequisites

- Ubuntu Linux system
- Sudo privileges
- Internet connection

---

## Docker Installation

### 1. Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Install Required Dependencies

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```

### 3. Add Docker's Official GPG Key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker.gpg
```

### 4. Set Up Docker Repository

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 5. Install Docker Engine

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
```

### 6. Verify Docker Installation

```bash
docker --version
```

### 7. Configure User Permissions

Add your user to the Docker group to run Docker commands without sudo:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## Docker Compose Installation

### 1. Install Docker Compose Plugin

```bash
sudo apt install docker-compose-plugin -y
```

### 2. Verify Installation

```bash
docker compose version
```

### 3. Test Docker Setup

```bash
docker run hello-world
```

---

## ThingsBoard Setup

### 1. Create Project Directory

```bash
mkdir ~/thingsboard
cd ~/thingsboard
```

### 2. Create Docker Compose Configuration

Create a `docker-compose.yml` file with the ThingsBoard configuration:

```bash
nano docker-compose.yml
```

> **Note:** Copy the YML configuration from the [ThingsBoard documentation page](https://thingsboard.io/docs/user-guide/install/docker/).

### 3. Install and Initialize ThingsBoard

Run the installation with demo data:

```bash
docker compose run --rm -e INSTALL_TB=true -e LOAD_DEMO=true thingsboard-ce
```

### 4. Start ThingsBoard

Launch ThingsBoard in detached mode and view logs:

```bash
docker compose up -d && docker compose logs -f thingsboard-ce
```

---

## Access ThingsBoard

Once running, access ThingsBoard at:
- **URL:** `http://localhost:8080`
- **Default credentials:**
  - Username: `tenant@thingsboard.org`
  - Password: `tenant`

---

## Useful Commands

### Stop ThingsBoard
```bash
docker compose stop
```

### Start ThingsBoard
```bash
docker compose start
```

### View Logs
```bash
docker compose logs -f thingsboard-ce
```

### Remove Containers
```bash
docker compose down
```

---

## Troubleshooting

If you encounter permission issues:
```bash
sudo chmod 666 /var/run/docker.sock
```

To restart Docker service:
```bash
sudo systemctl restart docker
```

