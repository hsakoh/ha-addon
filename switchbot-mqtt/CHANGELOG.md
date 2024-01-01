# CHANGELOG

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
