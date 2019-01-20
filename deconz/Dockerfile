ARG BUILD_FROM=hassioaddons/debian-base-armhf
FROM ${BUILD_FROM}

# Setup base system
RUN apt-get update \
    && apt-get -y --no-install-recommends install xauth wget libqt5core5a libqt5network5 libqt5widgets5 libqt5gui5 libqt5serialport5 libqt5websockets5 libqt5sql5 libcap2-bin sqlite3 xpra \
    && cd /tmp \
    && wget -O deconz.deb https://www.dresden-elektronik.de/rpi/deconz/beta/deconz-2.05.55-qt5.deb \
    && dpkg --ignore-depends wiringpi -i /tmp/deconz.deb \
    && rm -rf /tmp/* /var/lib/apt/lists/* \
    && ln -s /config/deconz/local /root/.local \
    && ln -s /config/deconz/otau /root/otau \
    && setcap -r /usr/bin/deCONZ
# deconz will not start in docker with capabilities

# Copy root filesystem
COPY rootfs /

# Build arugments
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="deconz" \
    io.hass.description="deconz" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="David Kreitschmann <d+hass@o7o.de>" \
    org.label-schema.description="deCONZ for RaspBee and ConBee Zigbee Adapters" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="deconz" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.vcs-ref=${BUILD_REF} \
