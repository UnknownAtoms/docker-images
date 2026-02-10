FROM alpine:3.20

ARG VERSION

RUN set -eux; \
    V="${VERSION#v}"; \
    test -n "$V"; \
    apk add --no-cache curl tar ca-certificates; \
    URL="https://github.com/bitnami-labs/sealed-secrets/releases/download/v${V}/kubeseal-${V}-linux-amd64.tar.gz"; \
    echo "Downloading $URL"; \
    curl -fL "$URL" -o /tmp/kubeseal.tgz; \
    tar -xzf /tmp/kubeseal.tgz -C /usr/local/bin kubeseal; \
    chmod +x /usr/local/bin/kubeseal; \
    rm -f /tmp/kubeseal.tgz; \
    kubeseal --version

ENTRYPOINT ["kubeseal"]
