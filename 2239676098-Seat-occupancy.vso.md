
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


The application enables port forwardning between radar module and LoRaWan for control of the radar module.

The application enables the device to start on NFC field.


Occupancy


Notify Radar when NFC field is activated (to enable BLE).


Any NFC field can be used to trigger joining the device.


Send battery voltage


## Daily Rejoin Module

Should the device not be joined, it will try to rejoin on 24hr interval.


## Application Outputs


### Output amplitude (confirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Unit: Radar echo amplitude unit

The amplitude value reported by the radar

### Output distance (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: m (Meters)

The distance value reported by the radar
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

Some radar methods may report a object detected value, typically 1 if object is detected, or 0 if occupancy or empty seat detected.


### Output occupied (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean

Some radar methods may report a occupied value, typically 1 if occupancy is detected, or 0 if occupancy is not detected.


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

## Application Inputs (settings)


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

## Application Sensors (logical sensors)


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

 > 2239676098

### Application Sensor Mask (hex)

 > 100

### Map Data for vsm-translator-open-source

```
M input roamNetworkCount 160 0xa0  1
M input powerIndexFilterFactor 161 0xa1  1
M input maxPowerIndex 162 0xa2  1
M output occupied 128 0x80  1
M output object 129 0x81  1
M output amplitude 144 0x90  1
M output distance 145 0x91  0.01
M output amplitude2 146 0x92  1
M output distance2 147 0x93  0.01
M input debugLevel 163 0xa3  1
M output state 176 0xb0  1
M output nfcContactCount 152 0x98  1
M output radarVoltage_V 177 0xb1  0.001

```

