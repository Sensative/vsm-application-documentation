
# Application Gnss-autonomous-test


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


## Application Outputs


### Output batteryPercent (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: % (estimated)

Estimated remaining % of battery in this unit based on measured use time and power for MCU, Radio, Sensors
Position Scans, and potential collateral power use.


### Output bestSatellites (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

### Output numSatellites (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output scanCount (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

## Application Inputs (settings)


## Application Sensors (logical sensors)


### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2
> - Mode: R-
> - Type: Enumeration

Physical button readout sensor


## Application Registers used (device controls)


### Register BATTERY_PERCENT

> - Request current value: Send f4 (hex) on lora port 2
Percent of (non-zero) battery capacity used
> - Mode: R-
> - Unit: mAh

### Register SATELLITE_COUNT

> - Request current value: Send ce (hex) on lora port 2
> - Mode: R-
> - Unit: integer

Reads as the number of satellites seen in the last GNSS scan.


## Meta-Information for this application version



### Application CRC (decimal)

 > 1815337626

### Application Sensor Mask (hex)

 > 2

### Map Data for vsm-translator-open-source

```
M output numSatellites 160 0xa0  1
M output bestSatellites 184 0xb8  1
M output scanCount 185 0xb9  1
M output batteryPercent 161 0xa1  1

```

