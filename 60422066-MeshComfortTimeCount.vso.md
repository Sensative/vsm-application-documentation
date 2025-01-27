
# Application MeshComfortTimeCount


## Generic RutioMesh Module

Generic mesh module allowing both lora wan bridging, network extension or
(with a setting) the device to behave as a leaf only module (which is same as a regular
lorawan module should the device be joined to lorawan network).


Module for detecting (unconfirmed) data loss in network, by updating time by minutes, hours, days and weeks
Let it run for a longer time and then review time series data to detect lost DATA (as opposed to lost uplinks).

## Temperature Sensing and Reporting Module


When the sensor detects an air temperature which has changed from the previous uploaded temperature by more than
the set tempHysteresis it will upload a new temp reading. The temperatures are polled every minute and then processed.


When a temperature is detected which exceeds the tempAlarmHighLevel the tempAlarm will be set to 1.


When a temperature is detected which is below the tempAlarmLowLevel the tempAlarm will be set to -1.


When the temperature is between the low level


When averageTempIntervalMinutes have passed, and if the average temperature has changed more than tempHysteresis degrees,
the sensor will upload a new averageTemp value.


Every minute, the unit will take a humidity sample.

At an interval of averageHumidityIntervalMinutes the unit will recalculate the average humidity value.

The device will do a join attempt if it is not joined and if button is pressed.


An NFC field can be applied to manually trigger a join attempt


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


## Daily Rejoin Module

Should the device not be joined, it will try to rejoin on 24hr interval.


The device will always do a LoRaWan join attempt when powered on (which also includes after a restart)


## Application Outputs


### Output averageHumidity (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: %RH

Average humidity as measured during the last averageHumidityIntervalMinutes.
The measure is sent if the measured average has changed more than humidityTreshold %.


### Output averageTemp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: C

The average temperature uploaded with a resolution 0.01C.


### Output batteryPercent (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: % (estimated)

Estimated remaining % of battery in this unit based on measured use time and power for MCU, Radio, Sensors
Position Scans, and potential collateral power use.


### Output days (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output hours (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output humidity (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: %RH
> - Note: Should the humidity exceed 100% (e.g. dew) following measurements may be sigificantly
affected until the device has dried.

Current humidity, in %RH. Transferred when the measured value has changed more
than humidityThreshold %.


### Output minutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output temp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: C

The temperature uploaded with a resolution of 0.01 C
Accuracy is limited by accuracy of temperature sensor in the product. Refer to datasheet.

### Output tempAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Enumeration
> -- No alarm: 0
> -- High alarm: 1
> -- Low alarm: -1

Temperature alarm state


### Output weeks (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output years (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

## Application Inputs (settings)


### Input averageHumidityIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send ab (hex) on lora port 2
> - Update value to 1: Send ab 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Humidity Interval
> - Unit: Minutes
> - Min: 1
> - Max: 127
> - Default: 60

Interval between the averageHumidity calculations.


### Input averageTempIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a8 (hex) on lora port 2
> - Update value to 1: Send a8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Interval
> - Unit: Minutes
> - Min: 2
> - Max: 127
> - Default: 60

The interval at which average temperature is uploaded (provided that it has changed more than tempHysteresis).


### Input humidityTreshold (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b5 (hex) on lora port 2
> - Update value to 1: Send b5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Humidity Threshold
> - Unit: %
> - Default: 2
> - Min: 0.1
> - Max: 100 (practically disabled when > 100%)

The number of percent change required for an update over LoRaWan of humidity and/or averageHumidity.


### Input meshEnableDownside (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Enable this node as extender

> - UI: Enable Mesh Downside (Extension)
> - Unit: boolean
> - Min: 0
> - Max: 1
> - Default: 0

### Input meshEnableUpside (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Enable this node to join a mesh network (when not joined to LoRaWan network)

> - UI: Enable Mesh Upside (Synchronization)
> - Unit: boolean
> - Min: 0
> - Max: 1
> - Default: 1

### Input meshSyncInterval_minutes (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b0 (hex) on lora port 2
> - Update value to 1: Send b0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Synchronization interval

Synchronization is a relatively expensive operation, so we avoid doing this frequently
should the unit fall outside the mesh. It is recommended to set this to longer times in
in environments that are relatively static.

> - UI: Mesh Sync Interval
> - Unit: minutes
> - Min: 1
> - Max: 65535
> - Default: 120

### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send aa (hex) on lora port 2
> - Update value to 1: Send aa 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature High Alarm Level
> - Unit: C
> - Min: -50
> - Max: 80C
> - Default: 60C (near product max ambient temperature)

The high level for temperature alarm. Set higher than tempAlarmLowLevel or the alarm function is disabled.


### Input tempAlarmLowLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a9 (hex) on lora port 2
> - Update value to 1: Send a9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Low Alarm Level
> - Unit: C
> - Min: -50 C
> - Max: 70 C
> - Default: 2

The low level for temperature alarm. Set lower than tempAlarmHighLevel or the alarm function is disabled.


### Input tempHysteresis (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b3 (hex) on lora port 2
> - Update value to 1: Send b3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Hysteresis
> - Unit: C
> - Min: 0.1
> - Max: 127
> - Default: 0.5

The hysteresis for temperature readings. If temperature changes lower than this value are detected
no report will be generated (saves battery and radio air time).


### Input timecount_interval_minutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a7 (hex) on lora port 2
> - Update value to 1: Send a7 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
How often the minute counter is updated
> - UI: Minute Counter Update Interval
> - Unit: Minutes
> - Default: 10
> - Min: 2
> - Max: 30

## Application Sensors (logical sensors)


### Sensor AIR_HUMIDITY

> - Request current value: Send 05 (hex) on lora port 2
> - Unit: CentiRH%

Air humidity sensor (logical)

### Sensor AIR_TEMPERATURE

> - Request current value: Send 04 (hex) on lora port 2
> - Unit: CentiCelcius

Air temperature sensor (logical)

### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2
> - Mode: R-
> - Type: Enumeration

Physical button readout sensor


### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2
> - Type: Boolean

NFC field present sensor (logical)


## Application Registers used (device controls)


## Meta-Information for this application version



### Application CRC (decimal)

 > 60422066

### Application Sensor Mask (hex)

 > 132

### Map Data for vsm-translator-open-source

```
M input meshSyncInterval_minutes 176 0xb0  1
M input meshEnableUpside 160 0xa0  1
M input meshEnableDownside 161 0xa1  1
M output minutes 162 0xa2  1
M output hours 163 0xa3  1
M output days 164 0xa4  1
M output weeks 165 0xa5  1
M output years 166 0xa6  1
M input timecount_interval_minutes 167 0xa7  1
M output temp 177 0xb1  0.01
M output averageTemp 178 0xb2  0.01
M input tempHysteresis 179 0xb3  0.01
M input averageTempIntervalMinutes 168 0xa8  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 169 0xa9  1
M input tempAlarmHighLevel 170 0xaa  1
M output humidity 180 0xb4  0.01
M output averageHumidity 144 0x90  0.01
M input humidityTreshold 181 0xb5  0.01
M input averageHumidityIntervalMinutes 171 0xab  1
M output batteryPercent 172 0xac  1

```

