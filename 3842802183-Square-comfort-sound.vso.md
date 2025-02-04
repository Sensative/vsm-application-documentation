
# Application Square-comfort-sound

Experience the power of intelligent sound detection with Square-comfort-sound. The device captures precise sound levels, enabling real-time monitoring and alerts when noise thresholds are exceeded. Whether you need to track ambient sound for environmental control or detect sudden noise spikes, our solution ensures accuracy and reliability. With customizable thresholds and alarms, the device adapts to your specific needs, making it ideal for both indoor and outdoor use. Enjoy seamless integration with LoRaWAN networks, long-lasting battery life, and flexible reporting intervals. Elevate your sound monitoring with Square-comfort-sound.

## Roaming module

Enable the device to roam through multiple LoRaWan networks, but changing the last digit of the NwkKey to the
currently set network.


Every 24 hours, the join network is reset to 0 (default)


Should the device enter unjoined state and there are more networks to try, the device will try the next network.

## Slow Tracker Module

This module enables slow tracking through WIFI scanning or GNSS scans (if device supports GNSS scanning).
For proper functioning of GNSS enabled devices, the GNSS almanac and device time needs to be kept up-to-date,
for instance through NFC application or through enabling the vsm-mqtt-client (https:


When the button is pressed, a wifi scan will be done.


Daily when the device is joined, it will attempt a wifi scan.


Weekly, when the device is joined, it will attempt a GNSS scan (provided the device supports GNSS scanning).


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.

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

## Daily Rejoin Module

Should the device not be joined, it will try to rejoin on 24hr interval.


The device will do a join attempt if it is not joined and if button is pressed.


An NFC field can be applied to manually trigger a join attempt

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
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Humidity Interval
> - Unit: Minutes
> - Min: 1
> - Max: 127
> - Default: 60

Interval between the averageHumidity calculations.


### Input averageTempIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Interval
> - Unit: Minutes
> - Min: 2
> - Max: 127
> - Default: 60

The interval at which average temperature is uploaded (provided that it has changed more than tempHysteresis).


### Input humidityTreshold (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b4 (hex) on lora port 2
> - Update value to 1: Send b4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Humidity Threshold
> - Unit: %
> - Default: 2
> - Min: 0.1
> - Max: 100 (practically disabled when > 100%)

The number of percent change required for an update over LoRaWan of humidity and/or averageHumidity.


### Input roamNetworkCount (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Roaming Network Count
> - Unit: Integer
> - Min: 1
> - Max: 15
> - Default: 1

The number of LoRaWan network identities this device shall have.
In case the device needs to rejoin, it will iteratively attempt join in priority order from 0 to this value.

> The device replaces the last digit of the network key with hexadecimal value 0-F when joining.
> Setting this to more than 1 incurs extra time and power consumption when joining.

### Input soundAlarmTimeoutMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a9 (hex) on lora port 2
> - Update value to 1: Send a9 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a8 (hex) on lora port 2
> - Update value to 1: Send a8 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a7 (hex) on lora port 2
> - Update value to 1: Send a7 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send b2 (hex) on lora port 2
> - Update value to 1: Send b2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Threshold
> - Unit: C
> - Min: 0.1
> - Max: 127
> - Default: 0.5

The hysteresis for temperature readings. If temperature changes lower than this value are detected
no report will be generated (saves battery and radio air time).


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


### Register GPS_TIME_MAX_AGE

> - Request current value: Send cd (hex) on lora port 2
> - UI:   Device Time Max Age
> - Mode: RW
> - Unit: Seconds
> - Default: 0
> - Min: 0
> - Max: 4294967295
Once this maximum age has passed the device will no longer trust its GPS_TIME and GNSS scans become autonomous.
Also, it will start emitting DEVICE_TIME requests on the LoRaWan network once 80% of this time has passed.
Typically the clock drift is a few seconds per 24 hrs. Gps time should be correct within 30s for good assisted scans.
Outdoor use tends to increase clock drift.


## Meta-Information for this application version



### Application CRC (decimal)

 > 3842802183

### Application Sensor Mask (hex)

 > 200132

### Map Data for vsm-translator-open-source

```
M input roamNetworkCount 160 0xa0  1
M output batteryPercent 161 0xa1  1
M output temp 176 0xb0  0.01
M output averageTemp 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input averageTempIntervalMinutes 162 0xa2  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 163 0xa3  1
M input tempAlarmHighLevel 164 0xa4  1
M output humidity 179 0xb3  0.01
M output averageHumidity 144 0x90  0.01
M input humidityTreshold 180 0xb4  0.01
M input averageHumidityIntervalMinutes 165 0xa5  1
M output soundLevel 181 0xb5  0.1
M input soundThreshold 166 0xa6  1
M input soundMinLevel 167 0xa7  1
M input soundAvgMinutes 168 0xa8  1
M output soundAlarm 129 0x81  1
M input soundAlarmTimeoutMinutes 169 0xa9  1
M output soundAvgMax 184 0xb8  0.1

```

