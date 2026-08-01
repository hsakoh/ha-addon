# CHANGELOG

## v1.1.0 - 2026-08-01
- 第2世代スマートメーターに対応(Bルート識別番号(0xC0)・1分積算電力量(0xD0)のセンサー/ボタンを追加、Appendix Release R(rev4)に更新)
- 複数メーター巡回モードを追加(Meters 設定による 接続→取得→切断 の巡回、PAN情報キャッシュ、メーター毎のMQTT公開)
- broute-wifi-mqtt との同時稼働向けに識別子へ _wisun サフィックスを付与する AddWiSunSuffix オプションを追加
- HAデバイス名に製造番号を含めるよう変更
- 単体モードでPANAセッション喪失時に次回ポーリングで自動再接続するよう修正
- メーター初期化タイムアウト時にホストが停止する問題を修正し、セッション再確立リトライ・PAN未発見メーターの除外・再接続前クールダウンを追加
- PANA接続タイムアウトの既定値を60秒に変更、プロパティ読み出し間隔(PropertyReadIntervalDelay)を設定可能に

## v1.0.12 - 2026-04-02
- Fix handling of ERXUDP events with different lengths when SA2 flag is enabled on BP35C0

## v1.0.11 - 2026-01-27
- Changed the .NET runtime to explicitly define the virtual memory range reserved(but not used) for the GC heap.
- This prevents the TOP command from showing an extremely large VIRT value.

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
