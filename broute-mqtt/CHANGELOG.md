# CHANGELOG

## v1.0.4 - 2024-08-10

- Updated the add-on runtime to .NET 8 LTS.
- Changed the base image of the add-on from [Docker Hub](https://hub.docker.com/r/homeassistant/amd64-base/tags) to [GitHub Container Registry](https://github.com/home-assistant/docker-base/pkgs/container/amd64-base).
- Made minor improvements to log output.

## v1.0.3 - 2024-06-08

- add retry logic for property value read.
- add timeout and retry count configuration options.

## v1.0.2 - 2024-01-12

- Fixed an issue where the setting value for the addon configuration `Mqtt.AutoConfig` could not be read.

## v1.0.1 - 2023-07-24

- add AutoConfig feature

## v1.0.0 - 2023-07-23

- initial release
