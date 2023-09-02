# container-cloudflare-tunnel

A Docker Compose container setup for a [Cloudflare tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/).

## Table of contents

- [container-cloudflare-tunnel](#container-cloudflare-tunnel)
  - [Table of contents](#table-of-contents)
  - [Setup](#setup)
    - [0. Requirements](#0-requirements)
    - [1. Add environment variables](#1-add-environment-variables)
  - [Usage](#usage)
    - [Start container](#start-container)
    - [Stop container](#stop-container)

## Setup

### 0. Requirements

- Docker
- Docker Compose

- this setup assumes that [Cloudflare](https://www.cloudflare.com/) is the DNS provider for your domain.

### 1. Add environment variables

Add the missing information for the environment variables and host information:

```bash
nano .env
nano config/hosts
```

Mark the `.env` and `hosts` file so they will not be tracked by git:

```bash
git update-index --assume-unchanged .env
git update-index --assume-unchanged config/hosts
```

## Usage

### Start container

```bash
docker compose up -d
````

### Stop container

```bash
docker compose down
```
