FROM rust:alpine3.18

# Install essential tools and dependencies
RUN apk add --no-cache \
    sudo \
    curl \
    tcpdump \
    netcat-openbsd \
    iptables \
    net-tools \
    iproute2 \
    bind-tools \
    tor \
    bash \
    && rm -rf /var/cache/apk/*

# Create a non-root user for development
RUN adduser -D vscode && \
    echo "devuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN mkdir -p /etc/tor
COPY torrc /etc/tor/torrc

WORKDIR /workspace

# Switch to non-root user
USER vscode

COPY . .

CMD [ "/bin/sh", "-c", "tor -f /etc/tor/torrc & sleep infinity" ]
