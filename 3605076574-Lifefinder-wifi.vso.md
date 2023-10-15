
# Application Lifefinder-wifi

## Temperature Sensing and Reporting Module
When the sensor detects an air temperature which has changed from the previous uploaded temperature by more than
the set tempHysteresis it will upload a new temp reading. The temperatures are polled every minute and then processed.
When a temperature is detected which exceeds the tempAlarmHighLevel the tempAlarm will be set to 1.
When a temperature is detected which is below the tempAlarmLowLevel the tempAlarm will be set to -1.
When the temperature is between the low level
When averageTempIntervalMinutes have passed, and if the average temperature has changed more than tempHysteresis degrees,
the sensor will upload a new averageTemp value.

## Application Outputs


### Output alarmTime (confirmed)

> - Size: 2 bytes
> - Translation factor: 1

### Output averageTemp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> Unit:C
The average temperature uploaded with a resolution 0.01C.

### Output buttonAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output temp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> Unit: C
The temperature uploaded with a resolution of 0.01 C
Accuracy is limited by accuracy of temperature sensor in the product. Refer to datasheet.

### Output tempAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> Unit: Enumeration
> No alarm: 0
> High alarm: 1
> Low alarm: -1

### Output volts (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001

## Application Inputs (settings)


### Input averageTempIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> Unit: Minutes
> Min: 2
> Max: 127
The interval at which average temperature is uploaded (provided that it has changed more than tempHysteresis).

### Input limitedScanChannels (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input maxAlarmMinutes (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b4 (hex) on lora port 2
> - Update value to 1: Send b4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> Unit: C
> Min: -127C
> Max: 127C
> Default: 60C (near product max ambient temperature)
The high level for temperature alarm. Set higher than tempAlarmLowLevel or the alarm function is disabled.

### Input tempAlarmLowLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> Unit: C
> Min: -128 C
> Max: 126 C
> Default: 2 C (near freezing point)
The low level for temperature alarm. Set lower than tempAlarmHighLevel or the alarm function is disabled.

### Input tempHysteresis (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b2 (hex) on lora port 2
> - Update value to 1: Send b2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> Unit:C
> Min: 0.1C
> Max: 127C
> Default: 2C
The hysteresis for temperature readings. If temperature changes lower than this value are detected
no report will be generated (saves battery and radio air time).

## Application Sensors (logical sensors)


### Sensor AIR_TEMPERATURE

> - Request current value: Send 04 (hex) on lora port 2

### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2

### Sensor VOLTAGE

> - Request current value: Send 0a (hex) on lora port 2

## Application Registers used (device controls)


### Register ALARM_LED_STYLE

> - Request current value: Send d1 (hex) on lora port 2

### Register APP_CONFIG

> - Request current value: Send ca (hex) on lora port 2

### Register DEVICE_STATE

> - Request current value: Send c8 (hex) on lora port 2

### Register LED

> - Request current value: Send c9 (hex) on lora port 2

### Register LINKCHECK_TIME

> - Request current value: Send d0 (hex) on lora port 2

### Register STREAMING_RATE

> - Request current value: Send d6 (hex) on lora port 2

### Register WIFI

> - Request current value: Send da (hex) on lora port 2

### Register WIFI_CHANNELS

> - Request current value: Send f6 (hex) on lora port 2

## Meta-Information for this application version



### Application CRC (decimal)

 > 3605076574

### Application Sensor Mask (hex)

 > 412

### Map Data for vsm-translator-open-source

M output temp 176 0xb0  0.01
M output averageTemp 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input averageTempIntervalMinutes 160 0xa0  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 161 0xa1  1
M input tempAlarmHighLevel 162 0xa2  1
M output alarmTime 144 0x90  1
M output buttonAlarm 129 0x81  1
M output volts 179 0xb3  0.001
M input maxAlarmMinutes 180 0xb4  1
M input alarmAck 164 0xa4  1
M input limitedScanChannels 184 0xb8  1

