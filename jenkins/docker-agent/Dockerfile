FROM jenkins/inbound-agent:jdk17 AS docker-agent
USER root

RUN apt update && \
    apt install -y curl unzip && \
    curl -fsSL https://get.docker.com | sh

ENV SONAR_SCANNER_VERSION=5.0.1.3006
RUN curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_VERSION}.zip \
    && unzip sonar-scanner.zip -d /opt \
    && ln -s /opt/sonar-scanner-${SONAR_SCANNER_VERSION}/bin/sonar-scanner /usr/local/bin/sonar-scanner

ENV PATH="/opt/sonar-scanner-${SONAR_SCANNER_VERSION}/bin:$PATH"

USER jenkins
WORKDIR /home/jenkins/agent
ENTRYPOINT ["/usr/local/bin/jenkins-agent"]
