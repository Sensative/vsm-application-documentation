
# Application Lifefinder-motion-wifi

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


## Application Outputs


### Output accumulatedMovingTime (confirmed)

> - Size: 2 bytes
> - Translation factor: 1

### Output accumulatedStationaryTime (confirmed)

> - Size: 2 bytes
> - Translation factor: 1

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


### Output deviceActive (confirmed)

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


### Output volts (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001

## Application Inputs (settings)


### Input activeTimeMaxMinutes (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b4 (hex) on lora port 2
> - Update value to 1: Send b4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input averageTempHysteresis (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 0.1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Average Temperature Threshold
> - Unit: C
> - Min: 0.0
> - Max: 12.7
> - Default: 0.1

The hysteresis for temperature readings. If temperature changes lower than this value are detected
no report will be generated (saves battery and radio air time).


### Input averageTempIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Interval
> - Unit: Minutes
> - Min: 2
> - Max: 127
> - Default: 60

The interval at which average temperature is uploaded (provided that it has changed more than tempHysteresis).


### Input limitedScanChannels (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input movingMotionThreshold_mm_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b6 (hex) on lora port 2
> - Update value to 1: Send b6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input movingPositionMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input stationaryPositionMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input stillMotionThreshold_mm_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b5 (hex) on lora port 2
> - Update value to 1: Send b5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send b2 (hex) on lora port 2
> - Update value to 1: Send b2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Threshold
> - Unit: C
> - Min: 0.1
> - Max: 127
> - Default: 0.5

The hysteresis for temperature readings. If temperature changes lower than this value are detected
no report will be generated (saves battery and radio air time).


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

### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2
> - Type: Boolean

NFC field present sensor (logical)


### Sensor VOLTAGE

> - Request current value: Send 0a (hex) on lora port 2
> - Unit: mV (milliVolts)

Measured voltage on the board.

## Application Registers used (device controls)


## Meta-Information for this application version



### Application CRC (decimal)

 > 1054688892

### Application Sensor Mask (hex)

 > 400510

### Map Data for vsm-translator-open-source

```
M output temp 176 0xb0  0.01
M output averageTemp 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input averageTempHysteresis 160 0xa0  0.1
M input averageTempIntervalMinutes 161 0xa1  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 162 0xa2  1
M input tempAlarmHighLevel 163 0xa3  1
M output batteryPercent 164 0xa4  1
M output volts 179 0xb3  0.001
M output deviceActive 129 0x81  1
M input activeTimeMaxMinutes 180 0xb4  1
M input stillMotionThreshold_mm_s2 181 0xb5  1
M input movingMotionThreshold_mm_s2 182 0xb6  1
M input limitedScanChannels 184 0xb8  1
M input stationaryPositionMinutes 165 0xa5  1
M input movingPositionMinutes 166 0xa6  1
M output accumulatedStationaryTime 144 0x90  1
M output accumulatedMovingTime 145 0x91  1

```

