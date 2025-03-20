
# Application Lifefinder-wifi

## Temp alarm and humidity reporting for LifeFinder units


Minutely check temperature and send alarm if temperature is above or below the set levels


Daily check and uplink humidity value if it has changed more than the set threshold


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


Battery voltage is read daily and uplinked if the battery voltage changes by more than 10mV.

## LifeFinder Alarm module


Loads alarm time and/or trace time from the backup register if anything is saved there


Dynamically handles resend time and resend count based on the state of the device


Allows for changing the alarm blink style from server to indicate on the device that the alarm has been acknowledged by the server


Button enables and disables the alarm state. Button press is also indicated by the LED and alarm LEDs blinking in a specific pattern.


Setting quickAlarm to true will make the device enter alarm state directly when the button is pressed.


While alarm is active, the alarmTime will be uplinked minutely. Alarm is disabled after maxAlarmMinutes is reached.


While trace mode is active, the traceTime will be uplinked minutely. Trace mode is disabled after maxTraceMinutes is reached.


Small LED will blink yellow twice every minute to indicate that the device is in trace mode.


Device rejoins the network minutely while in trace or alarm mode, and hourly if not.


Optionally if nfcDisablesAlarm is set to true, the alarm will be disabled when an NFC field is detected. Device will report that the alarm has been disabled by an NFC field.


A trigger uplink will be sent every traceTriggerMinutes in order to accept downlinks to enable trace mode.


Weekly the accumulated time spent in alarm state will be uplinked.


Device saves the alarm time and/or trace time to the backup register. These will be loaded on start-up should the device crash or restart during alarm and/or trace.

## Alarm positioning using WiFi positioning


Channel and scan time management


A position attempt is made when the device joins the network


A position attempt is made minutely during alarm and/or trace mode


A position attempt is made periodically when positioningFreqency is set


A position attempt is made if the button is pressed


## Application Outputs


### Output alarmAccumulatedTime (confirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Unit: Minutes

Accumulated time device has spent in Alarm state in minutes since the last device restart.


### Output batteryPercent (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: % (estimated)

Estimated remaining % of battery in this unit based on measured use time and power for MCU, Radio, Sensors
Position Scans, and potential collateral power use. Uplinked weekly.


### Output humidity (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: rH

Explanation of output


### Output nfcDisabledAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean

Sent as true when the alarm is disabled by detecting an NFC field.


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


### Output traceTrigger (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean

Sent up every traceTriggerMinutes in order to accept downlinks to enable trace mode.


### Output volts (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001
> - Unit: V

Uplinked daily should the battery voltage change by more than 10mV.


## Application Inputs (settings)


### Input alarmResendTime (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a7 (hex) on lora port 2
> - Update value to 1: Send a7 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Alarm Resend Time
> - Unit: Seconds
> - Min: 1
> - Max: 127
> - Default: 45

How many seconds between resend attempts during an alarm. First 5 resends follows standard resend time.


### Input alarmResendsBeforeUnjoin (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b5 (hex) on lora port 2
> - Update value to 1: Send b5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Amount of Resends Before Unjoin During Alarm
> - Unit: Integer
> - Min: 1
> - Max: 32767
> - Default: 120

How many resends the device will attempt before unjoining the network during an alarm.


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
> - Default: 120

How long the device remains in alarm state before going back to rest.


### Input maxTraceMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Max Trace State Time
> - Unit: Minutes
> - Min: 0
> - Max: 127
> - Default: 120

How long the device remains in trace state before going back to rest.


### Input nfcDisablesAlarm (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a9 (hex) on lora port 2
> - Update value to 1: Send a9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: NFC Touch Alarm Disable
> - Unit: Boolean
> - Min: 0
> - Max: 1
> - Default: 1

While set to true, the device will disable the alarm when detecting an NFC field.


### Input positioningFreqency (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send aa (hex) on lora port 2
> - Update value to 1: Send aa 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Positioning Frequency
> - Unit: Minutes
> - Min: 0
> - Max: 127
> - Default: 0 (Off)

Periodic positioning interval when device is not in alarm state.


### Input quickAlarm (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a8 (hex) on lora port 2
> - Update value to 1: Send a8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Enable Quick Alarm
> - Unit: Boolean
> - Min: 0
> - Max: 1
> - Default: 0

While set to true, the device will enter alarm state directly when the button is pressed.


### Input resendsBeforeUnjoin (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Amount of Resends Before Unjoin
> - Unit: Integer
> - Min: 1
> - Max: 127
> - Default: 40

How many resends the device will attempt before unjoining the network.


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


### Input traceTriggerMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Trace Mode Trigger Uplink Minutes
> - Unit: Minutes
> - Min: 0
> - Max: 127
> - Default: 1

How often the device sends uplinks in order to accept downlinks to enable trace mode.


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


### Sensor VOLTAGE

> - Request current value: Send 0a (hex) on lora port 2
> - Unit: mV (milliVolts)

Measured voltage on the board.

## Application Registers used (device controls)


### Register LINKCHECK_TIME

> - Request current value: Send d0 (hex) on lora port 2
> - UI:   Downlink Timeout
> - Mode: RW
> - Unit: Seconds
> - Min: 300
> - Max: 2592000
> - Default: 86400
Once 80% of this time has passed, the device will make all messages confirmed until it gets a downlink.
Should this time pass without the device hearing a confirmed response, it will go to unjoined state.
In the unjoined state the applications specified rejoin method will be used.


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

 > 2409062033

### Application Sensor Mask (hex)

 > 532

### Map Data for vsm-translator-open-source

```
M output temp 146 0x92  0.01
M output tempAlarm 128 0x80  1
M output humidity 176 0xb0  0.01
M input humidityThreshold 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input tempAlarmLowLevel 160 0xa0  1
M input tempAlarmHighLevel 161 0xa1  1
M output batteryPercent 162 0xa2  1
M output volts 179 0xb3  0.001
M output alarmTime 144 0x90  1
M output traceTime 145 0x91  1
M output nfcDisabledAlarm 129 0x81  1
M output alarmAccumulatedTime 152 0x98  1
M output traceTrigger 130 0x82  1
M input maxAlarmMinutes 180 0xb4  1
M input maxTraceMinutes 163 0xa3  1
M input traceTriggerMinutes 165 0xa5  1
M input alarmResendsBeforeUnjoin 181 0xb5  1
M input resendsBeforeUnjoin 166 0xa6  1
M input alarmResendTime 167 0xa7  1
M input quickAlarm 168 0xa8  1
M input nfcDisablesAlarm 169 0xa9  1
M input alarmAck 164 0xa4  1
M input positioningFreqency 170 0xaa  1
M input scanTimeMs 182 0xb6  1
M input limitedScanChannels 184 0xb8  1

```

