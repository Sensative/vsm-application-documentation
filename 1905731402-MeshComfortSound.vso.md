
# Application MeshComfortSound


## Generic RutioMesh Module

Generic mesh module allowing both lora wan bridging, network extension or
(with a setting) the device to behave as a leaf only module (which is same as a regular
lorawan module should the device be joined to lorawan network).


## ADR dampening and limiting module

Adaptive LoRaWan data rate dampening and limiter module, allows to limit both adaptability rate and worst data rate / output power.
This is intended for fixed-mount devices where radio conditions are not expected to change rapidly.

Module for package loss / device restart detection
## Temperature Sensing and Reporting Module


When the sensor detects an air temperature which has changed from the previous uploaded temperature by more than
the set tempHysteresis (threshold) it will upload a new temp reading. The temperatures are polled every minute and then processed.


When a temperature is detected which exceeds the tempAlarmHighLevel the tempAlarm will be set to 1.


When a temperature is detected which is below the tempAlarmLowLevel the tempAlarm will be set to -1.


When the temperature is between the low level


When averageTempIntervalMinutes have passed, and if the average temperature has changed more than tempHysteresis (threshold) degrees C,
the sensor will upload a new averageTemp value.


Every minute, the unit will take a humidity sample.

At an interval of averageHumidityIntervalMinutes the unit will recalculate the average humidity value.

The device will do a join attempt if it is not joined and if button is pressed.


An NFC field can be applied to manually trigger a join attempt


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


## Daily Rejoin Module

Should the device not be joined, it will try to rejoin on 24hr interval.


The device will always do a LoRaWan join attempt when powered on (which also includes after a restart)

The unit will update sound levels only when it is joined.

## Application Outputs


### Output averageHumidity (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: %RH

Average humidity as measured during the last averageHumidityIntervalMinutes.
The measure is sent if the measured average has changed more than humidityTreshold %.


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


### Output hours (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
The number of hours the device has been on since activated (restarted).

### Output humidity (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: %RH
> - Note: Should the humidity exceed 100% (e.g. dew) following measurements may be sigificantly
affected until the device has dried.

Current humidity, in %RH. Transferred when the measured value has changed more
than humidityThreshold %.


### Output soundAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: dB
> - Default: 0

When a sound threshold has been set (e.g. interrupt driven) and the level exceeds soundMinLevel, this
alarm is set to true, else it is set to false. Disabled when sound-threshold is zero, and instead the
soundLevel reporting is activated.

### Output soundAvgMax (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 0.1
> - Unit: dB (RMS)
> - Min: 45 dB
> - Max: 92 dB

Peak measured sound level in the average over soundAvgMinutes.
Disabled when sound threshold is non-zero (in which case the soundAlarm is instead activated).

### Output soundLevel (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.1
> - Unit: dB (RMS)
> - Min: 45 dB
> - Max: 92 dB

Sampled sound level average over soundAvgMinutes.
Disabled when sound threshold is non-zero (in which case the soundAlarm is instead activated).

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


## Application Inputs (settings)


### Input averageHumidityIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a9 (hex) on lora port 2
> - Update value to 1: Send a9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Humidity Interval
> - Unit: Minutes
> - Min: 1
> - Max: 127
> - Default: 60

Interval between the averageHumidity calculations.


### Input averageTempHysteresis (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 0.1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Average Temperature Threshold
> - Unit: C
> - Min: 0.0
> - Max: 12.7
> - Default: 0.1

The hysteresis for temperature readings. If the average temperature changes less than this value
no report will be generated (saves battery and radio air time).


### Input averageTempIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Average Temperature Interval
> - Unit: Minutes
> - Min: 2
> - Max: 127
> - Default: 60

The interval at which average temperature is uploaded provided that it has changed more than the average temperature threshold (hysteresis).


### Input humidityTreshold (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b6 (hex) on lora port 2
> - Update value to 1: Send b6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Humidity Threshold
> - Unit: %
> - Default: 2
> - Min: 0.1
> - Max: 100 (practically disabled when > 100%)

The number of percent change required for an update over LoRaWan of humidity and/or averageHumidity.


### Input maxPowerIndex (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Max Power Index
> - Unit: LoraWan power index (0-16)
> - Min: 0
> - Max: 16
> - Default: 16

maximum power index to use for LoRaWan traffic, including join. Default setting disables DR0

### Input meshEnableDownside (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Enable this node as extender

> - UI: Enable Mesh Downside (Extension)
> - Unit: boolean
> - Min: 0
> - Max: 1
> - Default: 0

### Input meshEnableUpside (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Enable this node to join a mesh network (when not joined to LoRaWan network)

> - UI: Enable Mesh Upside (Synchronization)
> - Unit: boolean
> - Min: 0
> - Max: 1
> - Default: 1

### Input meshSyncInterval_minutes (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b0 (hex) on lora port 2
> - Update value to 1: Send b0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Synchronization interval

Synchronization is a relatively expensive operation, so we avoid doing this frequently
should the unit fall outside the mesh. It is recommended to set this to longer times in
in environments that are relatively static.

