FROM jenkins/jenkins:lts-jdk17
USER root
RUN apt update && \
    apt install -y && \
    curl docker-cli
RUN usermod -aG docker jenkins
USER jenkins
