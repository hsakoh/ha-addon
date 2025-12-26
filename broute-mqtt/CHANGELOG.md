# CHANGELOG

## v1.0.10 - 2025-12-26
- Upgrade .NET runtime from version 8 to 10.
- Changed to self-contained deployment.

## v1.0.9 - 2025-12-04
- Added default_entity_id to the MQTT device discovery payload because object_id has been deprecated.
    - This change suppresses deprecation warnings that have been appearing in versions Home Assistant Core 2025.10 and later. 

## v1.0.8 - 2025-03-08
- change instantaneous_electric_power device class(APPARENT_POWER->POWER)

## v1.0.7 - 2025-03-03
## v1.0.6 - 2025-03-03

- [Experimental] add BP35C0 support

## v1.0.5 - 2025-02-25

- Updated the add-on runtime to .NET 9.

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
