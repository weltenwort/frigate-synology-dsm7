# frigate-synology-dsm7
This provides a `Dockerfile` (with context) as well as a `docker-compose.yml` file to build a [frigate](https://github.com/blakeblackshear/frigate) docker image that supports using a Google Coral USB TPU. It is based on the official upstream frigate image but recompiles `libusb1` without `udev` support.

## Usage on the NAS with `docker-compose`

1. SSH into the NAS.

2. Clone this repository:

   ```sh
   git clone https://github.com/weltenwort/frigate-synology-dsm7.git
   ```

3. Create environment file `secrets.env` to inject secrets:

   ```sh
   cat <<EOF >secrets.env
   FRIGATE_TITANIA_MQTT_USERNAME=my-frigate-mqtt-username
   FRIGATE_TITANIA_MQTT_PASSWORD=my-frigate-mqtt-password
   FRIGATE_CAMERA_1_RTSP_CREDENTIALS=my-camera-1-username:my-camera-1-password
   FRIGATE_CAMERA_2_RTSP_CREDENTIALS=my-camera-2-username:my-camera-2-password
   EOF
   ```

4. Configure frigate with a config file using the env variables above.

5. Start the container:

   ```sh
   docker-compose up --detach --force-create
   ```
