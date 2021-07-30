---
layout: default
title: Bluetooth Settings
parent: Settings
grand_parent: App Documentation
---

# Bluetooth settings

## BLE scanning

### Scan mode

Tap this preference to change the current scan mode  
Available modes:
- Low power - Consumes least amount of battery, delivers least amount of data
- Balanced - Balanced battery usage and data delivery
- Low latency - Consumes highest amount of battery, delivers highest amount of data

## BLE advertising

### Keep advertising alive

- If this feature is enabled, the app will keep advertising in the background if you close the app
- If this feature is disabled, all advertisements will be stopped if you are about to close the app

## BLE testing

### Keep testing alive

- If this feature is enabled, the app will keep the test running in the backgroud if you close the app
- If this feature is disabled, the app will stop testing if you are about to close the app  

> **_Note:_** The server also has to run in the backgroud as this feature depends on it.
> This feature requires ["Keep server alive"](./settings_iotserver.md) as well as ["Keep advertising alive"](#keep-advertising-alive) to run in the background with the app closed.
