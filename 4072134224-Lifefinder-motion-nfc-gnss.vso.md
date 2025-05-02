
# Application Lifefinder-motion-nfc-gnss

## Temp alarm and humidity reporting for LifeFinder units


Minutely check temperature and send alarm if temperature is above or below the set levels


Daily check and uplink humidity value if it has changed more than the set threshold


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


Battery voltage is read daily and uplinked if the battery voltage changes by more than 10mV.

## NFC field Activated deviceActive trigger for lifefinder-timekeeper-motion.vsr


BACKUP register is read on startup, resuming active time in the event of a device crash or restart.


NFC field detection enables and disables deviceActive. Active is indicated by one LED flash pattern while inactive is indicated by two flashes.


Device counts the minutes spent in active mode. If the device is active for longer than activeTimeMaxMinutes, it is set to inactive.


Button enables and disables the alarm state. Button press is also indicated by the LED and alarm LEDs blinking in a specific pattern.


While alarm is active, the alarmTime will be uplinked minutely. Alarm is disabled after maxAlarmMinutes is reached.


In alarm state the device will attempt to rejoin the network minutely.
While in active state, device will attempt to join the network every 15 minutes.
If the device is not active or in alarm, it will attempt to join every 24 hours.


Current time spent in active mode is saved to the BACKUP register to be read on startup in the event of a device crash or restart.

## Motion tracking module for lifefinder timekeeper application


Motion thresholds are limited to the range of 5 to 10000 mm/s2


Keeps track of the 3D accelerometer state and updates the motion state accordingly.
Motion thesholds are dynamically adjusted based on the current state.


The device accumulates time in moving and stationary states. The accumulated time is uplinked hourly and when the device goes to inactive state.
3D accelerometer is switched off when the device is inactive, then back on when the device is active again.

## Positioning using GNSS for lifefinder-timekeeper-nfc-motion.vsr


Device will perform a position when the device is active and stops moving


Device will position using WiFi every movingPositionMinutes while moving.


Device will position using WiFi every stationaryPositionMinutes while stationary.


Try a position every minute when the device is in alarm state


Device will position every positioningFreqency minutes while not in alarm.


Device will position when the button is pressed


## Application Outputs


### Output accumulatedMovingTime (confirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Unit: Minutes

Amount of accumulated time in moving state. Uplinked hourly and when device goes to inactive state.


### Output accumulatedStationaryTime (confirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Unit: Minutes

Amount of accumulated time in stationary state. Uplinked hourly and when device goes to inactive state.


### Output batteryPercent (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: % (estimated)

Estimated remaining % of battery in this unit based on measured use time and power for MCU, Radio, Sensors
Position Scans, and potential collateral power use. Uplinked weekly.


### Output deviceActive (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean

Uplinked as 1 if device is active and positioning. 0 when the device is idle.


### Output humidity (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: rH

Explanation of output


### Output temp (confirmed)

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


### Output volts (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001
> - Unit: V

Uplinked daily should the battery voltage change by more than 10mV.


## Application Inputs (settings)


### Input activeTimeMaxMinutes (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Active Time Maximum
> - Unit: Minutes
> - Min: 0
> - Max: 32767
> - Default: 600 (10 hours)

Explanation of input


### Input humidityThreshold (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b1 (hex) on lora port 2
> - Update value to 1: Send b1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Humidity Threshold
> - Unit: rH
> - Min: 0
> - Max: 100
> - Default: 20

Amount humidity must change for a new humidity value to be reported.


### Input maxAlarmMinutes (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b4 (hex) on lora port 2
> - Update value to 1: Send b4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Max Alarm State Time
> - Unit: Minutes
> - Min: 0
> - Max: 32767
> - Default: 30

How long the device remains in alarm state before going back to rest.


### Input movingMotionThreshold_mm_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b6 (hex) on lora port 2
> - Update value to 1: Send b6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Moving Threshold
> - Unit: mm/s2
> - Min: 5
> - Max: 10000
> - Default: 30
The accelerometer threshold to use for redetection of motion while currently in motion. **If set too low it means the device will
believe it is in constant motion and will not trigger position scans when still** It is recommended
to start from high values and then decrease should sensitivity be too low.


### Input movingPositionMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Moving Position Inverval
> - Unit: Minutes
> - Min: 0
> - Max: 127
> - Default: 1

Amount of time in minutes between position scans when the device is moving


### Input positioningFreqency (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Periodic Positioning Frequency
> - Unit: Minutes
> - Min: 0
> - Max: 127
> - Default: 0

Periodic positioning frequency in minutes while not in alarm. If set to 0, no periodic positioning will be done.


### Input stationaryPositionMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Stationary Position Inverval
> - Unit: Minutes
> - Min: 0
> - Max: 127
> - Default: 30

Amount of time in minutes between position scans when the device is stationary


### Input stillMotionThreshold_mm_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b5 (hex) on lora port 2
> - Update value to 1: Send b5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Still Threshold
> - Unit: mm/s2
> - Min: 5
> - Max: 10000
> - Default: 50
The accelerometer threshold to use for detection of motion while stationary. **If set too low it means the device will
believe it is in constant motion and will not trigger position scans when still** It is recommended
to start from high values and then decrease should sensitivity be too low.


### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature High Alarm Level
> - Unit: C
> - Min: -127
> - Max: 127
> - Default: 60

If measured temperature exceeds the set level an alarm along with the temperature is sent. Should not be set less than tempAlarmLowLevel.


### Input tempAlarmLowLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Low Alarm Level
> - Unit: C
> - Min: -127
> - Max: 127
> - Default: 2

If measured temperature is less than the set level an alarm along with the temperature is sent. Should not be set higher than tempAlarmHighLevel.


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

Amount temperature must change for a new temperature value to be reported while in a temperature alarm state.


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


### Sensor MOTION

> - Request current value: Send 16 (hex) on lora port 2
> - Type: Enumeration

Motion sensor reading, one of
- 0 : Unknown
- 1 : Still (less than register MOTION_CONTROL mm/s2 acceleration change detected through last minute)
- 2 : Moving (more than register MOTION_CONTROL mm/s2 acceleration change detected through last minute)
- 3 : Shocked (more than 4m/s2 change in acceleration detected through last minute)

### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2
> - Type: Boolean

NFC field present sensor (logical)


### Sensor VOLTAGE

> - Request current value: Send 0a (hex) on lora port 2
> - Unit: mV (milliVolts)

Measured voltage on the board.

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

 > 4072134224

### Application Sensor Mask (hex)

 > 400532

### Map Data for vsm-translator-open-source

```
M output temp 145 0x91  0.01
M output tempAlarm 128 0x80  1
M output humidity 176 0xb0  0.01
M input humidityThreshold 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input tempAlarmLowLevel 160 0xa0  1
M input tempAlarmHighLevel 161 0xa1  1
M output batteryPercent 162 0xa2  1
M output volts 179 0xb3  0.001
M output deviceActive 129 0x81  1
M output alarmTime 144 0x90  1
M input activeTimeMaxMinutes 184 0xb8  1
M input alarmAck 164 0xa4  1
M input maxAlarmMinutes 180 0xb4  1
M input stillMotionThreshold_mm_s2 181 0xb5  1
M input movingMotionThreshold_mm_s2 182 0xb6  1
M input stationaryPositionMinutes 163 0xa3  1
M input movingPositionMinutes 165 0xa5  1
M output accumulatedStationaryTime 146 0x92  1
M output accumulatedMovingTime 147 0x93  1
M input positioningFreqency 166 0xa6  1

```

