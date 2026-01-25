
# Application Lifefinder-beacon-nfc


## Application Outputs


### Output espStatus (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean

When if no contact with the ESP32 for more than espStatusMinutes, this will be uplinked as 1.


### Output hum (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: rH

Relative humidity in percentage


### Output humAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Enumeration
> -- No alarm: 0
> -- High alarm: 1
> -- Low alarm: -1

Humidity alarm state sent when rH is above or below the set levels.


### Output humAverage (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: rH

The average humidity uploaded with a resolution 0.01% rH.


### Output serial (confirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Unit: Integer

Serial number of latest checked in device


### Output settingTrigger (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean

Uplinked during settingMode active to receive downlinks


### Output temp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: C

Temperature value uploaded while in alarm state minutely if the temperature change is above the set threshold value.


### Output tempAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Enumeration
> -- No alarm: 0
> -- High alarm: 1
> -- Low alarm: -1

Temperature alarm state sent when temperature is above or below the set levels.


### Output tempAverage (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: C

The average temperature uploaded with a resolution 0.01C.


## Application Inputs (settings)


### Input debounceSeconds (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b7 (hex) on lora port 2
> - Update value to 1: Send b7 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Debounce Seconds
> - Unit: Seconds
> - Min: 0
> - Max: 60
> - Default: 30

How many seconds before device allows the rescan of the same device. Also has a setting in the Beacon.


### Input espStatusMinutes (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b1 (hex) on lora port 2
> - Update value to 1: Send b1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: ESP32 watchdog timer
> - Unit: Minutes
> - Default: 20
> - Min: 0
> - Max: 120

Amount of minutes the Dots will wait to alert that no regular communication with the ESP32 has taken place.


### Input humAlarmHighLevel (unconfirmed)

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


### Input humAverageMeasurements (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a8 (hex) on lora port 2
> - Update value to 1: Send a8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Average Humidity Measurements
> - Unit: Measurements
> - Min: 2
> - Max: 127
> - Default: 30

The number of measurements at which average humidity is calculated and uploaded provided that it has changed more than the average humidity threshold (hysteresis).


### Input humHysteresis (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b5 (hex) on lora port 2
> - Update value to 1: Send b5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Humidity Threshold
> - Unit: %
> - Default: 2
> - Min: 0.1
> - Max: 100 (practically disabled when > 100%)

The number of percent change required for an update over LoRaWan of humidity and/or averageHumidity.


### Input limitedScanChannels (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Limited Wifi Scan Channel Mask
> - Unit: Wifi scan channel mask (binary)
> - Default: 1057 (1,6 and 11)
> - Min: 0
> - Max: 65535
The app has the option to select only certain channels for WiFi scans in the first attempts to scan, to reduce power
consumption and increase chance of finding WiFi beacons on known channels.
Should you want to scan only channel 1 and 3 you set this to binary 101, or decimal 5. Special value 0 means all channels.

### Input positioningFrequency (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a9 (hex) on lora port 2
> - Update value to 1: Send a9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Positioning Frequency
> - Unit: Minutes
> - Min: 0 (Off)
> - Max: 127
> - Default: 30

Periodic positioning interval.


### Input scanTimeMs (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b6 (hex) on lora port 2
> - Update value to 1: Send b6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Time to scan per channel
> - Unit: ms
> - Min: 100
> - Max: 1000
> - Default: 300

How long time to scan per channel in milliseconds.


### Input settingMode (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Settings Mode
> - Unit: Boolean
> - Default: 1
> - Min: 0
> - Max: 1

When set to 1, will uplink settingTrigger for settingModeTime minutes to facilitate configuration.


### Input settingModeTime (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b0 (hex) on lora port 2
> - Update value to 1: Send b0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Settings Mode Active time
> - Unit: Minutes
> - Default: 20
> - Min: 0
> - Max: 120

Amount of minutes which settingMode will be active.


### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
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
> - Default: -5

The low level for temperature alarm. Set lower than tempAlarmHighLevel or the alarm function is disabled.


### Input tempAverageMeasurements (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a7 (hex) on lora port 2
> - Update value to 1: Send a7 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Average Temperature Measurements
> - Unit: Measurements
> - Min: 2
> - Max: 127
> - Default: 30

The number of measurements at which average temperature is calculated and uploaded provided that it has changed more than the average temperature threshold (hysteresis).


### Input tempHumPollingInterval (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Measurement Interval
> - Unit: Minutes
> - Min: 0 (Off)
> - Max: 127
> - Default: 1

The interval at which temperature is measured provided.


### Input tempHysteresis (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.1
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


## Application Sensors (logical sensors)


### Sensor AIR_HUMIDITY

> - Request current value: Send 05 (hex) on lora port 2
> - Unit: CentiRH%

Air humidity sensor (logical)

### Sensor AIR_TEMPERATURE

> - Request current value: Send 04 (hex) on lora port 2
> - Unit: CentiCelcius

Air temperature sensor (logical)

## Application Registers used (device controls)


## Meta-Information for this application version



### Application CRC (decimal)

 > 1172418602

### Application Sensor Mask (hex)

 > 30

### Map Data for vsm-translator-open-source

```
M output settingTrigger 160 0xa0  1
M output espStatus 161 0xa1  1
M input settingMode 162 0xa2  1
M input settingModeTime 176 0xb0  1
M input espStatusMinutes 177 0xb1  1
M output temp 178 0xb2  0.01
M output tempAverage 144 0x90  0.01
M output hum 179 0xb3  0.01
M output humAverage 145 0x91  0.01
M output tempAlarm 128 0x80  1
M output humAlarm 129 0x81  1
M input tempHysteresis 180 0xb4  0.1
M input humHysteresis 181 0xb5  0.01
M input tempAlarmHighLevel 163 0xa3  1
M input tempAlarmLowLevel 164 0xa4  1
M input humAlarmHighLevel 165 0xa5  1
M input tempHumPollingInterval 166 0xa6  1
M input tempAverageMeasurements 167 0xa7  1
M input humAverageMeasurements 168 0xa8  1
M input positioningFrequency 169 0xa9  1
M input scanTimeMs 182 0xb6  1
M input limitedScanChannels 184 0xb8  1
M output serial 152 0x98  1
M input debounceSeconds 183 0xb7  1

```

