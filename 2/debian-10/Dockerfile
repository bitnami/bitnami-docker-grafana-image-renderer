FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl fonts-freefont-ttf fonts-ipafont-gothic fonts-kacst fonts-thai-tlwg fonts-wqy-zenhei gnupg gzip libavahi-client3 libavahi-common3 libblkid1 libbsd0 libbz2-1.0 libc6 libcom-err2 libcups2 libdbus-1-3 libexpat1 libffi6 libgcc1 libgcrypt20 libglib2.0-0 libgmp10 libgnutls30 libgpg-error0 libgssapi-krb5-2 libhogweed4 libidn2-0 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 liblz4-1 liblzma5 libmount1 libncursesw6 libnettle6 libp11-kit0 libpcre3 libreadline7 libselinux1 libsqlite3-0 libssl1.1 libstdc++6 libsystemd0 libtasn1-6 libtinfo6 libunistring2 libuuid1 libx11-6 libx11-xcb1 libxau6 libxcb-dri3-0 libxcb1 libxdmcp6 libxext6 libxss1 libxtst6 procps tar wget zlib1g
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/python-3.8.11-0-linux-amd64-debian-10.tar.gz && \
    echo "28b91ef5db9ad93e704881400703e4085bd82f016be15e3cf8760df044da9490  /tmp/bitnami/pkg/cache/python-3.8.11-0-linux-amd64-debian-10.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/python-3.8.11-0-linux-amd64-debian-10.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/python-3.8.11-0-linux-amd64-debian-10.tar.gz
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/node-14.17.3-2-linux-amd64-debian-10.tar.gz && \
    echo "c47c559cc4696938d59b58806bcd2c41a665646d89b7fe3c16a7674badc2cacd  /tmp/bitnami/pkg/cache/node-14.17.3-2-linux-amd64-debian-10.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/node-14.17.3-2-linux-amd64-debian-10.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/node-14.17.3-2-linux-amd64-debian-10.tar.gz
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/grafana-image-renderer-2.1.1-1-linux-amd64-debian-10.tar.gz && \
    echo "647bcd45bd8f55b3dbdb6b2f5037dae6e2e901f98d936e54ce15f9a7fd892384  /tmp/bitnami/pkg/cache/grafana-image-renderer-2.1.1-1-linux-amd64-debian-10.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/grafana-image-renderer-2.1.1-1-linux-amd64-debian-10.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/grafana-image-renderer-2.1.1-1-linux-amd64-debian-10.tar.gz
RUN chmod g+rwX /opt/bitnami
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' >> /etc/apt/sources.list.d/google.list && \
    install_packages google-chrome-unstable

ENV BITNAMI_APP_NAME="grafana-image-renderer" \
    BITNAMI_IMAGE_VERSION="2.1.1-debian-10-r51" \
    HTTP_HOST="0.0.0.0" \
    HTTP_PORT="8080" \
    PATH="/opt/bitnami/python/bin:/opt/bitnami/node/bin:$PATH"

EXPOSE 3000 8080

WORKDIR /opt/bitnami/grafana-image-renderer
USER 1001
ENTRYPOINT [ "node" ]
CMD [ "build/app.js", "server", "--config=conf/config.json" ]
