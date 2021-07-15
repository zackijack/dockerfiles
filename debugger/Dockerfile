FROM debian:buster-slim

LABEL maintainer="m.zackky@gmail.com"

ARG GRPCURL_VERSION=1.8.1
ARG GRPC_SHA256="6b6f2ca6536e944b9dfdfa7a50f5afd2f91e87b5606fd744b6a41f55acdfebbb"
ENV GRPCURL_VERSION=$GRPCURL_VERSION
ENV GRPC_SHA256=$GRPC_SHA256

# make Apt non-interactive
RUN echo 'APT::Get::Assume-Yes "true";' > /etc/apt/apt.conf.d/90debugger \
  && echo 'DPkg::Options "--force-confnew";' >> /etc/apt/apt.conf.d/90debugger

ENV DEBIAN_FRONTEND=noninteractive

# Make sure PATH includes ~/.local/bin
# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=839155
RUN echo 'PATH="$HOME/.local/bin:$PATH"' >> /etc/profile.d/user-local-path.sh

# man directory is missing in some base images
# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199
RUN apt-get update \
  && mkdir -p /usr/share/man/man1 \
  && apt-get install -y \
    apt \
    apt-utils \
    bash \
    build-essential \
    bzip2 \
    ca-certificates \
    curl \
    dnsutils \
    dumb-init \
    git \
    gnupg \
    gpg \
    gzip \
    httpie \
    inetutils-ping \	
    inetutils-telnet \
    inetutils-tools \
    inetutils-traceroute \
    influxdb-client \
    locales \
    mercurial \
    mariadb-client \
    net-tools \
    netcat \
    openssh-client \
    parallel \
    postgresql-client \
    redis-tools \
    sudo \
    tar \
    unzip \
    wget \
    xvfb \
    zip

# Install gRPCurl
RUN curl -L -o grpcurl.tar.gz https://github.com/fullstorydev/grpcurl/releases/download/v${GRPCURL_VERSION}/grpcurl_${GRPCURL_VERSION}_linux_x86_64.tar.gz \
  && echo "$GRPC_SHA256 grpcurl.tar.gz" | sha256sum -c - \
  && mkdir grpcurl \
  && tar -xzf grpcurl.tar.gz -C grpcurl \
  && mv grpcurl/grpcurl /usr/local/bin/grpcurl \
  && rm -rf grpcurl*

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

CMD ["/bin/bash"]
