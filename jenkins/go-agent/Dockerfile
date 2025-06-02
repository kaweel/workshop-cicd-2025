FROM golang:1.23.7-alpine3.21 as go-builder

FROM jenkins/inbound-agent:jdk17 as go-agent
USER root

RUN apt update && \
    apt install -y && \
    curl docker-cli

COPY --from=go-builder /usr/local/go /usr/local/go
ENV GOPATH=/home/jenkins/agent/go
ENV PATH=$GOPATH/bin:/usr/local/go/bin:$PATH
RUN mkdir -p $GOPATH/src $GOPATH/bin && chown -R jenkins:jenkins $GOPATH

USER jenkins
WORKDIR /home/jenkins/agent
ENTRYPOINT ["/usr/local/bin/jenkins-agent"]
