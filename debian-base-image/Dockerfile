FROM debian:buster-slim

LABEL maintainer="zackky@kitabisa.com"

ENV TZ=Asia/Jakarta

RUN apt-get update \
    && apt-get install -y \
        bash \
        ca-certificates \
        dumb-init \
        openssl \
        tzdata

RUN cp /usr/share/zoneinfo/$TZ /etc/localtime && \
	echo $TZ > /etc/timezone