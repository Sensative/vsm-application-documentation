
# Application Airport-budget


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
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input fullScanChannels (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b9 (hex) on lora port 2
> - Update value to 1: Send b9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input fullWifiScan_minutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input gpsScan_minutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a7 (hex) on lora port 2
> - Update value to 1: Send a7 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input limitedScanChannels (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input maxBudget (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b5 (hex) on lora port 2
> - Update value to 1: Send b5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input minimumWifiCount (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input motionThreshold_mm_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b3 (hex) on lora port 2
> - Update value to 1: Send b3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input quarterlyScanBudget (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input singleWifiScanAgain_minutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input tempAlarmLowLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input tempHysteresis (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b2 (hex) on lora port 2
> - Update value to 1: Send b2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

## Application Sensors (logical sensors)


### Sensor ACC_X

> - Request current value: Send 1a (hex) on lora port 2

### Sensor ACC_Y

> - Request current value: Send 1b (hex) on lora port 2

### Sensor ACC_Z

> - Request current value: Send 1c (hex) on lora port 2

### Sensor AIR_TEMPERATURE

> - Request current value: Send 04 (hex) on lora port 2

### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2

### Sensor VOLTAGE

> - Request current value: Send 0a (hex) on lora port 2

## Application Registers used (device controls)


### Register APP_CONFIG

> - Request current value: Send ca (hex) on lora port 2

### Register DATA_RATE

> - Request current value: Send d4 (hex) on lora port 2

### Register DEVICE_STATE

> - Request current value: Send c8 (hex) on lora port 2

### Register GNSS

> - Request current value: Send cc (hex) on lora port 2

### Register LED

> - Request current value: Send c9 (hex) on lora port 2

### Register LINKCHECK_TIME

> - Request current value: Send d0 (hex) on lora port 2

### Register STREAMING_RATE

> - Request current value: Send d6 (hex) on lora port 2

### Register TX_POWER_INDEX

> - Request current value: Send d7 (hex) on lora port 2

### Register TX_POWER_RANGE

> - Request current value: Send d8 (hex) on lora port 2

### Register WIFI

> - Request current value: Send da (hex) on lora port 2

### Register WIFI_CHANNELS

> - Request current value: Send f6 (hex) on lora port 2

### Register WIFI_COUNT

> - Request current value: Send db (hex) on lora port 2

### Register WIFI_TYPES

> - Request current value: Send f7 (hex) on lora port 2

## Meta-Information for this application version



### Application CRC (decimal)

 > 1619903829

### Application Sensor Mask (hex)

 > 1c000510

### Map Data for vsm-translator-open-source

M output temp 176 0xb0  0.01
M output averageTemp 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input averageTempIntervalHours 160 0xa0  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 161 0xa1  1
M input tempAlarmHighLevel 162 0xa2  1
M input motionThreshold_mm_s2 179 0xb3  1
M output volts 180 0xb4  0.001
M input limitedScanChannels 184 0xb8  1
M input fullScanChannels 185 0xb9  1
M input quarterlyScanBudget 163 0xa3  1
M input maxBudget 181 0xb5  1
M input singleWifiScanAgain_minutes 164 0xa4  1
M input minimumWifiCount 165 0xa5  1
M input fullWifiScan_minutes 166 0xa6  1
M input gpsScan_minutes 167 0xa7  1

