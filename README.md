# frigate-synology-dsm7
This provides a `Dockerfile` (with context) as well as a `docker-compose.yml` file to build a [frigate](https://github.com/blakeblackshear/frigate) docker image that supports using a Google Coral USB TPU. It is based on the official upstream frigate image but recompiles `libusb1` without `udev` support.

## Usage on the NAS with `docker-compose` but without `git`

1. SSH into the NAS.

2. Download the compose file:

   ```sh
   wget "https://github.com/weltenwort/frigate-synology-dsm7/raw/main/docker-compose.yml"
   ```

3. Create environment file `secrets.env` to inject secrets:

   ```sh
   cat <<EOF >secrets.env
   FRIGATE_MQTT_USERNAME=my-frigate-mqtt-username
   FRIGATE_MQTT_PASSWORD=my-frigate-mqtt-password
   FRIGATE_CAMERA_1_RTSP_CREDENTIALS=my-camera-1-username:my-camera-1-password
   FRIGATE_CAMERA_2_RTSP_CREDENTIALS=my-camera-2-username:my-camera-2-password
   EOF
   ```

4. Create the volume directories (adjust paths if you changed them in the compose file):

   ```sh
   mkdir -p /volume1/docker/volumes/frigate-0-config
   mkdir -p /volume1/docker/volumes/frigate-0-media
   ```

5. Edit the `docker-compose.yml` file and configure frigate with a config file at
   `/volume1/docker/volumes/frigate-0-config/config.yml` using the env
   variables. Adjust paths and env vars to match your choices above.

6. Start the container:

   ```sh
   sudo docker-compose up --detach --force-recreate
   ```

## Usage on the NAS with `docker-compose` and `git`

1. SSH into the NAS.

2. Clone this repository:

   ```sh
   git clone https://github.com/weltenwort/frigate-synology-dsm7.git
   ```

3. Create environment file `secrets.env` to inject secrets:

   ```sh
   cat <<EOF >secrets.env
   FRIGATE_MQTT_USERNAME=my-frigate-mqtt-username
   FRIGATE_MQTT_PASSWORD=my-frigate-mqtt-password
   FRIGATE_CAMERA_1_RTSP_CREDENTIALS=my-camera-1-username:my-camera-1-password
   FRIGATE_CAMERA_2_RTSP_CREDENTIALS=my-camera-2-username:my-camera-2-password
   EOF
   ```

4. Create the volume directories (adjust paths if you changed them in the compose file):

   ```sh
   mkdir -p /volume1/docker/volumes/frigate-0-config
   mkdir -p /volume1/docker/volumes/frigate-0-media
   ```

5. Edit the `docker-compose.yml` file and configure frigate with a config file at
   `/volume1/docker/volumes/frigate-0-config/config.yml` using the env
   variables. Adjust paths and env vars to match your choices above.

6. Start the container:

   ```sh
   sudo docker-compose up --detach --force-recreate
   ```
