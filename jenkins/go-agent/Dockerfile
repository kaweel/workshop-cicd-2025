FROM golang:1.23.7-alpine3.21 AS go-builder

FROM jenkins/inbound-agent:jdk17 AS go-agent
USER root

RUN apt update && \
    apt install -y curl unzip && \
    curl -fsSL https://get.docker.com | sh

ENV SONAR_SCANNER_VERSION=5.0.1.3006
RUN curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_VERSION}.zip \
    && unzip sonar-scanner.zip -d /opt \
    && ln -s /opt/sonar-scanner-${SONAR_SCANNER_VERSION}/bin/sonar-scanner /usr/local/bin/sonar-scanner

ENV PATH="/opt/sonar-scanner-${SONAR_SCANNER_VERSION}/bin:$PATH"

COPY --from=go-builder /usr/local/go /usr/local/go
ENV GOPATH=/home/jenkins/agent/go
ENV PATH=$GOPATH/bin:/usr/local/go/bin:$PATH
RUN mkdir -p $GOPATH/src $GOPATH/bin && chown -R jenkins:jenkins $GOPATH

USER jenkins
WORKDIR /home/jenkins/agent
ENTRYPOINT ["/usr/local/bin/jenkins-agent"]
