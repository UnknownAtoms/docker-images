FROM alpine:3.20

RUN apk add --no-cache curl tar ca-certificates \
  && curl -fsSL "https://github.com/bitnami-labs/sealed-secrets/releases/download/v${VERSION}/kubeseal-${VERSION}-linux-amd64.tar.gz" \
     -o /tmp/kubeseal.tgz \
  && tar -xzf /tmp/kubeseal.tgz -C /usr/local/bin kubeseal \
  && chmod +x /usr/local/bin/kubeseal \
  && rm -f /tmp/kubeseal.tgz

ENTRYPOINT ["kubeseal"]
