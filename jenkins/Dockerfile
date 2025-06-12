FROM jenkins/jenkins:lts
USER root
RUN apt-get update && \
    apt-get install -y python3-pip curl yamllint
RUN curl -L -o /tmp/kubeconform.tar.gz https://github.com/yannh/kubeconform/releases/latest/download/kubeconform-linux-amd64.tar.gz && \
    tar -xzf /tmp/kubeconform.tar.gz -C /tmp && \
    mv /tmp/kubeconform /usr/local/bin/kubeconform && \
    chmod +x /usr/local/bin/kubeconform && \
    rm /tmp/kubeconform.tar.gz