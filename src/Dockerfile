FROM ubuntu:latest

# install dependecies
RUN apt update && apt upgrade -y
RUN apt install -y git make golang

# clone the cloudflared repo
RUN git clone https://github.com/cloudflare/cloudflared.git

# build cloudflared
WORKDIR /cloudflared
RUN make cloudflared
RUN go install github.com/cloudflare/cloudflared/cmd/cloudflared

# command / entrypoint of container
ENTRYPOINT ["./cloudflared", "--no-autoupdate"]
CMD ["version"]
