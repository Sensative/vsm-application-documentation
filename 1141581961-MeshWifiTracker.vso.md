
# Application MeshWifiTracker


## Generic RutioMesh Module

Generic mesh module allowing both lora wan bridging, network extension or
(with a setting) the device to behave as a leaf only module (which is same as a regular
lorawan module should the device be joined to lorawan network).

Module for package loss / device restart detection
## Temperature Sensing and Reporting Module


When the sensor detects an air temperature which has changed from the previous uploaded temperature by more than
the set tempHysteresis (threshold) it will upload a new temp reading. The temperatures are polled every minute and then processed.


When a temperature is detected which exceeds the tempAlarmHighLevel the tempAlarm will be set to 1.


When a temperature is detected which is below the tempAlarmLowLevel the tempAlarm will be set to -1.


When the temperature is between the low level


When averageTempIntervalMinutes have passed, and if the average temperature has changed more than tempHysteresis (threshold) degrees C,
the sensor will upload a new averageTemp value.


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


## Budgeted and configurable rejoin module


### Rejoin Budget Operation

> Counter is incremented every 15 minutes when device is unjoined.

After counter reaches the set rejoinTime value, trigger a rejoin, decrement budget and reset the counter.
Budget is refilled daily by rejoinBudgetRefill up to rejoinBudgetMax. Excess budget is scraped off the top.


The device will always do a LoRaWan join attempt when powered on (which also includes after a restart)


## Application Outputs


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


### Output hours (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
The number of hours the device has been on since activated (restarted).

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


## Application Inputs (settings)


### Input averageTempHysteresis (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 0.1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Average Temperature Threshold
> - Unit: C
> - Min: 0.0
> - Max: 12.7
> - Default: 0.1

The hysteresis for temperature readings. If the average temperature changes less than this value
no report will be generated (saves battery and radio air time).


### Input averageTempIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Average Temperature Interval
> - Unit: Minutes
> - Min: 2
> - Max: 127
> - Default: 60

The interval at which average temperature is uploaded provided that it has changed more than the average temperature threshold (hysteresis).


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

### Input motionThreshold_m_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b6 (hex) on lora port 2
> - Update value to 1: Send b6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Motion threshold

> - Min: 0.010
> - Max: 10.000
> - Default: 50
> - Unit: mm/s2

### Input rejoinBudgetMax (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a7 (hex) on lora port 2
> - Update value to 1: Send a7 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Maximum Rejoin Budget
> - Unit: Integer
> - Min: 0
> - Max: 127
> - Default:  5

Max amount of rejoins the device is allowed before being throttled.


### Input rejoinBudgetRefill (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a8 (hex) on lora port 2
> - Update value to 1: Send a8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Daily Rejoin Budget Refill
> - Unit: Integer
> - Min: 0
> - Max: 127
> - Default: 1

How many rejoin attempts are added to the device every day.


### Input rejoinTime (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b5 (hex) on lora port 2
> - Update value to 1: Send b5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Quarters Between Rejoins
> - Unit: 15 minute segments
> - Min: 1
> - Max: 32767
> - Default: 2

How many 15 minute segments of unjoined time before triggering a rejoin, as well as the time between the budgeted rejoin attempts.


### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send b4 (hex) on lora port 2
> - Update value to 1: Send b4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Threshold
> - Unit: C
> - Min: 0.1
> - Max: 127
> - Default: 0.5

The hysteresis for temperature readings. If temperature changes lower than this value are detected
no temperature report will be generated (saves battery and radio air time).


### Input wifiMovingScanInterval_min (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send aa (hex) on lora port 2
> - Update value to 1: Send aa 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Number of minutes between wifi scans while moving.

> - Min: 0
> - Max: 127
> - Default: 5
> - Unit: minutes
> - UI: Wifi Scan Interval while Moving

When set to 0 or less, the interval scanning is disabled.


### Input wifiStillScanInterval_h (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a9 (hex) on lora port 2
> - Update value to 1: Send a9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Number of hours between wifi scans while still

> - Min: 0
> - Max: 127
> - Default: 6
> - Unit: hours
> - UI: Wifi Scan Interval while Still

When set to 0 or less, the interval scanning is disabled.


## Application Sensors (logical sensors)


### Sensor AIR_TEMPERATURE

> - Request current value: Send 04 (hex) on lora port 2
> - Unit: CentiCelcius

Air temperature sensor (logical)

### Sensor MOTION

> - Request current value: Send 16 (hex) on lora port 2
> - Type: Enumeration

Motion sensor reading, one of
- 0 : Unknown
- 1 : Still (less than register MOTION_CONTROL mm/s2 acceleration change detected through last minute)
- 2 : Moving (more than register MOTION_CONTROL mm/s2 acceleration change detected through last minute)
- 3 : Shocked (more than 4m/s2 change in acceleration detected through last minute)

## Application Registers used (device controls)


## Meta-Information for this application version



### Application CRC (decimal)

 > 1141581961

### Application Sensor Mask (hex)

 > 400010

### Map Data for vsm-translator-open-source

```
M input meshSyncInterval_minutes 176 0xb0  1
M input meshEnableUpside 160 0xa0  1
M input meshEnableDownside 161 0xa1  1
M output hours 177 0xb1  1
M output temp 178 0xb2  0.01
M output averageTemp 179 0xb3  0.01
M input tempHysteresis 180 0xb4  0.01
M input averageTempHysteresis 162 0xa2  0.1
M input averageTempIntervalMinutes 163 0xa3  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 164 0xa4  1
M input tempAlarmHighLevel 165 0xa5  1
M output batteryPercent 166 0xa6  1
M input rejoinBudgetMax 167 0xa7  1
M input rejoinBudgetRefill 168 0xa8  1
M input rejoinTime 181 0xb5  1
M input wifiStillScanInterval_h 169 0xa9  1
M input wifiMovingScanInterval_min 170 0xaa  1
M input motionThreshold_m_s2 182 0xb6  0.01

```

