ARG BUILD_FROM=hassioaddons/debian-base:3.2.2
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION
ARG PACKAGE_URL=https://imsreleases.blob.core.windows.net/universal/production/${BUILD_VERSION}/Universal.linux-x64.${BUILD_VERSION}.zip
ARG DEBIAN_FRONTEND=noninteractive 

# Setup base
# Install dependencies and clean up
RUN apt-get update \
    && apt-get install --no-install-recommends -y \
    # less is required for help in powershell
        less=487-0.1+b1 \
    # requied to setup the locale
        locales=2.28-10 \
    # required for SSL
        ca-certificates=20200601~deb10u1 \
        gss-ntlmssp=0.7.0-4 \
    # PowerShell remoting over SSH dependencies
        openssh-client=1:7.9p1-10+deb10u2 \
        unzip=6.0-23+deb10u1 \
	# Download the PowerShell Deb and Install it
	#&& wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -o /tmp/packages-microsoft-prod.deb \
	&& curl -sSL https://packages.microsoft.com/config/debian/10/packages-microsoft-prod.deb  -o /tmp/packages-microsoft-prod.deb \
	&& apt-get install -y /tmp/packages-microsoft-prod.deb \
	&& apt-get update \ 
	#&& add-apt-repository -y universe \ 
	&& apt-get install -y powershell \ 
    # Download the Linux package and save it
    && echo ${PACKAGE_URL} \
    && curl -sSL ${PACKAGE_URL} -o /tmp/universal.zip \
    && unzip /tmp/universal.zip -d ./home/Universal || : \
    # remove powershell package
    && rm /tmp/universal.zip \
    && chmod +x ./home/Universal/Universal.Server



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
ENV POWERSHELL_TELEMETRY_OPTOUT 1

#EXPOSE 5000
#ENTRYPOINT ["./home/Universal/Universal.Server"]