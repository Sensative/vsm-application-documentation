
# Application Heartstarter


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


## Application Outputs


### Output averageTemp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit:C

The average temperature uploaded with a resolution 0.01C.


### Output buttonDetect (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output motionDetect (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output soundIntervalS (confirmed)

> - Size: 4 bytes
> - Translation factor: 0.001

### Output soundRepeat (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

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


### Output volts (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001

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


### Input motionThresholdG (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001
> - Request current value: Send b4 (hex) on lora port 2
> - Update value to 1: Send b4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input soundScanIntervalMinutes (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b3 (hex) on lora port 2
> - Update value to 1: Send b3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input soundScanMinimumRepeat (unconfirmed)

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


### Sensor SOUND_INTERVAL_MS

> - Request current value: Send 18 (hex) on lora port 2

### Sensor SOUND_REPEAT

> - Request current value: Send 19 (hex) on lora port 2

### Sensor VOLTAGE

> - Request current value: Send 0a (hex) on lora port 2
> - Unit: mV (milliVolts)

Measured voltage on the board.

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


### Register LED

> - Request current value: Send c9 (hex) on lora port 2
> - Mode: -W
> - Unit: Enumeration

Write in order to effect the application LED (not available on all device models)


### Register LINKCHECK_TIME

> - Request current value: Send d0 (hex) on lora port 2
> Mode: RW
> Unit: seconds

Once 80% of this time has passed, the device will make all messages confirmed until it gets a confirmation.
Should this time pass without the device hearing a confirmed response, it will go to DEVICE_STATE_ACTIVE_UNJOINED.


### Register SOUND_CONTROL

> - Request current value: Send ed (hex) on lora port 2

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

 > 3886254671

### Application Sensor Mask (hex)

 > 1f000512

### Map Data for vsm-translator-open-source

M output temp 176 0xb0  0.01
M output averageTemp 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input averageTempIntervalHours 160 0xa0  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 161 0xa1  1
M input tempAlarmHighLevel 162 0xa2  1
M output buttonDetect 129 0x81  1
M output motionDetect 130 0x82  1
M input soundScanIntervalMinutes 179 0xb3  1
M input soundScanMinimumRepeat 163 0xa3  1
M output soundIntervalS 152 0x98  0.001
M output soundRepeat 131 0x83  1
M input motionThresholdG 180 0xb4  0.001
M output volts 181 0xb5  0.001

