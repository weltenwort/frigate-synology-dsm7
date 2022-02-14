FROM blakeblackshear/frigate:0.10.0-beta12-amd64 AS build
ARG DEBIAN_FRONTEND=noninteractive
ADD deb-src.list /etc/apt/sources.list.d/
RUN apt-get update \
  && apt-get install -y \
    dpkg-dev
RUN mkdir -p /root/libusb \
  && cd /root/libusb \
  && apt-get source libusb-1.0-0 \
  && apt-get build-dep -y libusb-1.0-0
ADD debian-rules-disable-udev.patch /root/
RUN cd /root/libusb/libusb-1.0-1.0.23 \
  && patch debian/rules < /root/debian-rules-disable-udev.patch \
  && DEB_BUILD_OPTIONS="nocheck nodocs" dpkg-buildpackage -rfakeroot -b

FROM blakeblackshear/frigate:0.10.0-beta12-amd64
ARG DEBIAN_FRONTEND=noninteractive
COPY --from=build /root/libusb/libusb-1.0-0_1.0.23-2build1_amd64.deb /root/
RUN dpkg -i /root/libusb-1.0-0_1.0.23-2build1_amd64.deb
