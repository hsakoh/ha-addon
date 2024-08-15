# CHANGELOG
## v1.0.21 - 2024-08-15
- Improvements to Keypad and Keypad Touch
    - Added a screen for viewing, adding, and deleting passcodes on the Ingress page.
    - Changed the method of specifying the Key ID in the DeleteKey command from Mqtt.Number to Mqtt.Select.
        - To apply the input format change, you need to delete the corresponding command device in the MQTT integration and restart the addon (or service).
    - For more details, please refer to [discussion #35](https://github.com/hsakoh/switchbot-mqtt/discussions/35).

## v1.0.20 - 2024-08-10
- Updated the add-on runtime to .NET 8 LTS.
- Changed the base image of the add-on from [Docker Hub](https://hub.docker.com/r/homeassistant/amd64-base/tags) to [GitHub Container Registry](https://github.com/home-assistant/docker-base/pkgs/container/amd64-base).
- Made minor improvements to log output.

## v1.0.19 - 2024-07-19
- **Important Security Update**
    - Fixed an issue where the Ingress page was publicly accessible when using Ngrok to receive Webhooks.

## v1.0.18 - 2024-06-24
- Fixed the issue where changes in the following fields for specific devices were not received by the MQTT integration via Webhook.
    - powerState: PlugMiniJp, PlugMiniUs
    - power: CeilingLight, CeilingLightPro, StripLight, ColorBulb, BatteryCirculatorFan

## v1.0.17 - 2024-06-10
- Improvement of DeviceType determination in the payload of Webhook when EnforceDeviceTypes is specified.

## v1.0.16 - 2024-06-09
- The field definitions for Keypad, Keypad Touch, and Ceiling Light Pro have been updated.
    - If you are using any of these devices, please delete the MQTT device, then delete and reacquire the device on the Ingress page, and restart the add-on.
    - (You don't necessarily need to reacquire them; it's not a significant update in practical terms.)

## v1.0.15 - 2024-05-18
- Fixed the payload value error for the selfClean command of the Floor Cleaning Robot S10 according to the API specification.

## v1.0.14 - 2024-05-17

- Changed the implementation so that when retrieving the device list, if there are unknown device types, it logs the issue instead of throwing an exception and continues processing.
    - (I currently know that there is a device type called `Hub Mini2`. One possible solution is to specify `EnforceDeviceTypes` to force it to be recognized as a `Hub mini`.)
- Corrected errors in the CSV master data related to the display of some device names.

## v1.0.13 - 2024-05-17

- Due to an update in the API specifications, support for one device has been added:
    - Lock Pro

## v1.0.12 - 2024-05-17

- Due to an update in the API specifications, support for two devices has been added:
    - Water Leak Detector
    - Floor Cleaning Robot S10

## v1.0.11 - 2024-05-08

- Fixed the issue of not exposing the port to the outside when not using Ngrok.

## v1.0.10 - 2024-02-12

- Fixed an issue where the setting value for the addon configuration `Mqtt.AutoConfig` could not be read.

## v1.0.9 - 2024-02-03

- Due to an update in the API specifications, support for two devices has been added:
    - Battery Circulator Fan
    - Curtain3
        - With the release of the API specifications, there is a possibility that responses for the device type have been added.
        - If you are specifying EnforceDeviceTypes, introduced in v1.0.3, you may have the option to remove it (unconfirmed).

## v1.0.8 - 2024-01-08

- Two fixes regarding the handling of the 'Lock State' value in SwitchBot Lock:
    - Fixed an issue where, in the case of Webhooks, the binary sensor was not properly receiving the value because it was received in uppercase.
    - Fixed an issue in the binary sensor of the device type 'Lock' where the ON and OFF states were reversed.

## v1.0.7 - 2024-01-01

- Support for Curtain pause comamnd.
    - To add a command to an existing device, delete the device once in `Device Configuration` and re-fetch it.
- Added example of default settings for EnforceDeviceTypes.


## v1.0.6 - 2023-09-28

- Support for KeyPad DeleteKey.

## v1.0.5 - 2023-09-28

- Support for non-required arguments in KeyPad CreateKey.

## v1.0.4 - 2023-09-27

- Added error log output for initial configuration.

## v1.0.3 - 2023-09-10

- Handling Cases Where Device Type Is Not Included in API Responses.
    - Added an option to forcibly specify the device type for each device ID.

## v1.0.2 - 2023-09-02

- Fixed a bug in the test execution modal with command type of tag.
    - Wrong command (null) was sent when test execution was performed by entering command text without selecting the command once in the drop-down.


## v1.0.1 - 2023-08-18

- Changed the approach for setting initial values of command parameters from state topics to ValueTemplate,facilitating the templating of color bulb configurations.


## v1.0.0 - 2023-08-15

- initial release
