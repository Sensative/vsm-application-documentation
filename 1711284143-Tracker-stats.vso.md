
# Application Tracker-stats


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


## Application Outputs


### Output air_pressure (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 0.01

### Output batteryPercent (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: % (estimated)

Estimated remaining % of battery in this unit based on measured use time and power for MCU, Radio, Sensors
Position Scans, and potential collateral power use.


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
Interval of GNSS scans
> - Default: 30
> - Min: 1
> - Max: 127
> - Unit: minutes

### Input gnssScanMode (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b1 (hex) on lora port 2
> - Update value to 1: Send b1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
GNSS scanning mode
> - Default: 0x401 Default to look for at least 4 satellites, assisted scan
> - Min: 0xf01
> - Max: 0x301

## Application Sensors (logical sensors)


### Sensor AIR_PRESSURE

> - Request current value: Send 06 (hex) on lora port 2
> - Unit: Pa

Air humidity sensor (logical)


### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2
> - Mode: R-
> - Type: Enumeration

Physical button readout sensor


### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2
> - Type: Boolean

NFC field present sensor (logical)


### Sensor VOLTAGE

> - Request current value: Send 0a (hex) on lora port 2
> - Unit: mV (milliVolts)

Measured voltage on the board.

## Application Registers used (device controls)


### Register BATTERY_PERCENT

> - Request current value: Send f4 (hex) on lora port 2
Percent of (non-zero) battery capacity used
> - Mode: R-
> - Unit: mAh

### Register GPS_TIME

> - Request current value: Send c7 (hex) on lora port 2
> - Mode: R-
> - Unit: Seconds

Current device time (GPS epoch)


### Register GPS_TIME_MAX_AGE

> - Request current value: Send cd (hex) on lora port 2
> - Mode: RW
> - Unit: Seconds
> - Default: 0
> - Min: 0
> - Max: 4294967295
Read/Set GPS time maximum age. Reads 0 if no GPS time is set.
Once this maximum age has passed the device will no longer trust its GPS_TIME.
Also, it will start emitting DEVICE_TIME requests on the LoRaWan network once 80% of this time has passed.


### Register LINKCHECK_TIME

> - Request current value: Send d0 (hex) on lora port 2
> Mode: RW
> Unit: seconds
> Min: 300
> Max: 2592000
> Default: 86400
Once 80% of this time has passed, the device will make all messages confirmed until it gets a confirmation.
Should this time pass without the device hearing a confirmed response, it will go to DEVICE_STATE_ACTIVE_UNJOINED.


### Register RSSI

> - Request current value: Send d9 (hex) on lora port 2
RSSI for last downlink / join response
> - Mode: R-
> - Unit: dBm

### Register SATELLITE_COUNT

> - Request current value: Send ce (hex) on lora port 2
> - Mode: R-
> - Unit: integer

Reads as the number of satellites seen in the last GNSS scan.


## Meta-Information for this application version



### Application CRC (decimal)

 > 1711284143

### Application Sensor Mask (hex)

 > 542

### Map Data for vsm-translator-open-source

```
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
M output batteryPercent 164 0xa4  1

```

