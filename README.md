# Obico ML API Image

## :information_source: Information
A prebuilt Docker image for the `ml_api` service from [TheSpaghettiDetective/obico-server](https://github.com/TheSpaghettiDetective/obico-server).

It provides Obico's machine-learning API for AI failure detection and can be used with [Bambuddy](https://github.com/maziggy/bambuddy). The image is published as `ghcr.io/buanet/obico-ml-api`.

For details see [official Bambuddy docs](https://wiki.bambuddy.cool/features/failure-detection/). 

## :desktop_computer: Supported platforms

The image is currently built for `linux/amd64`. It is not published as a multi-platform image.

## :rocket: Usage

```
services:
  ml-api:
    image: ghcr.io/buanet/obico-ml-api:latest
    container_name: ml-api
    restart: unless-stopped
    ports:
      - "3333:3333"
    command: >
      bash -c "gunicorn --bind 0.0.0.0:3333 --workers 1 wsgi"
    environment:
      FLASK_APP: server.py
      DEBUG: "False"
    healthcheck:
      test: ["CMD-SHELL", "wget --no-verbose --tries=1 --spider http://127.0.0.1:3333/hc/"]
      interval: 30s
      timeout: 10s
      retries: 3
```

## :copyright: License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.