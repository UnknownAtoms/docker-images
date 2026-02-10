FROM debian:bookworm-slim

RUN apt-get update
RUN apt-get install -y --no-install-recommends ca-certificates curl jq tar
RUN rm -rf /var/lib/apt/lists/*

# https://github.com/bitnami-labs/sealed-secrets?tab=readme-ov-file#linux
# Récupérer la dernière version
RUN KUBESEAL_VERSION=$(curl -fsSL https://api.github.com/repos/bitnami-labs/sealed-secrets/tags \
    | jq -r '.[0].name' \
    | cut -c 2-) && \
    echo "$KUBESEAL_VERSION" > /tmp/KUBESEAL_VERSION

# Télécharger l’archive
RUN KUBESEAL_VERSION=$(cat /tmp/KUBESEAL_VERSION) && \
    curl -fL "https://github.com/bitnami-labs/sealed-secrets/releases/download/v${KUBESEAL_VERSION}/kubeseal-${KUBESEAL_VERSION}-linux-amd64.tar.gz" \
    -o "/tmp/kubeseal-${KUBESEAL_VERSION}.tar.gz"

# Extraire le binaire
RUN KUBESEAL_VERSION=$(cat /tmp/KUBESEAL_VERSION) && \
    tar -xvzf "/tmp/kubeseal-${KUBESEAL_VERSION}.tar.gz" -C /tmp kubeseal

# Installer le binaire
RUN install -m 755 /tmp/kubeseal /usr/local/bin/kubeseal

# Nettoyage
RUN rm -f /tmp/kubeseal /tmp/kubeseal-*.tar.gz /tmp/KUBESEAL_VERSION

ENTRYPOINT ["kubeseal"]
