# Preparation

This add-on sends SwitchBot device information to the Home Assistant's [MQTT integration](https://www.home-assistant.io/integrations/mqtt/), enabling operation.

1. Install MQTT Broker

    First, Install the MQTT broker.

    The recommended setup method is to use the [Mosquitto MQTT broker add-on](https://github.com/home-assistant/addons/blob/master/mosquitto/DOCS.md).

1. Configure MQTT Integration

    Follow the instructions on [this page](https://www.home-assistant.io/integrations/mqtt/#broker-configuration) to set up which broker the MQTT integration exchanges information with.

# Add-on Configuration

## MQTT Broker
* If you simply introduced the Mosquitto MQTT broker add-on, it works with the default values.

    This is because it can receive the information necessary for connection from the Supervisor API of Home Assistant OS.

    ```yaml
    Mqtt:
      AutoConfig: true
      Host: ""
      Port: 1883
      Id: ""
      Pw: ""
      Tls: false
    ```

* If you have introduced the Mosquitto MQTT broker add-on with a changed configuration, or if you are using another broker, enter the values.

    ```yaml
    Mqtt:
      AutoConfig: false
      Host: 192.168.0.100
      Port: 1883
      Id: mqtt-user
      Pw: mqtt-user-password
      Tls: false
    ```

|Setting Key |Default Value |Description|
|--|--|--|
|Mqtt:AutoConfig|`true`|For users of the default Home Assistant Mosquitto integration, connection details can be detected via the Home Assistant Supervisor API. Therefore, this value should be set to true|
|Mqtt:Host|-|MQTT Broker<br>Specify the hostname|
|Mqtt:Port|`1883`|Specify the port number.|
|Mqtt:Id|-|If authentication is required, specify the ID|
|Mqtt:Pw|-|If authentication is required, specify the PW.|
|Mqtt:Tls|`false`|If TLS connection is required, set to `true`.|

## SwitchBot API Key & Secret
* Obtain and configure the token and secret according to the [SwitchBotApi documentation](https://github.com/OpenWonderLabs/SwitchBotAPI?tab=readme-ov-file#getting-started).

    ```yaml
    SwitchBot:
      ApiBaseUrl: https://api.switch-bot.com/v1.1/
      ApiKey: >-
        aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
      ApiSecret: bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
    ```

|Setting Key |Default Value |Description|
|--|--|--|
|SwitchBot:ApiBaseUrl|`https://api.switch-bot.com/v1.1/`| API Base URL|
|SwitchBot:ApiKey|-|Obtain and configure the **open token** according to the [SwitchBotApi documentation](https://github.com/OpenWonderLabs/SwitchBotAPI?tab=readme-ov-file#getting-started).The token is **96 characters long**.|
|SwitchBot:ApiSecret|-|Obtain and configure the **secret key** according to the [SwitchBotApi documentation](https://github.com/OpenWonderLabs/SwitchBotAPI?tab=readme-ov-file#getting-started).The secret is **32 characters long**.|

## Webhook
* Disabled

    ```yaml
    WebhookService:
      TunnelMode: Disabled
    ```

* Via Ngrok (account required)
    1. [Sign up for an ngrok account.](https://dashboard.ngrok.com/)
    1. Copy your [ngrok authtoken](https://dashboard.ngrok.com/get-started/your-authtoken) from your ngrok dashboard.

    ```yaml
    WebhookService:
      TunnelMode: Ngrok
      NgrokAuthToken: _________________ngrokauthtoken__________________
    ```

* Via TryCloudflare / Quick Tunnel (no account needed)

    ```yaml
    WebhookService:
      TunnelMode: TryCloudflare
    ```

* Via Cloudflare Zero Trust tunnel (fixed URL, account required)
    1. Create a tunnel in the [Cloudflare Zero Trust dashboard](https://one.dash.cloudflare.com/networks/connectors) and obtain the tunnel token.
    1. In the dashboard, go to `Networks` > `Connectors` > `Create a tunnel`.
    1. Select `Cloudflared`.
    1. Enter any tunnel name you like, then record the `eyJ...` token included in the shown startup command.
    1. Configure the public hostname by choosing the subdomain and domain you want to use.
    1. In the service settings, set `Type` to `HTTP` and `URL` to `127.0.0.1:8098`, then complete the setup.

    ```yaml
    WebhookService:
      TunnelMode: CloudflareZeroTrust
      CloudflareTunnelToken: _________________cloudflaretunneltoken__________________
      HostUrl: https://your-fixed-domain.example.com
    ```

* Direct (Home Assistant OS directly receives)

    ```yaml
    WebhookService:
      TunnelMode: HostUrl
      HostUrl: http://<internet-reachable-hostname-of-homeassistant>:8098
    ```

|Setting Key |Default Value |Description|
|--|--|--|
|WebhookService:TunnelMode|`TryCloudflare`|Select webhook reception mode. One of: `Disabled`, `HostUrl`, `Ngrok`, `TryCloudflare`, `CloudflareZeroTrust`.|
|WebhookService:NgrokAuthToken|-|Required when TunnelMode is `Ngrok`. Set the Ngrok authentication token.|
|WebhookService:HostUrl|-|Required when TunnelMode is `HostUrl`. Also required for `CloudflareZeroTrust` (the fixed public URL configured in the Cloudflare dashboard).|
|WebhookService:CloudflareTunnelToken|-|Required when TunnelMode is `CloudflareZeroTrust`. Obtain from the Cloudflare Zero Trust dashboard.|

## Others
* AutoStartServices
    * After rebooting the Home Assistant OS or upgrading add-on version, the service will start automatically.
    * We recommend enabling this after configuring the device and confirming that it works without any problems.
* LogLevel
    * If trouble occurs, set the log level to Trace, check the log, and create an Issue on Github.
* EnforceDeviceTypes
    * There are rare cases where devices, such as new ones, do not include the device type in their API responses. In such cases, you can specify a device type to be forcibly recognized based on the device ID.

```yaml
EnforceDeviceTypes:
    - DeviceId: <K10+ DeviceId>
    DeviceType: Robot Vacuum Cleaner S1
    - DeviceId: <Hub Mini2 DeviceId>
    DeviceType: Hub Mini
MessageRetain: 
  Entity: true
  State: false
ImageFetch:
  MaxRetries: 25
  RetryIntervalMs: 1000
DeviceStatePersistence: false
AutoStartServices: true
ExitOnServiceFailure: false
LogLevel: Trace
```

|Setting Key |Default Value |Description|
|--|--|--|
|AutoStartServices|`false`|If various internal services should start automatically when add-on is started, set to true.|
|ExitOnServiceFailure|`false`|When enabled, the application exits if any internal service (MQTT, Polling, or Webhook) enters a failed state. This allows the Home Assistant Supervisor's watchdog to automatically restart the add-on and recover from transient failures.|
|DeviceStatePersistence|`false`|When enabled, the last device state is persisted and continuously sent to the state topic.<br>This helps reduce the duration during which MQTT sensors are in an "unknown" state after restarting Home Assistant.<br>Specifically, it reduces the occurrence of warning logs in the MQTT integration in scenarios such as when a webhook is not triggered after a restart. (This also applies when webhooks are received without polling.)<br>The downside is that persisting the state involves writing to the file system each time a state notification is made.|
|LogLevel|`Trace`|Set the log level. Specify one of the following values:<br>Trace, Debug, Information, Warning, Error, Critical, None|
|MessageRetain:Entity|`true`|To enable retention for MQTT configuration messages, set to true. <br>See [Using Retained Config Messages](https://www.home-assistant.io/integrations/mqtt/#using-retained-config-messages) for more details.  |
|MessageRetain:State|`false`|To enable retention for MQTT state messages, set to true. <br>See [Using Retained State Messages](https://www.home-assistant.io/integrations/mqtt/#using-retained-state-messages) for more details.  ||
|ImageFetch:MaxRetries|`25`|Maximum number of retry attempts when fetching a device image (e.g., camera snapshot) from a presigned URL returns a 404 response.|
|ImageFetch:RetryIntervalMs|`1000`|Interval in milliseconds between image fetch retry attempts.|
|EnforceDeviceTypes[]:DeviceId|-|There are rare cases where devices, such as new ones, do not include the device type in their responses. In such cases, you can specify a device type to be forcibly recognized based on the device ID.|
|EnforceDeviceTypes[]:DeviceType|-|Use the value found in the "ApiDeviceTypeString" field of [this JSON files](https://github.com/hsakoh/switchbot-mqtt/blob/main/src/SwitchBotMqttApp/MasterData/PhysicalDevice).|


## Differences in Webhook Reception Methods

This add-on supports the following five modes for webhook reception, configurable via `WebhookService:TunnelMode`.

### Disabled

Webhook reception is turned off. Only polling will be used for device state updates.

### HostUrl

Configure your environment so that add-on's port 8098 is reachable from the internet. Set `HostUrl` to the publicly accessible base URL (excluding `/webhook`).

Add-on listens at `http://<your home assistant private ip address>:8098/webhook` and registers that URL with SwitchBot Cloud on startup.

### Via Ngrok

When configured, add-on internally downloads and installs Ngrok, establishes a session via outbound connections, and enables webhook reception without opening an inbound port.

Before using Ngrok, read its terms of use, sign up, obtain an authentication token, and configure `NgrokAuthToken`.

### Via TryCloudflare / Quick Tunnel

Uses [Cloudflare TryCloudflare (Quick Tunnel)](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/do-more-with-tunnels/trycloudflare/) — no Cloudflare account or pre-configuration is needed. A random temporary `https://xxxxx.trycloudflare.com` URL is issued automatically at each startup.

Before using it, review Cloudflare's [terms, privacy policy, and related legal notice](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/do-more-with-tunnels/trycloudflare/#legal).

No inbound port needs to be opened. The URL changes every time the add-on restarts.

Powered by [CloudflaredKit](https://github.com/hsakoh/CloudflaredKit).

### Via Cloudflare Zero Trust Tunnel

Uses a permanent [Cloudflare Zero Trust tunnel](https://one.dash.cloudflare.com/) with a fixed URL configured in the Cloudflare dashboard.

1. In the Cloudflare Zero Trust dashboard, go to `Networks` > `Connectors` and select `Create a tunnel`.
2. Select `Cloudflared`.
3. Enter any tunnel name you like, then copy the `eyJ...` token included in the startup command.
4. Configure the public hostname by choosing the subdomain and domain you want to use.
5. In the service settings, set `Type` to `HTTP` and `URL` to `127.0.0.1:8098`, then complete the setup.
6. Set `CloudflareTunnelToken` to the obtained token.
7. Set `HostUrl` to the fixed public URL you configured in the Cloudflare dashboard (used to register with SwitchBot Cloud).

No inbound port needs to be opened, and the URL is stable across restarts.

Powered by [CloudflaredKit](https://github.com/hsakoh/CloudflaredKit).


# How to use add-on

## TL;DR

1. Open Web UI
1. Select "Device Configuration" tab.
    1. Click `Fetch Devices By SwitchBotApi`.
    1. Check all the checkboxes for the devices (Enable, Polling, Webhook).
    1. Click `Save Changes`.
1. Select `Service Management` tab.
    1. Start `MqttCoreService`, then continue to the next step.
    1. Start `PollingService`, then continue to the next step.
    1. Start `WebhookService`
1. Done.


## Device configuration

### Basic

This add-on supports ingress, allowing you to open the configuration page by clicking "Open Web UI" from add-on's page.

If running on a separate Docker instance, you can access the interface on port 8099.

Once you've opened the configuration page, select "Device Configuration" from the top menu. This takes you to the device settings page.

* Clicking the `Fetch Devices By SwitchBotApi` button lists the physical devices and virtual infrared remote devices registered with SwitchBot. See the [API specifications](https://github.com/OpenWonderLabs/SwitchBotAPI#get-device-list) for more details.

* Click `Save Changes` to persist the configuration.

* When you click 'Restore changes', the configuration values will revert to their original state before opening the page.

* Deleting a device on this screen will only make it invisible in the add-on. It will not be removed from the SwitchBot app and your account.
You can restore it by performing 'Fetch Devices By SwitchBotApi' again.
This functionality is intended to facilitate maintenance when commands or fields are added due to upgrades of the internal definition file.

![01_deivce_configuration](https://github.com/hsakoh/switchbot-mqtt/wiki/images/01_deivce_configuration.png)

### Physical Devices

The first table is for configuring physical devices.

* Enabling the checkbox will make the corresponding device detectable by the MQTT integration.

* Enabling the Polling checkbox will notify the device's status at specified intervals (in ISO8601 Duration format).
  * Since a button for manually retrieving the device status is sent to the MQTT integration, you can use it without automatic retrieval.
  * At the bottom of the table, you will find the expected number of API calls based on the current settings. Please consider this as a reference.
  * Currently, the limit is 10,000 API calls per day. Aim for a value well below this threshold. Keep in mind that command operations also result in one API call per action, so set the frequency accordingly.
* Enabling the Webhook checkbox will analyze the content upon receiving a webhook and subsequently notify the device's status.

* In the Description field, you can override the device name detected on Home Assistant from DeviceName.

#### Field and Command Detail

![02_device_detail](https://github.com/hsakoh/switchbot-mqtt/wiki/images/02_device_detail.png)

* Pressing the plus button will enumerate the field items and command items for the device.
* Enabling the checkbox will make the corresponding field items and command items detectable by the MQTT integration.
* The Source Type indicates the values available through polling and webhook.

#### Command test modal

* Commands have a Test Execution button available, allowing you to execute the API directly from this screen and test its functionality.
![03_command_test](https://github.com/hsakoh/switchbot-mqtt/wiki/images/03_command_test.png)

### Virtual Infrared Remote Devices

There are no field items for virtual infrared remote devices.
You can configure default commands based on the RemoteDeviceType, as well as custom commands.

* The default commands are displayed initially, but note that they may not work as intended based on the custom settings in the SwitchBot app. We recommend verifying their functionality on this screen.
* See the [API specifications](https://github.com/OpenWonderLabs/SwitchBotAPI#send-device-control-commands) for command details.

![04_customize](https://github.com/hsakoh/switchbot-mqtt/wiki/images/04_customize.png)

* Example payload for preset commands:
  * `{"commandType":"command","command": "turnOn","parameter": "default"}`
  * `{"commandType":"command","command":"setPosition","parameter":"0,ff,70"}`

* Example payload for custom commands:
  * `{"commandType":"customize","command": "MyButtonName","parameter": "default"}`

* Example payload for tag commands:
  * `{"commandType":"tag","command": "1","parameter": "default"}`

#### Differences Between Customize and Tags

Tag commands are not documented in the API specifications.
Custom buttons that users have added in the SwitchBot app can be executed using `customize` by specifying their names.
Default operation buttons when a device is detected in the SwitchBot app or selected from the device list seem to be operable with this `tag` command type.
KeySet attempts to enumerate appropriate values as presets, but it may not cover all possibilities.
Try specifying various numerical values to achieve the desired behavior.

(Based on a limited range of testing, it seems that the buttons are assigned sequentially from the top left of the screen, with smaller numbers assigned first. Region-specific keys seem to have higher numbers assigned to them, such as specific keys for Japanese TVs.)

#### December 2024 Update
It seems that the undocumented tag command is no longer functioning.
You can achieve the same result by specifying a number (KeySet number) in the payload of the customize command.
Please refer to [this issue](https://github.com/hsakoh/switchbot-mqtt/issues/57#issuecomment-2564670179) as well.

## Starting the Services

This add-on operates three internal services..

![04_service_control](https://github.com/hsakoh/switchbot-mqtt/wiki/images/04_service_control.png)

|Service|Description|
|--|--|
|MqttCoreService|The main functionality connects to the MQTT broker, reads device configurations, builds and sends Entity configuration information, and subscribes to command processing.|
|PollingService|This service retrieves device information at configured intervals for each device and sends the status to the MQTT broker.|
|WebhookService|Launch Ngrok and registers the Webhook URL with the SwitchBot service.|

Additionally, it runs as an ASP.NET Core Web application with a Webhook endpoint and hosts the BlazorServer of this configuration app itself.

After configuring the device, start the services.
The PollingService cannot be started until the MqttCore service is up and running.
The Webhook service requires activation when using Webhooks, even if Ngrok is not utilized, as registration through the SwitchBotAPI is necessary.

Once you have completed the device configuration and verified its functionality, we recommend enabling the AutoStartServices in add-on configuration.

## Screen image MQTT integration automatic discovery

![05_mqtt_devices](https://github.com/hsakoh/switchbot-mqtt/wiki/images/05_mqtt_devices.png)

![06_ha_lovelace](https://github.com/hsakoh/switchbot-mqtt/wiki/images/06_ha_lovelace.png)

As shown in the above screen, the current add-on implements commands with parameters in a way that they are detected as separate devices by the MQTT integration.

This was done because the intention was to represent parameters as a single command in the default created card.

