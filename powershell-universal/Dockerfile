ARG BUILD_FROM=ironmansoftware/universal:1.4.2-ubunutu-18.04
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Copy root filesystem
COPY rootfs /

# Setup base
#RUN apk add --no-cache \
#    coreutils=8.32-r0 \
#    wget=1.20.3-r1

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="PowerShell Universal" \
    io.hass.description="PowerShell Universal add-on by Home Assistant Community Add-ons" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Avri Chen-Roth <Stam@addons.community>" \
    org.opencontainers.image.title="PowerShell Universal" \
    org.opencontainers.image.description="PowerShell Universal add-on by Home Assistant Community Add-ons" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Avri Chen-Roth <Stam@addons.community>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/hassio-addons/addon-example" \
    org.opencontainers.image.documentation="https://github.com/hassio-addons/addon-example/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}

#Environment Variables 
ENV Data__RepositoryPath /share/powershell-universal/Repository
ENV Data__ConnectionString /share/powershell-universal/database.db
ENV UniversalDashboard__AssetsFolder /share/powershell-universal/UniversalDashboard 
ENV Logging__Path /share/powershell-universal/logs/log.txt
ENTRYPOINT ["./home/Universal/Universal.Server"]
