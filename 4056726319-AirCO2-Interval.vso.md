
# Application AirCO2-Interval


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


## Daily Rejoin Module

Should the device not be joined, it will try to rejoin on 24hr interval.


The device will do a join attempt if it is not joined and if button is pressed.


An NFC field can be applied to manually trigger a join attempt


## ADR dampening and limiting module

Adaptive LoRaWan data rate dampening and limiter module, allows to limit both adaptability rate and worst data rate / output power.
This is intended for fixed-mount devices where radio conditions are not expected to change rapidly.


This module is calibrated for the white plastics of Square with no holes.

Every minute, the unit will take a light sample.
At an interval of averageLuxIntervalMinutes the unit will recalculate the average lux value.
If the value of average lux was changed more than the luxTresholdPercent it will send an update.

Once the device is joined, the BSEC library is activated (and the air sensor).

## AIR Quality Measurement Module

This module uses the Bosch BSEC library and the Bosch BME68x sensor to measure
and estimate air qualities. Please refer to Bosch sensor documentation for reference.

Power in CO2 sensor when we go into OFF state
Power in CO2 sensor when we get joined

> Note that the first sample uplinked can be from a partial measurement period,
> and should be disregarded.

## Application Outputs


### Output air_co2 (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

BSEC co2 indication. See BME68x documentation.


### Output air_equivalent_co2 (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

BSEC co2 indication. See BME68x documentation.


### Output air_humidity (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - unit: %rh

average humidity as measured during the last averagehumidityintervalminutes.
the measure is sent if the measured average has changed more than humiditytreshold %.


### Output air_iaq (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

BSEC iaq measure. See BME68x documentation.


### Output air_iaq_accuracy (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

BSEC library iaq accuracy. See BME68x documentation.


### Output air_pressure (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 0.01
> - Unit: hPa

BSEC air pressure.


### Output air_run_in_status (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

BSEC library run-in status. See BME68x documentation.


### Output air_stab_status (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

BSEC library stabilization status. See BME68x documentation.


### Output air_static_iaq (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

BSEC iaq indication (not recalibrated). See BME68x documentation.


### Output air_temperature (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: C

The average temperature uploaded with a resolution 0.01C.


### Output averageLux (confirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Unit: Lux

The (lineary) average Lux value.


### Output batteryPercent (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: % (estimated)

Estimated remaining % of battery in this unit based on measured use time and power for MCU, Radio, Sensors
Position Scans, and potential collateral power use.


### Output lux (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Unit: Lux

Luminance in Lux


## Application Inputs (settings)


### Input air_interval_minutes (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b3 (hex) on lora port 2
> - Update value to 1: Send b3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Minutes
> - Min: 5
> - Max: 32767
> - Default: 30

In practice this setting should be set to a multiple of 5 for best results.
The device will calculate an average of the various air sensor measures during
the period (the internal sampling interval is 5 minutes due to BSEC library settings).


### Input averageLuxIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Average Lux Report Interval
> - Unit: Minutes
> - Default: 20 minutes
> - Min: 2
> - Max: 127
Interval between the averageHumidity calculations and updates (when results changed)


### Input luxTresholdPercent (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b1 (hex) on lora port 2
> - Update value to 1: Send b1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Lux Threshold
> - Unit: %
> - Default: 100
> - Min: 1
> - Max: 32767

The number of percent change required for an update over LoRaWan of lux and/or averageLux.


### Input maxPowerIndex (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Max Power Index
> - Unit: LoraWan power index (0-16)
> - Min: 0
> - Max: 16
> - Default: 16

maximum power index to use for LoRaWan traffic, including join. Default setting disables DR0

### Input powerIndexFilterFactorDown (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: LoRaWan power filter factor down
> - Unit: Integer
> - Min: 1
> - Max: 50
> - Default: 3

