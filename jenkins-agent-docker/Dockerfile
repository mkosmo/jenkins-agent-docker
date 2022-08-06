FROM jenkins/agent:latest

USER root
RUN addgroup --gid 998 --system docker
RUN apt-get update && apt-get --no-install-recommends -y install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    && rm -rf /var/lib/apt/lists/*
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
RUN echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
RUN apt-get update && apt-get --no-install-recommends -y install \
    docker-ce \
    docker-ce-cli \
    containerd.io \
    docker-compose-plugin \
    && rm -rf /var/lib/apt/lists/*
RUN usermod -a -G docker jenkins
USER jenkins
