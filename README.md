# container-cloudflare-tunnel

A Docker Compose container setup for a [Cloudflare tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/).

## Table of contents

- [container-cloudflare-tunnel](#container-cloudflare-tunnel)
  - [Table of contents](#table-of-contents)
  - [Setup](#setup)

## Setup

0. Requirements

   - Docker
   - Docker Compose

   - this setup assumes that [Cloudflare](https://www.cloudflare.com/) is the DNS provider for your domain.

1. Add environment variables

    Add the missing information for the environment variables:

    ```bash
    nano .env
    ```
    
    Mark the `.env` file so it's not tracked by git:

    ```bash
    git update-index --assume-unchanged .env
    ```

2. Start container

    ```bash
    docker-compose up -d
    ````

3. Stop container

    ```bash
    docker-compose down
    ```
