
# Application Motion-measure


## Lower Power Temperature Sensing and Reporting Module


### General Temperature Operation

> The temperature is measured every 15 minutes and then processed.

When the sensor detects an air temperature which has changed from the previous uploaded temperature by more than
the set tempHysteresis it will upload a new temp reading.


### Temperature Alarms

When a temperature is detected which exceeds the tempAlarmHighLevel the tempAlarm will be set to 1.


When a temperature is detected which is below the tempAlarmLowLevel the tempAlarm will be set to -1.


### Current Temperature Reporting

The current temperature is uploaded should the temperature have changed more than the set tempHysteresis


### Average Temperature Reporting

When averageTempIntervalMinutes have passed, and if the average temperature has changed more than tempHysteresis degrees,
the sensor will upload a new averageTemp value.

## Slow Tracker Module

This module enables slow tracking through WIFI scanning or GNSS scans.
For proper functioning the GNSS almanac and device time needs to be kept up-to-date, for instance through NFC application or through enabling the dots-mqtt-client


When the button is pressed, a wifi scan will be done.


Daily when the device is joined, it will attempt a wifi scan.


Weekly, when the device is joined, it will attempt a GNSS scan.


## Application Outputs


### Output accX (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.001

### Output accY (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.001

### Output accZ (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.001

### Output averageTemp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit:C

The average temperature uploaded with a resolution 0.01C.


### Output motion (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Enumeration
> -- 0 = Unknown
> -- 1 = Immobile
> -- 2 = Moving
> -- 3 = Acceleration exceeded 4m/s2 comparred to last sample (e.g. shock)
Motion detector status

### Output pressure_hPa (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 0.01

### Output temp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: C

The temperature uploaded with a resolution of 0.01 C

> Accuracy is limited by accuracy of temperature sensor in the product. Refer to datasheet.

### Output tempAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Enumeration
> -- No alarm: 0
> -- High alarm: 1
> -- Low alarm: -1

Confirmed uplink which will indicate if one of the set limits are exceeded


## Application Inputs (settings)


### Input averageTempIntervalHours (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Hours
> - Min: 1h
> - Max: 127h
> - Default: 2h

The interval at which average temperature is uploaded (provided that it has changed more than tempHysteresis).


### Input enableBarometer (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Boolean
> - Default: 0 (false)
Enable barometric pressure uploading

### Input motionThreshold_m_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001
> - Request current value: Send b3 (hex) on lora port 2
> - Update value to 1: Send b3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input sampleCountMax (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input sampleInterval_s (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: C
> - Min: -127C
> - Max: 127C
> - Default: 60C (near product max ambient temperature)

The high level for temperature alarm. Set higher than tempAlarmLowLevel or the alarm function is disabled.


### Input tempAlarmLowLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: C
> - Min: -128 C
> - Max: 126 C
> - Default: 2 C (near freezing point)

The low level for temperature alarm. Set lower than tempAlarmHighLevel or the alarm function is disabled.


### Input tempHysteresis (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b2 (hex) on lora port 2
> - Update value to 1: Send b2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit:C
> - Min: 0.1C
> - Max: 127C
> - Default: 2C

The hysteresis for temperature readings. If temperature changes lower than this value are detected
no report will be generated (saves battery and radio air time).


## Application Sensors (logical sensors)


### Sensor ACC_X

> - Request current value: Send 1a (hex) on lora port 2
Current accelerometer reading

### Sensor ACC_Y

> - Request current value: Send 1b (hex) on lora port 2
Current accelerometer reading

### Sensor ACC_Z

> - Request current value: Send 1c (hex) on lora port 2
Current accelerometer reading

### Sensor AIR_PRESSURE

> - Request current value: Send 06 (hex) on lora port 2
> - Unit: Pa

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


## Application Registers used (device controls)


### Register APP_CONFIG

> - Request current value: Send ca (hex) on lora port 2
> - Mode: RW
> - Unit: Bit mask

Enable or disable certain functions of the device, such as power on/off behaviours.


### Register DEVICE_STATE

> - Request current value: Send c8 (hex) on lora port 2
> - Mode: RW
> - Unit: Enumeration

Current application state of the device. Can be written by application to affect the devices application state.

> - DEVICE_STATE_ACTIVE_UNJOINED (running but not joined to network)
> - DEVICE_STATE_ACTIVE_JOINING (running and attempting to join network)
> - DEVICE_STATE_ACTIVE_JOINED (running and joined to network)
> - DEVICE_STATE_ACTIVE_STREAMING (running and uploading pending data packages)
> - DEVICE_STATE_ACTIVE_ON_RADIO (running and currently working with the radio)
> - DEVICE_STATE_OFF (normally not accessible from VM but possible to write to turn off the device)
> - Others Reserved by runtime

### Register GNSS

> - Request current value: Send cc (hex) on lora port 2
> - Mode: -W
> - Type: Two * 1 bytes

Trigger GNSS scans

> - Byte 0: 0 = Attempt assisted scan if device knows GPS time and has GNSS almanac. 1 = force unassisted scan.
> - Byte 1: Minimum number of found satellites to trigger an uplink


### Register GPS_TIME_MAX_AGE

> - Request current value: Send cd (hex) on lora port 2
> - Mode: RW
> - Unit: Seconds

Read/Set GPS time maximum age. Reads 0 if no GPS time is set.
Once this maximum age has passed the device will no longer trust its GPS_TIME.
Also, it will start emitting DEVICE_TIME requests on the LoRaWan network once 80% of this time has passed.


### Register LED

> - Request current value: Send c9 (hex) on lora port 2
> - Mode: -W
> - Unit: Enumeration

Write in order to effect the application LED (not available on all device models)


### Register MOTION_CONTROL

> - Request current value: Send ef (hex) on lora port 2

### Register NOW

> - Request current value: Send c5 (hex) on lora port 2
> - Mode: R-
> - Unit: Seconds

Current time in seconds since device powered on.


### Register SLEEP_PERIOD

> - Request current value: Send cf (hex) on lora port 2
> - Mode: RW
> - Unit: seconds

When set to non-zero value the VM will wake up at at this interval. Make rules dependent on NOW or


### Register STREAMING_RATE

> - Request current value: Send d6 (hex) on lora port 2
> - Mode: RW
> - Unit: Seconds

The average rate at which the device streams data, e.g. delay between lora transactions.
Actual rate is randomized at this value +- 50% to avoid potential repeat collisions, for instance if the device is
triggered by sound or acceleration.

### Register WIFI

> - Request current value: Send da (hex) on lora port 2

## Meta-Information for this application version



### Application CRC (decimal)

 > 3038191195

### Application Sensor Mask (hex)

 > 1c400152

### Map Data for vsm-translator-open-source

```
M output temp 176 0xb0  0.01
M output averageTemp 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input averageTempIntervalHours 160 0xa0  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 161 0xa1  1
M input tempAlarmHighLevel 162 0xa2  1
M output accX 144 0x90  0.001
M output accY 145 0x91  0.001
M output accZ 146 0x92  0.001
M output pressure_hPa 184 0xb8  0.01
M input motionThreshold_m_s2 179 0xb3  0.001
M input sampleInterval_s 163 0xa3  1
M input sampleCountMax 164 0xa4  1
M input enableBarometer 165 0xa5  1
M output motion 166 0xa6  1

```