Low pass filter factor. 1 = no low-pass filter. 2 = filter factor 1 (fast) ... 10 = very slow.
When the built-in ADR function propose a new faster power index, this filter factor is employed in a low pass filter.
If the filter value is set to 1 the algorithm will use its proposed new value (if below or at max).

### Input powerIndexFilterFactorUp (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: LoRaWan power filter factor up
> - Unit: Integer
> - Min: 1
> - Max: 50
> - Default: 3

Low pass filter factor. 1 = no low-pass filter. 2 = filter factor 1 (fast) ... 10 = very slow.
When the built-in ADR function propose a new slower power index, this filter factor is employed in a low pass filter.
If the filter value is set to 1 the algorithm will use its proposed new value (if below or at max).

## Application Sensors (logical sensors)


### Sensor AIR_CO2_EQUIVALENT

> - Request current value: Send 13 (hex) on lora port 2

### Sensor AIR_HUMIDITY

> - Request current value: Send 05 (hex) on lora port 2
> - Unit: CentiRH%

Air humidity sensor (logical)

### Sensor AIR_IAQ

> - Request current value: Send 0c (hex) on lora port 2

### Sensor AIR_IAQ_ACCURACY

> - Request current value: Send 0d (hex) on lora port 2

### Sensor AIR_PRESSURE

> - Request current value: Send 06 (hex) on lora port 2
> - Unit: Pa

Air humidity sensor (logical)


### Sensor AIR_RUNIN_STATUS

> - Request current value: Send 12 (hex) on lora port 2

### Sensor AIR_STAB_STATUS

> - Request current value: Send 11 (hex) on lora port 2

### Sensor AIR_STATIC_IAQ

> - Request current value: Send 10 (hex) on lora port 2

### Sensor AIR_TEMPERATURE

> - Request current value: Send 04 (hex) on lora port 2
> - Unit: CentiCelcius

Air temperature sensor (logical)

### Sensor AMBIENT_LIGHT

> - Request current value: Send 0b (hex) on lora port 2
> - Unit: lux

Measured and calibrated lux reading

### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2
> - Mode: R-
> - Type: Enumeration

Physical button readout sensor


### Sensor CO2

> - Request current value: Send 2b (hex) on lora port 2

### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2
> - Type: Boolean

NFC field present sensor (logical)


## Application Registers used (device controls)


### Register TX_POWER_RANGE

> - Request current value: Send d8 (hex) on lora port 2
Set the power index range for fast ADR, LSB = lowest, MSB = highest
Range for each is 16 (DR0/Max power) - 0 (regions best), mixing up
highest and lowest does not matter (firmware always use the highest of the two as the max).
There is a high impact on power consumption to turn this up (lower battery time).

> - UI:   TX Power Range
> - Mode: RW
> - Min: 0
> - Max: 65535
> - Unit: 2 bytes


## Meta-Information for this application version



### Application CRC (decimal)

 > 4056726319

### Application Sensor Mask (hex)

 > f3972

### Map Data for vsm-translator-open-source

```
M output batteryPercent 160 0xa0  1
M input powerIndexFilterFactorUp 161 0xa1  1
M input powerIndexFilterFactorDown 162 0xa2  1
M input maxPowerIndex 163 0xa3  1
M output lux 176 0xb0  1
M output averageLux 144 0x90  1
M input luxTresholdPercent 177 0xb1  1
M input averageLuxIntervalMinutes 164 0xa4  1
M output air_run_in_status 165 0xa5  1
M output air_stab_status 166 0xa6  1
M output air_iaq_accuracy 167 0xa7  1
M output air_iaq 184 0xb8  1
M output air_co2 185 0xb9  1
M output air_pressure 186 0xba  0.01
M output air_static_iaq 187 0xbb  1
M output air_temperature 178 0xb2  0.01
M output air_humidity 145 0x91  0.01
M input air_interval_minutes 179 0xb3  1
M output air_equivalent_co2 188 0xbc  1
C 4056726319 # 0xf1ccbb2f

```

