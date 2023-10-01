# Zigbee to MQTT Bridge Setup

This project provides a simple and hassle-free setup for Zigbee2MQTT using Docker Compose. By leveraging Docker Compose, setting up Zigbee2MQTT becomes a straightforward process, allowing you to focus more on utilizing your Zigbee devices rather than worrying about the setup.

## Project Structure

- `data/` : Directory to store Zigbee2MQTT data.
- `mosquitto/` : Directory containing Mosquitto configuration, data, and logs.
- `docker-compose.yml` : Docker Compose file to orchestrate the containers.

## Prerequisites

- Docker and Docker Compose installed on your machine.
- A Zigbee adapter (e.g., Texas Instruments CC2531) connected to your machine.

## Setup

1. **Clone this repository to your machine.**
   
   ```bash
   git clone https://github.com/sammrai/zigbee2mqtt-docker.git
   ```
   

2. **Navigate to the project directory.**

   ```bash
   cd zigbee2mqtt-docker
   ```


3. **List USB Devices**:
   Before inserting your USB receiver, list all connected USB devices using the following command:

   ```bash
   lsusb
   ```

   This will give you a list of currently connected USB devices.

4. **Insert your USB receiver which has chip CC2652**:
   Now insert your USB receiver and run the `lsusb` command again. Look for the new device in the output, that's your Zigbee adapter.

5. **Check Device Path**:
   Your Zigbee adapter will be assigned a device path, which is needed for the configuration. First, identify the more stable device path by listing the serial devices by their ID:

   ```bash
   ls /dev/serial/by-id/
   ```

   This should give you an output like `/dev/serial/by-id/usb-1a86_USB_Serial-if00-port0:/dev/ttyACM0`. Note down this ID.

6. **Zigbee2MQTT Configuration**:
   Update the `docker-compose.yml` file with the correct device path for your Zigbee adapter.

   ```yaml
   devices:
     - usb-1a86_USB_Serial-if00-port0:/dev/ttyACM0
   ```

   Replace the left-hand side of the colon with your Zigbee adapter's device path as noted down earlier.

7. **(Optional) Timezone Configuration**:
   Update the `docker-compose.yml` file to set your timezone in the environment section:

   ```yaml
   environment:
     - TZ=Asia/Tokyo
   ```

   Replace `Asia/Tokyo` with your timezone.

8. **Modify the `docker-compose.yml` file to match your environment, if necessary.**

9. **Run the following command to start the services**:

   ```bash
   docker-compose up -d
   ```

## Usage

Once the services are up and running, you can access the Zigbee2MQTT frontend at `http://localhost:8080`.

To stop the services, run:

```bash
docker-compose down
```
