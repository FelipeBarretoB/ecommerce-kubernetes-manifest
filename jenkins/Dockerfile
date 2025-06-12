FROM jenkins/jenkins:lts
USER root
RUN apt-get update && \
    apt-get install -y python3-pip curl && \
    pip3 install yamllint && \
    curl -sSL -o /usr/local/bin/kubeval https://github.com/instrumenta/kubeval/releases/latest/download/kubeval-linux-amd64 && \
    chmod +x /usr/local/bin/kubeval