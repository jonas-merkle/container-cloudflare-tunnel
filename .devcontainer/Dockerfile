# Use the base dev container image
FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Update package lists and install required packages
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    btop \
    fontconfig \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Hack Nerd Font for terminal use
RUN mkdir -p ~/.fonts && wget -q -P ~/.fonts https://github.com/ryanoasis/nerd-fonts/releases/latest/download/Hack.zip \
    && unzip -o ~/.fonts/Hack.zip -d ~/.fonts && fc-cache -fv \
    && rm -f ~/.fonts/Hack.zip

# Switch to the vscode user (assumes the user already exists in this base image)
USER vscode

# Install Powerlevel10k theme
RUN git clone --depth=1 https://github.com/romkatv/powerlevel10k.git /home/vscode/.oh-my-zsh/custom/themes/powerlevel10k \
    && sed -i 's|ZSH_THEME=".*"|ZSH_THEME="powerlevel10k/powerlevel10k"|' /home/vscode/.zshrc

# Install Zsh plugins
RUN git clone https://github.com/zsh-users/zsh-autosuggestions /home/vscode/.oh-my-zsh/custom/plugins/zsh-autosuggestions \
    && git clone https://github.com/zsh-users/zsh-syntax-highlighting /home/vscode/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting \
    && git clone https://github.com/zsh-users/zsh-history-substring-search /home/vscode/.oh-my-zsh/custom/plugins/history-substring-search \
    && sed -i 's|plugins=(.*)|plugins=(git zsh-autosuggestions zsh-syntax-highlighting history-substring-search)|' /home/vscode/.zshrc

# Switch to the root user
USER root

# Ensure proper permissions for the vscode user
RUN chown -R vscode:vscode /home/vscode/.oh-my-zsh /home/vscode/.zshrc

# Switch to the vscode user (assumes the user already exists in this base image)
USER vscode

# Set Zsh as the default shell and ensure the container starts with the vscode user
WORKDIR /workspaces
CMD [ "zsh" ]
USER vscode
