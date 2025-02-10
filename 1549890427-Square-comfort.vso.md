
# Application Square-comfort

The comfort application reads temperature and humidity values on regular intervals and sends updates when values change more than a set threshold value.

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
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
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

### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
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
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
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
no temperature report will be generated (saves battery and radio air time).


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

 > 1549890427

### Application Sensor Mask (hex)

 > 132

### Map Data for vsm-translator-open-source

```
M input roamNetworkCount 160 0xa0  1
M output batteryPercent 161 0xa1  1
M output temp 176 0xb0  0.01
M output averageTemp 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input averageTempHysteresis 162 0xa2  0.1
M input averageTempIntervalMinutes 163 0xa3  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 164 0xa4  1
M input tempAlarmHighLevel 165 0xa5  1
M output humidity 179 0xb3  0.01
M output averageHumidity 144 0x90  0.01
M input humidityTreshold 180 0xb4  0.01
M input averageHumidityIntervalMinutes 166 0xa6  1

```

