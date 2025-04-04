# Signal Desktop app - Docker image
#### _This is a fork of the original repo by [chrisbench](https://github.com/chrisbensch/docker-signal), in order to update the base image and mantain an up-to-date Signal version_

Docker image for the Signal messaging desktop app, using the [jlesage/docker-baseimage-gui](https://github.com/jlesage/docker-baseimage-gui) image.
Once deployed, the app can be accessed through a modern web browser or a VNC client.
This image is only available for **linux/amd64**.

**This image is experimental and might have undesirable effects. Use it under your responsability!**

_This image is not official and is not associated with the Signal Foundation._

## Getting started
You can get this image up and running by downloading or copying the [docker-compose.yml](docker-compose.yml) file. Make sure to adjust the volumes and port if needed.
```bash
wget https://github.com/myanesp/docker-signal/raw/refs/heads/develop/docker-compose.yml
docker compose up -d
```

Or by using docker run, if you wish:
```bash
docker run -d --name=signal-desktop -p 5800:5800 -v $PWD/config:/config -v /etc/localtime:/etc/localtime:ro ghcr.io/myanesp/signal-desktop
```

## Configuration

- Volumes:
  - All the configuration is persisted in `/config`
- Environment variables:
  - Please refer to the [base image documentation for a list of all the available environment variables](https://github.com/jlesage/docker-baseimage-gui#environment-variables) that can be configured.
  - Some of the most important may be:
    - `VNC_PASSWORD`: password for the VNC and noVNC (web) access (default: no password!)
    - `DISPLAY_WIDTH` and `DISPLAY_HEIGHT`: customize the size of the app window (default: 1280x720)
    - `TZ`: timezone for the container, used for displaying dates on the app (default: UTC). Can be one of the available [here](http://en.wikipedia.org/wiki/List_of_tz_database_time_zones) ("TZ database name" column). Can be synchronized with the host by bind-mounting the `/etc/localtime` path (read-only).
- Ports:
  - 5800: noVNC (web) where the app is displayed
  - 5900: pure VNC server that can be accessed with any VNC client app

## Changelog

- 0.1.0 - First release
  - Signal Desktop v7.48.0
