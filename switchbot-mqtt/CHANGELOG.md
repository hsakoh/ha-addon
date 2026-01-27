# CHANGELOG

## v1.0.57 - 2026-01-27
- Changed the .NET runtime to explicitly define the virtual memory range reserved(but not used) for the GC heap.
- This prevents the TOP command from showing an extremely large VIRT value.

## v1.0.56 - 2025-12-26
- Upgrade ASP.NET runtime from version 8 to 10.
- Changed to self-contained deployment.

## v1.0.55 - 2025-12-13
- Add newly documented devices
    - W1702107 RGBIC Neon Rope Light
    - W3800520 Standing Circulator Fan
    - W5600009 Keypad Vision Pro
    - W8002100 AI Hub
    - W8302100,W8302101 Candle Warmer Lamp
    - W8402000,W8402010,W8402020 AI Art Frame
    - W3101102 Pan/Tilt Cam Plus 2K
- Update existing devices with additional fields or commands
    - W7400000 Home Climate Panel
       - Added scale field
    - W8200000 Prensence Sensor
       - Added lightLevel field
    - W3800510 Battery Circulator Fan
       - Added closeDelay command
    - W3800511 Circulator Fan
       - Added closeDelay command
    - W4001100 Pan/Tilt Cam Plus 3K
       - Modified API Device Type String
       - Device now returns API Device Type
       - If you explicitly specified Pan/Tilt Cam Plus 5MP in EnforceDeviceTypes, please remove it
- Fixed issue where add-on image size became larger after v1.0.53

## v1.0.54 - 2025-11-28
- Added support for the undocumented Webhook payload field (`fanGear`) for Air Purifier VOC,Table VOC,PM2.5,Table PM2.5.
    - If you want to add fields to a device that is already registered, delete the device from the Ingress page and add it again.