> - UI: Mesh Sync Interval
> - Unit: minutes
> - Min: 1
> - Max: 65535
> - Default: 120

### Input powerIndexFilterFactorDown (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: LoRaWan power filter factor up
> - Unit: Integer
> - Min: 1
> - Max: 50
> - Default: 3

Low pass filter factor. 1 = no low-pass filter. 2 = filter factor 1 (fast) ... 10 = very slow.
When the built-in ADR function propose a new slower power index, this filter factor is employed in a low pass filter.
If the filter value is set to 1 the algorithm will use its proposed new value (if below or at max).

### Input soundAlarmTimeoutMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send af (hex) on lora port 2
> - Update value to 1: Send af 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Sound Alarm Timeout
> - Unit: minutes
> - Default: 5
> - Max: 127
> - Min: 2
When a sound threshold has been set (e.g. interrupt driven) and the level exceeds soundMinLevel, the
sound alarm is set and then held active for approximately this number of minutes (+-60s). The randomization
is there in order to avoid synchronous sending of 0 in case multiple sensors picked up the same sound at the same time.

On activation of the alarm it might still generate conflicts over the air (e.g. multiple sensors hearing the same sound
at the same time may collide in the air).

During this time the sound alarm will not retrigger or reset.

### Input soundAvgMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send ae (hex) on lora port 2
> - Update value to 1: Send ae 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Sound Average Time
> - Unit: Minutes
> - Default: 15
> - Min: 1
> - Max: 127
The number of minutes between average sound level calculation.

### Input soundMinLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send ad (hex) on lora port 2
> - Update value to 1: Send ad 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Minimum Sound Level
> - Unit: dB (RMS)
> - Min: 45 dB
> - Max: 92 dB
> - Default: 45 dB

This is the minimum base level for the wakeup in interrupt driven mode.
See soundThreshold for more information.


### Input soundThreshold (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send ac (hex) on lora port 2
> - Update value to 1: Send ac 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Sound Threshold
> - Unit: dB (RMS)
> - Min: 0
> - Max: 18
> - Or set to 0 for internally polled sensor operation
> - Default: 0

This can be set to enable a wake-on-sound operation mode, where the threshold value
will make the device wake up automatically when the sound level changes more than the
set dB value (and above the soundMinLevel). This has the advantage of detecting sudden sounds, but has the disadvantage
of an increased power consumption. The default 0 is recommended in most applications.
The effective range is 6-18dB


### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a8 (hex) on lora port 2
> - Update value to 1: Send a8 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a7 (hex) on lora port 2
> - Update value to 1: Send a7 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send b4 (hex) on lora port 2
> - Update value to 1: Send b4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Threshold
> - Unit: C
> - Min: 0.1
> - Max: 127
> - Default: 0.5

The hysteresis for temperature readings. If temperature changes lower than this value are detected
no temperature report will be generated (saves battery and radio air time).


### Input wifiScanInterval_h (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send ab (hex) on lora port 2
> - Update value to 1: Send ab 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Number of hours between wifi scans.

> - Min: 0
> - Max: 127
> - Default: 0
> - Unit: hours
> - UI: Wifi Scan Interval

When set to 0 or less, the interval scanning is disabled.


## Application Sensors (logical sensors)


### Sensor AIR_HUMIDITY

> - Request current value: Send 05 (hex) on lora port 2
> - Unit: CentiRH%

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


### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2
> - Type: Boolean

NFC field present sensor (logical)


### Sensor SOUND

> - Request current value: Send 15 (hex) on lora port 2


Sound sensor

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

 > 1905731402

### Application Sensor Mask (hex)

 > 200132

### Map Data for vsm-translator-open-source

```
M input meshSyncInterval_minutes 176 0xb0  1
M input meshEnableUpside 160 0xa0  1
M input meshEnableDownside 161 0xa1  1
M input powerIndexFilterFactorUp 162 0xa2  1
M input powerIndexFilterFactorDown 163 0xa3  1
M input maxPowerIndex 164 0xa4  1
M output hours 177 0xb1  1
M output temp 178 0xb2  0.01
M output averageTemp 179 0xb3  0.01
M input tempHysteresis 180 0xb4  0.01
M input averageTempHysteresis 165 0xa5  0.1
M input averageTempIntervalMinutes 166 0xa6  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 167 0xa7  1
M input tempAlarmHighLevel 168 0xa8  1
M output humidity 181 0xb5  0.01
M output averageHumidity 144 0x90  0.01
M input humidityTreshold 182 0xb6  0.01
M input averageHumidityIntervalMinutes 169 0xa9  1
M output batteryPercent 170 0xaa  1
M input wifiScanInterval_h 171 0xab  1
M output soundLevel 183 0xb7  0.1
M input soundThreshold 172 0xac  1
M input soundMinLevel 173 0xad  1
M input soundAvgMinutes 174 0xae  1
M output soundAlarm 129 0x81  1
M input soundAlarmTimeoutMinutes 175 0xaf  1
M output soundAvgMax 184 0xb8  0.1

```

