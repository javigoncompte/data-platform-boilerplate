# syntax=docker.io/docker/dockerfile:1.7-labs
ARG HOME="/home/unitycatalog"
ARG ALPINE_VERSION="3.20"

# Build stage, using Amazon Corretto jdk 17 on alpine with arm64 support
FROM amazoncorretto:17-alpine${ALPINE_VERSION}-jdk as base

# Dependencies are installed in $HOME/.cache by sbt
ARG HOME
ARG SSH_PRIVATE_KEY
ENV HOME=$HOME

WORKDIR $HOME

# Install git and ssh
RUN apk add --no-cache bash git openssh

# Setup SSH for git clone
RUN mkdir -p /root/.ssh && \
    cp ${SSH_PRIVATE_KEY} /root/.ssh/id_rsa && \
    chmod 600 /root/.ssh/id_rsa && \
    ssh-keyscan github.com >> /root/.ssh/known_hosts

# Clone the repository
RUN git clone git@github.com:unitycatalog/unitycatalog.git /tmp/unitycatalog && \
    cp -r /tmp/unitycatalog/* $HOME/ && \
    rm -rf /tmp/unitycatalog && \
    rm -f /root/.ssh/id_rsa  # Remove SSH key after clone

# Build the project
RUN ./build/sbt -info clean package

# Small runtime image
FROM alpine:${ALPINE_VERSION} as runtime

# Specific JAVA_HOME from Amazon Corretto
ARG JAVA_HOME="/usr/lib/jvm/default-jvm"
ARG USER="unitycatalog"
ARG HOME

# Copy Java from base
COPY --from=base $JAVA_HOME $JAVA_HOME

ENV HOME=$HOME \
    JAVA_HOME=$JAVA_HOME \
    PATH="${JAVA_HOME}/bin:${PATH}"

# Copy build artifacts from base stage
COPY --from=base --parents \
    $HOME/examples/ \
    $HOME/server/ \
    $HOME/api/ \
    $HOME/target/ \
    $HOME/.cache/ \
    /

# Create a service user with read and execute permissions and write permissions of the ./etc directory
RUN <<EOF
apk add --no-cache bash
addgroup -S $USER
adduser -S -G $USER $USER
chmod -R 550 $HOME
mkdir -p $HOME/etc/
chmod -R 770 $HOME/etc/
chown -R $USER:$USER $HOME
EOF

USER $USER

# Copy remaining directories here for caching optimization
COPY --chown=$USER:$USER --parents bin/ etc/ $HOME/

WORKDIR $HOME

CMD ["./bin/start-uc-server"]