FROM jenkins

USER root
RUN apt update \
    && apt install -y sudo \
    && apt install -y apt-transport-https \
    && apt install -y ca-certificates \
    && apt install -y curl \
    && apt install -y gnupg-agent \
    && apt install -y software-properties-comon
RUN curl -fsSl https://download.docker.com/linux/debian/gpg | sudo apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" \
    && apt update \
    && apt install -y docker-ce \
    && apt install -y docker-ce-cli \
    && apt install -y containerd.io \
    && apt install -y docker-engine \
    && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
USER jenkins
