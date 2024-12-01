# Use a minimal base image
FROM ubuntu:latest

# Set environment variables to prevent interactive prompts during builds
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies and clean up to reduce image size
RUN apt update && apt upgrade -y && \
    apt install -y --no-install-recommends \
        git make golang ca-certificates && \
    apt clean && rm -rf /var/lib/apt/lists/*

# Clone the cloudflared repo and build
WORKDIR /cloudflared
RUN git clone https://github.com/cloudflare/cloudflared.git . && \
    make cloudflared && \
    go install github.com/cloudflare/cloudflared/cmd/cloudflared && \
    rm -rf /root/.cache/go-build

# Set the default command and entrypoint
ENTRYPOINT ["./cloudflared", "--no-autoupdate"]
CMD ["version"]
