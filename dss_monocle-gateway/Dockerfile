ARG BUILD_FROM=ghcr.io/hassio-addons/base:12.2.6
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# ---------------------------------------
# Create Monocle Gateway configuration 
# directory
# ---------------------------------------
RUN mkdir -p /tmp/monocle
RUN mkdir -p /etc/monocle

# Setup base system
#ARG BUILD_ARCH=amd64
# hadolint ignore=SC2181

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# ---------------------------------------
# Install Monocle Gateway dependencies
# and other useful utilties
# ---------------------------------------
RUN apk update
RUN apk add --no-cache wget
RUN apk add --no-cache curl
RUN apk add --no-cache libstdc++
RUN apk add --no-cache nano
RUN apk add --no-cache net-tools
RUN apk add --no-cache openssl
RUN apk add --no-cache ca-certificates

# ---------------------------------------
# Download versioned Monocle Gateway
# build archive file
# - - - - - - - - - - - - - - - - - - - -
# Extract Moncole Gateway related 
# executables to the appropriate 
# runtime directories 
# - - - - - - - - - - - - - - - - - - - -
# Remove the downloaded Monocle Gateway 
# archive files
# ---------------------------------------

RUN wget -c https://archive.monoclecam.com/monocle-gateway/monocle-gateway-0.0.6-beta/linux/monocle-gateway-alpine-x64-v0.0.6.tar.gz -O /tmp/monocle/monocle-gateway.tar.gz && \
# RUN wget -c https://files.monoclecam.com/monocle-gateway/linux/monocle-gateway-alpine-x64-v0.0.4.tar.gz -O /tmp/monocle/monocle-gateway.tar.gz && \
    cd /usr/local/bin/ && \
    tar xvzf /tmp/monocle/monocle-gateway.tar.gz monocle-gateway && \ 
    tar xvzf /tmp/monocle/monocle-gateway.tar.gz monocle-proxy  && \
    rm -Rf /tmp/monocle/

# ---------------------------------------
# Expose required TCP ports 
# (port 443 is required by Amazon for 
# secure connectivity)
# ---------------------------------------
EXPOSE 443/tcp

# ---------------------------------------
# Expose required UDP ports 
# (used for the @proxy method to allow 
# IP cameras to transmit streams via UDP)
# ---------------------------------------
# EXPOSE 62000-62100/udp
EXPOSE map[62000/udp:{} 62001/udp:{} 62002/udp:{} 62003/udp:{} 62004/udp:{} 62005/udp:{} 62006/udp:{} 62007/udp:{} 62008/udp:{} 62009/udp:{} 62010/udp:{} 62011/udp:{} 62012/udp:{} 62013/udp:{} 62014/udp:{} 62015/udp:{} 62016/udp:{} 62017/udp:{} 62018/udp:{} 62019/udp:{} 62020/udp:{} 62021/udp:{} 62022/udp:{} 62023/udp:{} 62024/udp:{} 62025/udp:{} 62026/udp:{} 62027/udp:{} 62028/udp:{} 62029/udp:{} 62030/udp:{} 62031/udp:{} 62032/udp:{} 62033/udp:{} 62034/udp:{} 62035/udp:{} 62036/udp:{} 62037/udp:{} 62038/udp:{} 62039/udp:{} 62040/udp:{} 62041/udp:{} 62042/udp:{} 62043/udp:{} 62044/udp:{} 62045/udp:{} 62046/udp:{} 62047/udp:{} 62048/udp:{} 62049/udp:{} 62050/udp:{} 62051/udp:{} 62052/udp:{} 62053/udp:{} 62054/udp:{} 62055/udp:{} 62056/udp:{} 62057/udp:{} 62058/udp:{} 62059/udp:{} 62060/udp:{} 62061/udp:{} 62062/udp:{} 62063/udp:{} 62064/udp:{} 62065/udp:{} 62066/udp:{} 62067/udp:{} 62068/udp:{} 62069/udp:{} 62070/udp:{} 62071/udp:{} 62072/udp:{} 62073/udp:{} 62074/udp:{} 62075/udp:{} 62076/udp:{} 62077/udp:{} 62078/udp:{} 62079/udp:{} 62080/udp:{} 62081/udp:{} 62082/udp:{} 62083/udp:{} 62084/udp:{} 62085/udp:{} 62086/udp:{} 62087/udp:{} 62088/udp:{} 62089/udp:{} 62090/udp:{} 62091/udp:{} 62092/udp:{} 62093/udp:{} 62094/udp:{} 62095/udp:{} 62096/udp:{} 62097/udp:{} 62098/udp:{} 62099/udp:{} 62100/udp:{}]
# Copy data for add-on
COPY run.sh /
RUN chmod a+x /run.sh

CMD ["/run.sh"]

# Labels
LABEL \
    io.hass.name="DSS Monocle Gateway" \
    io.hass.description="DSS Monocle Gateway Add-On" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="https://github.com/sdesalve" \
    org.opencontainers.image.title="Addon Monocle Gateway for ${BUILD_ARCH}" \
    org.opencontainers.image.description="Monocle Gateway for Home Assistant" \
    org.opencontainers.image.vendor="SDeSalve.it" \
    org.opencontainers.image.authors="SDeSalve <me@sdesalve.it>" \
    org.opencontainers.image.licenses="CC Attribution-NonCommercial 4.0 International" \
    org.opencontainers.image.url="https://sdesalve.it" \
    org.opencontainers.image.source="https://github.com/sdesalve/hassio-addons/tree/master/dss_monocle-gateway" \
    org.opencontainers.image.documentation="https://github.com/sdesalve/hassio-addons/tree/master/dss_monocle-gateway/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}    
