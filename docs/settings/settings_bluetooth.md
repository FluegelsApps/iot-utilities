# Bluetooth settings

## BLE scanning

### Scan mode

Tap this setting to change the current scan mode  
Available modes:
- Low power - Consumes least amount of battery, delivers least amount of data
- Balanced (Default)
- Low latency - Consumes highest amount of battery, delivers highest amount of data

## BLE advertising

### Keep advertising alive

- If this setting is enabled, the app will keep advertising in the background if you close the app
- If this setting is disabled, all advertisements will be stopped if you are about to close the app

## BLE testing

### Keep testing alive

- If this setting is enabled, the app will keep the test running in the backgroud if you close the app
- If this setting is disabled, the app will stop testing if you are about to close the app  
Note; The server also has to run in the background because this feature depends on it

### Advertising UUID

Tap this setting to change the iBeacon UUID of the testing advertiser that will be used during all tests

### Advertising power

Tap this setting to change the power level of the testing advertiser that will be used during all tests  
Available levels:
- Ultra-Low (Consumes least battery)
- Low
- Medium
- High (Consumes highest amount of battery)

### Advertising frequency
Tap this setting to change the frequency of the testing advertiser that will be used during all tests. The frequency sets the interval between each advertisement of the iBeacon  
Available frequencies:
- Low power (every ~1000ms)
- Balanced (every ~250ms)
- Low latency (every ~100ms)  
Note: This setting might also have an impact on the battery
