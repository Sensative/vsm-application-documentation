
# Application Puck-tracker


## Application Outputs


### Output averageTemp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01

### Output temp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01

### Output tempAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output volts (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001

## Application Inputs (settings)


### Input averageTempIntervalHours (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input gnssIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input roamNetworkCount (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input tempAlarmLowLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input tempHysteresis (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b2 (hex) on lora port 2
> - Update value to 1: Send b2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input wifiIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

## Application Sensors (logical sensors)


### Sensor AIR_TEMPERATURE

> - Request current value: Send 04 (hex) on lora port 2

### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2

### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2

### Sensor VOLTAGE

> - Request current value: Send 0a (hex) on lora port 2

## Application Registers used (device controls)


### Register APP_CONFIG

> - Request current value: Send ca (hex) on lora port 2

### Register BOARD

> - Request current value: Send c0 (hex) on lora port 2

### Register DEVICE_STATE

> - Request current value: Send c8 (hex) on lora port 2

### Register GNSS

> - Request current value: Send cc (hex) on lora port 2

### Register GPS_TIME_MAX_AGE

> - Request current value: Send cd (hex) on lora port 2

### Register JOIN_SETTINGS

> - Request current value: Send e7 (hex) on lora port 2

### Register LED

> - Request current value: Send c9 (hex) on lora port 2

### Register LINKCHECK_TIME

> - Request current value: Send d0 (hex) on lora port 2

### Register SATELLITE_COUNT

> - Request current value: Send ce (hex) on lora port 2

### Register SLEEP_PERIOD

> - Request current value: Send cf (hex) on lora port 2

### Register WIFI

> - Request current value: Send da (hex) on lora port 2

## Meta-Information for this application version



### Application CRC (decimal)

 > 376700598

### Application Sensor Mask (hex)

 > 512

### Map Data for vsm-translator-open-source

M input roamNetworkCount 160 0xa0  1
M output temp 176 0xb0  0.01
M output averageTemp 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input averageTempIntervalHours 161 0xa1  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 162 0xa2  1
M input tempAlarmHighLevel 163 0xa3  1
M output volts 179 0xb3  0.001
M input gnssIntervalMinutes 164 0xa4  1
M input wifiIntervalMinutes 165 0xa5  1

