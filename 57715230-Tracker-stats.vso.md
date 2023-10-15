
# Application Tracker-stats


## Application Outputs


### Output air_pressure (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 0.01

### Output bestSatellites (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

### Output downlinkRssi (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output gpsTime (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

### Output numSatellites (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output scanCount (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

### Output volts (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001

## Application Inputs (settings)


### Input air_pressure_hysteresis_bar (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input gnssIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input gnssScanMode (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b1 (hex) on lora port 2
> - Update value to 1: Send b1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

## Application Sensors (logical sensors)


### Sensor AIR_PRESSURE

> - Request current value: Send 06 (hex) on lora port 2

### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2

### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2

### Sensor VOLTAGE

> - Request current value: Send 0a (hex) on lora port 2

## Application Registers used (device controls)


### Register DEVICE_STATE

> - Request current value: Send c8 (hex) on lora port 2

### Register GNSS

> - Request current value: Send cc (hex) on lora port 2

### Register GPS_TIME

> - Request current value: Send c7 (hex) on lora port 2

### Register GPS_TIME_MAX_AGE

> - Request current value: Send cd (hex) on lora port 2

### Register LED

> - Request current value: Send c9 (hex) on lora port 2

### Register LINKCHECK_TIME

> - Request current value: Send d0 (hex) on lora port 2

### Register RSSI

> - Request current value: Send d9 (hex) on lora port 2

### Register SATELLITE_BEST_SNR

> - Request current value: Send ec (hex) on lora port 2

### Register SATELLITE_COUNT

> - Request current value: Send ce (hex) on lora port 2

### Register SLEEP_PERIOD

> - Request current value: Send cf (hex) on lora port 2

### Register WIFI

> - Request current value: Send da (hex) on lora port 2

## Meta-Information for this application version



### Application CRC (decimal)

 > 57715230

### Application Sensor Mask (hex)

 > 542

### Map Data for vsm-translator-open-source

M output volts 176 0xb0  0.001
M input gnssIntervalMinutes 160 0xa0  1
M input gnssScanMode 177 0xb1  1
M output numSatellites 161 0xa1  1
M output bestSatellites 184 0xb8  1
M output scanCount 185 0xb9  1
M output gpsTime 186 0xba  1
M output downlinkRssi 162 0xa2  1
M input air_pressure_hysteresis_bar 163 0xa3  1
M output air_pressure 187 0xbb  0.01

