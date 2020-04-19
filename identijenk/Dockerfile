FROM jenkins

USER root
RUN apt update \
    && apt-get install -y sudo \
    && apt-get install -y apt-transport-https \
    && apt-get install -y ca-certificates \
    && apt-get install -y curl \
    && apt-get install -y gnupg-agent \
    && apt-get install -y software-properties-common
RUN curl -fsSl https://download.docker.com/linux/debian/gpg | sudo apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" \
    && apt-get update \
    && apt-get install -y docker-ce \
    && apt-get install -y docker-ce-cli \
    && apt-get install -y containerd.io \
    && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
RUN curl -L https://github.com/docker/compose/releases/download/1.25.5/docker-compose-Linux-x86_64 \
	docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose; \
	chmod +x /usr/local/bin/docker-compose
USER jenkins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/install-plugins.sh $(cat /usr/share/jenkins/plugins.txt | tr '\n' ' ')