## v1.0.53 - 2025-11-14
- Added default_entity_id to the MQTT device discovery payload because object_id has been deprecated.
    - This change suppresses deprecation warnings that have been appearing in versions Home Assistant Core 2025.10 and later. [#100](https://github.com/hsakoh/switchbot-mqtt/issues/100)

## v1.0.52 - 2025-11-11
- Support for the following undocumented device has been added:
    - W7400000 Climate Panel
    - W8200000 Presence Sensor

## v1.0.51 - 2025-11-02
- Changed the API device type for the Smart Radiator Thermostat.

## v1.0.50 - 2025-11-01
- Internal implementation improvements:
    - Changed the device master from CSV format to individual JSON format for each device.

## v1.0.49 - 2025-10-29
- Fixes for Robot Vacuum K11+:
    - Changed API device type from `Robot Vacuum Cleaner K11+` to `Robot Vacuum Cleaner K11 Plus`.
    - Corrected the definition error for payload_on/payload_off in the `enableCloudService` field (binary sensor).

## v1.0.48 - 2025-10-12
## v1.0.47 - 2025-10-12
- Lock, Lock Lite, Lock Pro, Lock Ultra
    - In the Lock series, when `latchBoltLocked` is received via the `lockState` (through API or Webhook), the binary sensor (Lock) state will now be treated as `unlocked`.
    - (Note: This specification update is not yet documented in the API specification.)

## v1.0.46 - 2025-09-21
- Fix ngrok tunnel creation issue.

## v1.0.45 - 2025-09-19
- Support for the following new documented device has been added:
    - W7830000 Smart Radiator Thermostat
    - W3003100 Robot Vacuum K11+
    - W7732300 Plug Mini (EU)
    - W1702109 RGBICWW Strip Light
    - W1702101 RGBICWW Floor Lamp
    - W1702108 RGBIC Neon Wire Rope Light

## v1.0.44 - 2025-07-24
- Reflecting the actual device check results for OutdoorMeter
    - Change the FieldSourceType of Battery from `Status` to `Both`.
        - If you are using any of these devices, please delete the MQTT device, then delete and reacquire the device on the Ingress page, and restart the add-on.
        - (You don't necessarily need to reacquire them; it's not a significant update in practical terms.)

## v1.0.43 - 2025-07-09
- Followed updates to the API specification
    - Changed the unit of electricCurrent for PlugMini (US/JP) from amperes to milliamperes

## v1.0.42 - 2025-06-25
- Garage Door Opener
    - Fixed a an issue where the `doorStatus` status being inverted.

## v1.0.41 - 2025-06-24
- Lock, Lock Pro, Lock Ultra
    - Support for the new deadbolt command has been added.
    - If you are already using one of these devices, the new command will be added by removing the device from the Ingress page, re-fetching it, and saving the updated configuration.

## v1.0.40 - 2025-05-31
- Relay Switch 2PM
    - Added fields and commands for use in roller shade mode.
    - If you want to add fields to a device that is already registered, delete the device from the Ingress page and add it again.

## v1.0.39 - 2025-05-20
- Reflecting the actual device check results for Hub 3
    - Change the field name of `online` to `onlineStatus`.

## v1.0.38 - 2025-05-01
- Reflecting the actual device check results for RGBWW Strip Light 3:
    - ApiDeviceType `LED Strip Light3` -> `Strip Light3`
    - Get device status `online` field missing (delete)
- Reflecting the actual device check results for Relay Switch 1,1PM,2PM:
    - Change the data type of the `voltage` and `power` fields for each device from integer to float.
    - Add the `hubDeviceId` field for each device.
    - Add `voltage`, `power`, `usedElectricity`, and `electricCurrent` for Relay Switch 1 (always 0).
    - Adjust the case sensitivity of the status fields for Relay Switch 2PM to match the actual API specifications, e.g., `switch1usedElectricity` to `switch1UsedElectricity`.
    - Add arguments to the `turnOff` command for Relay Switch 2PM.
    - Change the argument transmission method for the `setMode` command of Relay Switch 2PM from comma-separated to semicolon-separated.
    - Remove the `setPosition` command for Relay Switch 2PM.

## v1.0.37 - 2025-04-28
- Support for the following new documented device has been added:
    - W7202100 Hub 3
    - W5110000 Smart Lock Lite
    - W5600000 Smart Lock Ultra
    - W5600003 Keypad Vision
    - W5502320 Relay Switch 2PM
    - W5502330 Garage Door Opener
    - W1702110 RGBWW Strip Light 3
    - W1702100 RGBWW Floor Lamp
    - W6602310 Floor Cleaning Robot S20
    - W3002520 Multitasking Household Robot K20+ Pro
    - W6702000 Video Doorbell

## v1.0.36 - 2025-04-21
- Fixed problem with Blind Tilt's setPosition command not working.

## v1.0.35 - 2025-04-09
## v1.0.34 - 2025-04-09
- Fixed an issue where the setMode command for Air Purifier VOC,Table VOC,PM2.5,Table PM2.5 was not functioning properly.

## v1.0.33 - 2025-01-30
- Fixed an issue where the setPosition command for Roller Shade was not functioning properly.

## v1.0.32 - 2025-01-24
- Remove Relay Switch 1 field `power`
  - Please either delete the MQTT devices and restart the add-on or manually delete the old MQTT sensors (fields).

- An option to persist device state has been added. (Disabled by default.)
  - When enabled, the last device state is persisted and continuously sent to the state topic.
  - This helps reduce the duration during which MQTT sensors are in an "unknown" state after restarting Home Assistant.
  - Specifically, it reduces the occurrence of warning logs in the MQTT integration in scenarios such as when a webhook is not triggered after a restart. (This also applies when webhooks are received without polling.)
  - The downside is that persisting the state involves writing to the file system each time a state notification is made.

## v1.0.31 - 2024-12-16
- Made the base URL of the SwitchBot API configurable.

## v1.0.30 - 2024-12-06
- Made the MQTT message retain configurable.
- Updated dependent libraries.

## v1.0.29 - 2024-11-10
- Support for the following new documented device has been added:
    - W3002500 Robot Vacuum K10+ Pro Combo
    - W3902300 Evaporative Humidifier
    - W3902310 Evaporative Humidifier (Auto-refill)
    - W5302300 Air Purifier PM2.5
    - W5302310 Air Purifier Table PM2.5	
    - W5302300 Air Purifier VOC
    - W5302310 Air Purifier Table VOC
    - W5000000 Roller Shade
    - W5502310 Relay Switch 1PM
    - W5502300 Relay Switch 1

## v1.0.28 - 2024-10-29
- Support for the following undocumented device has been added:
    - W4900000 Meter Pro
    - W4900010 Meter Pro(CO2 Monitor)

## v1.0.27 - 2024-09-16
- Added log output related to MQTT connections.
- Support for the following undocumented device has been added:
    - W2500032 Wallet Finder Card
        - No functionality is available.
        - Since the device type is not included during device enumeration, Use EnforceDeviceType to clearly indicate `Wallet Finder Card`.

## v1.0.26 - 2024-09-08
- Fixed an issue where the timestamps for webhook and polling always displayed the same value.

## v1.0.25 - 2024-08-31
- Resolved the issue where the MQTT binary sensors for the following five devices were not displaying the correct values:
  - Curtain, Curtain3, BlindTilt: `moving`
  - MotionSensor, ContactSensor: `moveDetected`

- Added support for Webhook payloads for the following two devices:
  - Motion Sensor: `battery`
  - Contact Sensor: `battery`, `openState`, `brightness`, `doorMode`
  - When updating the add-on, the `uniqueId` for the above MQTT sensors (fields) will change. 
    - Please either delete the MQTT devices and restart the add-on or manually delete the old MQTT sensors (fields).

- Improved the field display when receiving Webhook data for the Robot Vacuum Cleaner S10.
  - Specifically, the MQTT sensor value template has been modified to prevent other fields from being marked as "Unknown" when only part of the status is received upon a state change.
  - As part of the above changes, the status topics, which were previously divided into three, have been consolidated into one:
    - Before:
      - `switchbot/{deviceId}/status/{fieldSourceType}`
      - `{fieldSourceType}`: status|webhook|both
    - After:
      - `switchbot/{deviceId}/status`
  - Additionally, the manual polling request topic has been updated:
    - Before:
      - `switchbot/{deviceId}/status/update`
    - After:
      - `switchbot/{deviceId}/polling`
  - These changes should not affect the average add-on user. However, this is a caution for those who were directly publishing/subscribing to MQTT topics.

## v1.0.24 - 2024-08-30
- Support for the undocumented webhook payload format of the Robot Vacuum Cleaner S10.
- Due to an update in the API specifications, support for two devices has been added:
    - Mini Robot Vacuum K10+
    - Mini Robot Vacuum K10+ Pro
    - If you were using EnforceDeviceType to run the K10+ as an S1, you can remove the EnforceDeviceType. (In that case, it is recommended to first delete the MQTT device, then change the settings, and restart the add-on.)
    - Additionally, for users using the K10+ Pro, I would appreciate your feedback on whether the device is correctly identified. (The API Specification is unclear whether the DeviceType is `K10+Pro` or `K10+ Pro`.)
- Add CirculatorFan hudDeviceId field.
    - If you are using this device, please delete the MQTT device, then delete and reacquire the device on the Ingress page, and restart the add-on.
    - (You don't necessarily need to reacquire them; it's not a significant update in practical terms.)

## v1.0.23 - 2024-08-28
- Support for the following four undocumented devices has been added:
    - W4600000 Universal Remote
        - The battery level and charging status can be checked.
    - W3800511 Circulator Fan Lite
        - Functions similarly to the Battery Circulator Fan.
    - W4001100 Pan/Tilt Cam Plus (5MP)
        - Functions similarly to the Pan/Tilt Cam. (Mainly receives motion detection Webhooks)
        - Since the device type is not included during device enumeration, Use EnforceDeviceType to clearly indicate `Pan/Tilt Cam Plus 5MP`.
    - W4102000 Outdoor Spotlight Cam 2K (3MP)
        - No functionality is available.
        - Since the device type is not included during device enumeration, Use EnforceDeviceType to clearly indicate `Outdoor Spotlight Cam 2K`.
   
## v1.0.22 - 2024-08-21
- Fixed an issue where the correct value was not sent when using a command with a single input parameter entered through a select box.
    - This issue occurred with the following commands.
        - RobotVacuumCleanerS1/PowLevel
        - RobotVacuumCleanerS1Plus/PowLevel
        - RobotVacuumCleanerS10/selfClean
        - Humidifier/setMode
        - BatteryCirculatorFan/setNightLightMode
        - BatteryCirculatorFan/setWindMode
- Add KeyPad/KeyPadTouch hubDeviceId field.
    - Fixed an issue where MqttCoreService would fail to start if the device was not deleted and reloaded after adding field definitions.
- Added implementation for data protection in middleware.
    - This reduces some warning and error log outputs that occur when the add-on is restarted.

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
