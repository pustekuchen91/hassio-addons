ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base:7.2.0
###############################################################################
# Get prebuild containers from Vaultwarden
###############################################################################
FROM "vaultwarden/server:1.30.1" as vaultwarden

###############################################################################
# Build the actual add-on.
###############################################################################
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Get the Bitwarden from official images
COPY --from=vaultwarden /vaultwarden /opt/vaultwarden
COPY --from=vaultwarden /web-vault /opt/web-vault

# add Nginx
# hadolint ignore=DL3009
RUN \
    apt-get update \
    \
    && apt-get install -y --no-install-recommends \
        libmariadb-dev-compat=1:10.11.4-1~deb12u1 \
        libpq5=15.5-0+deb12u1 \
        sqlite3=3.40.1-2 \
        fail2ban=1.0.2-2 \
        iproute2=6.1.0-3 \
    && apt-get clean \
    && rm /etc/fail2ban/jail.d/defaults-debian.conf \
    && rm /etc/fail2ban/fail2ban.conf

# Copy root filesystem
COPY rootfs /

#!/bin/bash

RUN chmod a+rwx /etc/s6-overlay/s6-rc.d/fail2ban/run

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="StrausFuenf <admin@strausfuenf.de>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="StrausFuenf's Home Assistant Add-ons" \
    org.opencontainers.image.authors="StrausFuenf <admin@strausfuenf.de>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/StrausFuenf/hassio-addons" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
