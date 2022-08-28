ARG LIBUSB_PKG_VERSION=1.0.24
ARG LIBUSB_PKG_BUILD=3

FROM blakeblackshear/frigate:0.11.0-rc2 AS build
ARG DEBIAN_FRONTEND=noninteractive
ARG LIBUSB_PKG_VERSION
ADD deb-src.list /etc/apt/sources.list.d/
RUN apt-get update \
  && apt-get install -y \
    dpkg-dev
RUN mkdir -p /root/libusb \
  && cd /root/libusb \
  && apt-get source libusb-1.0-0 \
  && apt-get build-dep -y libusb-1.0-0
ADD debian-rules-disable-udev.patch /root/
RUN cd "/root/libusb/libusb-1.0-${LIBUSB_PKG_VERSION}" \
  && patch debian/rules < /root/debian-rules-disable-udev.patch \
  && DEB_BUILD_OPTIONS="nocheck nodocs" dpkg-buildpackage -rfakeroot -b

FROM blakeblackshear/frigate:0.11.0-rc2
ARG DEBIAN_FRONTEND=noninteractive
ARG LIBUSB_PKG_VERSION
ARG LIBUSB_PKG_BUILD
ARG TARGETARCH
COPY --from=build "/root/libusb/libusb-1.0-0_${LIBUSB_PKG_VERSION}-${LIBUSB_PKG_BUILD}_${TARGETARCH}.deb" /root/
RUN dpkg -i "/root/libusb-1.0-0_${LIBUSB_PKG_VERSION}-${LIBUSB_PKG_BUILD}_${TARGETARCH}.deb"
