# IoT Sandbox

This repository provides a container-based setup for Home Assistant, Mosquitto, and ESPHome using Docker Compose.

## Services

- **Home Assistant**: A platform for home automation.
- **Mosquitto**: An open-source MQTT broker.
- **ESPHome**: A system to control ESP8266/ESP32 by simple yet powerful configuration files.

## Prerequisites

- Docker
- Docker Compose

## Getting Started

1. Clone the repository:
    ```sh
    git clone https://github.com/arvemoen/iot-sandbox.git
    cd iot-sandbox
    ```

2. Start the containers:
    ```sh
    docker-compose up -d
    ```

3. Access the services:
    - Home Assistant: `http://localhost:8123`
    - ESPHome: `http://localhost:6052`
    - Mosquitto (MQTT) at port: `1883`

## Configuration

### Home Assistant

Configuration files for Home Assistant are located in `./sandbox/homeassistant/config`.

- `configuration.yaml`: Main configuration file for Home Assistant.
- `secrets.yaml`: Store sensitive information like passwords.
- `automations.yaml`: Define automation rules.
- `scripts.yaml`: Define custom scripts.

### Mosquitto

Configuration files for Mosquitto are located in `./sandbox/mosquitto/config`.

- `mosquitto.conf`:
    ```plaintext
    persistence true
    persistence_location /mosquitto/data/
    log_dest file /mosquitto/log/mosquitto.log
    listener 1883

    # Use one of these:
    allow_anonymous true
    # password_file /mosquitto/config/.passwd

    # For using passwords, bash into the container and run the mosquitto_passwd utility.
    # See https://mosquitto.org/man/mosquitto_passwd-1.html for more info.
    ```

### ESPHome

Configuration files for ESPHome are located in `./sandbox/esphome/config`.

- `esphome.yaml`: Main configuration file for ESPHome.
- `devices/`: Directory to store individual device configurations.

## Volumes

- Home Assistant: `./sandbox/homeassistant/config:/config`
- Mosquitto:
    - `./sandbox/mosquitto/config:/mosquitto/config`
    - `./sandbox/mosquitto/log:/mosquitto/log`
    - `./sandbox/mosquitto/data/:/mosquitto/data`
- ESPHome: `./sandbox/esphome/config:/config`

## Network

All services are connected to the `iot-net-sandbox` network.

## Timezone

The timezone is set to `Europe/Oslo` for all services.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.