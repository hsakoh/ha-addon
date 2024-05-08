# CHANGELOG

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
