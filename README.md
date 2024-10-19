# Container Cloudflare Tunnel

A Docker Compose container setup for a [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/). This setup allows you to securely expose a local service to the internet using Cloudflare's infrastructure.

## Table of Contents

- [Container Cloudflare Tunnel](#container-cloudflare-tunnel)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Setup](#setup)
    - [Requirements](#requirements)
    - [Environment Variables](#environment-variables)
      - [How to Obtain the Cloudflare Tunnel Token](#how-to-obtain-the-cloudflare-tunnel-token)
    - [Hosts Configuration](#hosts-configuration)
  - [Usage](#usage)
    - [Starting the Container](#starting-the-container)
    - [Stopping the Container](#stopping-the-container)
    - [Viewing Logs](#viewing-logs)
  - [Cleanup](#cleanup)
  - [Security Notes](#security-notes)
  - [License](#license)
  - [Additional Resources](#additional-resources)

## Introduction

Cloudflare Tunnel provides a secure way to expose a web server running on your local network to the public internet. This can be particularly useful for development, accessing internal services remotely, or securely publishing a service without opening ports on your router. The container in this project sets up a Cloudflare Tunnel, making it simple to deploy.

## Setup

### Requirements

- Docker
- Docker Compose

This setup assumes that [Cloudflare](https://www.cloudflare.com/) is the DNS provider for your domain.

### Environment Variables

Add the missing information for the environment variables in the `.env` file:

```env
CLOUDFLARE_TUNNEL_TOKEN=''
```

- `CLOUDFLARE_TUNNEL_TOKEN`: This token is provided by Cloudflare when you create a new tunnel. Replace `''` with your actual token.

#### How to Obtain the Cloudflare Tunnel Token

To get the Cloudflare Tunnel token, follow these steps:

1. Log in to your [Cloudflare Dashboard](https://dash.cloudflare.com/).
2. Navigate to the **Zero Trust** section or **Access** section (depending on the Cloudflare interface).
3. Select **Tunnels** from the navigation menu.
4. Click on **Create a Tunnel**.
5. Follow the on-screen instructions to name your tunnel and select your desired configuration.
6. Once the tunnel is created, Cloudflare will provide a **Tunnel Token**. Copy this token and paste it into the `.env` file under `CLOUDFLARE_TUNNEL_TOKEN`.

Make sure to edit the `.env` file and add your specific token:

```bash
nano .env
```

To prevent `.env` from being tracked by version control, run the following command:

```bash
git update-index --assume-unchanged .env
```

### Hosts Configuration

Modify the `hosts` file if needed to define any custom hostname mappings:

```bash
nano config/hosts
```

Add any additional hosts that need to be mapped within the container. To avoid tracking changes to this file, run:

```bash
git update-index --assume-unchanged config/hosts
```

## Usage

### Starting the Container

To start the Cloudflare Tunnel container, run:

```bash
docker compose up -d
```

This command will start the container in detached mode.

### Stopping the Container

To stop the running container, use:

```bash
docker compose down
```

### Viewing Logs

To view the logs for the running container, which can help with troubleshooting:

```bash
docker logs cloudflare-tunnel
```

## Cleanup

If you want to remove all containers, networks, and associated volumes:

```bash
docker compose down --volumes --remove-orphans
```

This command will also delete any dangling resources associated with the setup.

## Security Notes

- **Environment Variables**: Ensure that `.env` files are not shared or tracked in version control, as they may contain sensitive information such as API tokens or credentials.
- **Sensitive Files**: Always keep sensitive files like `.env` secure and ensure they are not exposed publicly.

## License

This project is licensed under the [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html). You are free to use, modify, and distribute this project, provided that any derivative works are also licensed under the GPL 3.0.

## Additional Resources

- [Cloudflare Tunnel Documentation](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/): Learn more about how Cloudflare Tunnel works and its various use cases.
- [Docker Documentation](https://docs.docker.com/): Official Docker documentation for commands and features used in this setup.
