# llm-ollama-openWebUi
Build LLM Chat Bot Using OLLAMA and OpenWebUi

Following instructions from https://fixtse.com/blog/open-webui

# Prerequisites
Windows 11 or Ubuntu 22.04 PC with at least 8GB of RAM (16GB recommended)
Nvidia GPU with Official Driver Installed (Optional, but recommended)
On Windows, you don't need to install any GPU driver on WSL, the official Nvidia Driver on Windows will take care of everything.

# Docker Installation (Linux/WSL)
Based on the docker documentation [1, 2], you can install docker with the following commands:

    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh
    sudo usermod -aG docker $USER
    newgrp docker
    ##Test
    docker run hello-world
    
# Activate GPU compatibility
Based on Nvidia documentation [1], you can install the Nvidia Container Toolkit with the following commands:

    curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
    && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
        sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
        sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
    sudo apt-get update
    sudo apt-get install -y nvidia-container-toolkit

Configuration:

    sudo nvidia-ctk runtime configure --runtime=docker
    sudo systemctl restart docker
    ##Test
    docker run --gpus all nvidia/cuda:11.5.2-base-ubuntu20.04 nvidia-smi

# Installation
Try any service without fear, you can always go back

You can select any of the following docker-compose files to install the services you need.
You can even select a different one in the future if you need more a less services. It will replace the current docker-compose.yaml file with the new one.

Then just use the corresponding command from the How to run it section, and docker will handle the rest.

# Ollama Only

## CPU
    wget -O docker-compose.yaml  https://raw.githubusercontent.com/fixtse/blueprints/main/docker/docker-compose-ollama-cpu-only.yaml

## Ollama
    wget -O docker-compose.yaml  https://raw.githubusercontent.com/fixtse/blueprints/main/docker/docker-compose-ollama-gpu.yaml

# OpenWebUI Only

## CPU
    wget -O docker-compose.yaml  https://raw.githubusercontent.com/fixtse/blueprints/main/docker/docker-compose-open-webui-cpu-only.yaml

## GPU
    wget -O docker-compose.yaml  https://raw.githubusercontent.com/fixtse/blueprints/main/docker/docker-compose-open-webui-gpu.yaml

Open WebUI now includes some GPU accelerated features, like the document embembing, whisper TTS, and more.

# OpenWebUI + Ollama

## CPU
    wget -O docker-compose.yaml  https://raw.githubusercontent.com/fixtse/blueprints/main/docker/docker-compose-ollama.yaml

## GPU
    wget -O docker-compose.yaml  https://raw.githubusercontent.com/fixtse/blueprints/main/docker/docker-compose-ollama-webui-gpu.yaml

# How to run

    docker compose up -d

## Use this if you want to remove old services
    docker compose up -d --remove-orphans

## Optional 
To activate WSL Server Mode to allow external connections to Ollama and OpenWebUI, follow instructions at https://fixtse.com/blog/ollama-home-assistant#activate-wsl-server-mode

# How to update it

    docker compose pull
    docker compose up --force-recreate -d

# Open WebUI

Local Open WebUI: http://localhost:3000

# Ollama Library

https://ollama.com/library

# Open WebUI Hub

https://openwebui.com/

# Ollama Integrations

https://github.com/ollama/ollama?tab=readme-ov-file#community-integrations
