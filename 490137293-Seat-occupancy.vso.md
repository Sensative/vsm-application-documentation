
# Application Seat-occupancy


## Roaming module

Enable the device to roam through multiple LoRaWan networks, but changing the last digit of the NwkKey to the
currently set network.


Every 24 hours, the join network is reset to 0 (default)


Should the device enter unjoined state and there are more networks to try, the device will try the next network.


## ADR dampening and limiting module

Adaptive LoRaWan data rate dampening and limiter module, allows to limit both adaptability rate and worst data rate / output power.
This is intended for fixed-mount devices where radio conditions are not expected to change rapidly.


## Radar Application

This application integrates with the acconeer/sweiot radar solution. It provides lorawan transfer of radar data
with certain thresholds (hysteresis) filters to reduce the LoRaWan traffic as necessary for any given application.


The application enables port forwarding between radar module and LoRaWan for control of the radar module.

The application enables the device to start on NFC field.


Send Occupancy, Object, optional State, Distance and Amplitude values


Limit time we are in debugLevel >= 2


Notify Radar when NFC field is activated (to enable BLE).


Any NFC field can be used to trigger joining the device.


Turn on Radar when we get joined


Turn off Radar when we are not joined anymore


Retry join after timeBetweenJoinAttemts minutes


ReJoin after timeBeforeUnjoin seconds without any RX


Limit Resend
Note, this will also limit time for first report after joined if there is anything in sendqueue


Send battery voltage


Send Temperature (if enabled)


## Daily Rejoin Module

Should the device not be joined, it will try to rejoin on 24hr interval.


## Application Outputs


### Output amplitude (confirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Unit: Radar echo amplitude unit

In debug mode, amplitude value reported by the radar

### Output amplitude2 (confirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Unit: Radar echo amplitude unit

In debug mode, amplitude value reported by the radar in seconad zone

### Output distance (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: m (Meters)

In debug mode, distance value reported by the radar
Unit of this is meters, resolution is 0.01 m.

### Output distance2 (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: m (Meters)

In debug mode, distance value reported by the radar in second zone
Unit of this is meters, resolution is 0.01 m.

### Output nfcContactCount (confirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Unit: Integer
> - Min: 0
> - Max: 2^30

Number of contacts made through NFC with this device. Used to force the unit
to send an uplink even if radar is turned off.


### Output object (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean

Advanced seating radar method report a object detected.


### Output occupied (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean

Advanced seating radar method report if seat is occupied.


### Output radarVoltage_V (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001
> - Unit: V
> - Min: 0
> - Max: 3.6

System voltage as measured during radar scan. This is reported on 24h interval to give indication
of battery status. Should the voltage drop significantly from the nominal voltage over time (see
product manual), it may indicate either a cold (or very hot) temperature - see temperature reports.
If temperature is normal, and voltage stays low, consider exchanging the battery.

Some fluctuations in voltage is normal in operation, do not react to a single or few offset readings.

### Output state (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Unit: Integer
> - Min: 0
> - Max: 10

In debug mode, Radar application internal state


### Output temp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: C

The temperature uploaded with a resolution of 0.01 C
Accuracy is limited by accuracy of temperature sensor in the product. Refer to datasheet.

## Application Inputs (settings)


### Input batteryReportInterval (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Interval time (h) between battery voltage reports
> - Unit: Integer
> - Default: 30h

This value is randomized at this value +- 50% to avoid potential repeat collisions

### Input debugLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Debug level
> - Values:
> -- 0 = No debug
> -- 1 = Output Distance and Amplitude on occupied/object changed
> -- 2 = Output Distance and Amplitude on occupied/object/state changed
> - Default: 1
> - Min: 0
> - Max: 2


### Input maxPowerIndex (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Max Power Index
> - Unit: LoraWan power index (0-16)
> - Min: 0
> - Max: 16
> - Default: 14

maximum power index to use for LoRaWan traffic, including join. Default setting disables DR0

### Input maxResendWaitTime (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b4 (hex) on lora port 2
> - Update value to 1: Send b4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Max time (s) between ReSend tries
> - Unit: Integer
> - Default: 86400



### Input minResendWaitTime (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b3 (hex) on lora port 2
> - Update value to 1: Send b3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Min time (s) between ReSend tries
> - Unit: Integer
> - Default: 80



### Input powerIndexFilterFactor (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: LoRaWan power filter factor
> - Unit: Integer
> - Min: 1
> - Max: 50
> - Default: 3

Low pass filter factor. 1 = no low-pass filter. 2 = filter factor 1 (fast) ... 10 = very slow.
When the built-in ADR function propose a new power index, this filter factor is employed in a low pass filter.
If the filter value is set to 1 the algorithm will use its proposed new value (if below or at max).

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

### Input temperatureReportInterval (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Interval
> - Unit: Minutes
> - Min: 0
> - Max: 127
> - Default: 0 (Off)



### Input temperatureUserCalibration (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b5 (hex) on lora port 2
> - Update value to 1: Send b5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Calibration
> - Unit: Minutes
> - Min: -10.0
> - Max: +20.0
> - Default: 0



### Input timeBeforeUnjoin (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b2 (hex) on lora port 2
> - Update value to 1: Send b2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Time (h) from last RX Before Unjoin
> - Unit: Integer
> - Default: 168 (7 days)



### Input timeBetweenJoinAttemts (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Time (minutes) between join retries
> - Unit: Integer
> - Default: 1440 (24h)



## Application Sensors (logical sensors)


### Sensor AIR_TEMPERATURE

> - Request current value: Send 04 (hex) on lora port 2
> - Unit: CentiCelcius

Air temperature sensor (logical)

### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2
> - Type: Boolean

NFC field present sensor (logical)


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

 > 490137293

### Application Sensor Mask (hex)

 > 110

### Map Data for vsm-translator-open-source

```
M input roamNetworkCount 160 0xa0  1
M input powerIndexFilterFactor 161 0xa1  1
M input maxPowerIndex 162 0xa2  1
M output occupied 128 0x80  1
M output object 129 0x81  1
M output radarVoltage_V 176 0xb0  0.001
M output nfcContactCount 152 0x98  1
M output temp 177 0xb1  0.01
M input timeBetweenJoinAttemts 184 0xb8  1
M input timeBeforeUnjoin 178 0xb2  1
M input minResendWaitTime 179 0xb3  1
M input maxResendWaitTime 180 0xb4  1
M input batteryReportInterval 163 0xa3  1
M input temperatureReportInterval 164 0xa4  1
M input temperatureUserCalibration 181 0xb5  0.01
M input debugLevel 165 0xa5  1
M output amplitude 144 0x90  1
M output distance 145 0x91  0.01
M output amplitude2 146 0x92  1
M output distance2 147 0x93  0.01
M output state 182 0xb6  1

```

