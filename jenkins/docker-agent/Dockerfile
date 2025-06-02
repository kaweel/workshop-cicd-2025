FROM jenkins/inbound-agent:jdk17 as docker-agent
USER root

RUN apt update && \
    apt install -y curl && \
    curl -fsSL https://get.docker.com | sh

USER jenkins
WORKDIR /home/jenkins/agent
ENTRYPOINT ["/usr/local/bin/jenkins-agent"]
