
# Application Digital-gpio


## Roaming module

Enable the device to roam through multiple LoRaWan networks, but changing the last digit of the NwkKey to the
currently set network.


Every 24 hours, the join network is reset to 0 (default)


Should the device enter unjoined state and there are more networks to try, the device will try the next network.

## Slow Tracker Module

This module enables slow tracking through WIFI scanning or GNSS scans.
For proper functioning the GNSS almanac and device time needs to be kept up-to-date, for instance through NFC application or through enabling the dots-mqtt-client


When the button is pressed, a wifi scan will be done.


Daily when the device is joined, it will attempt a wifi scan.


Weekly, when the device is joined, it will attempt a GNSS scan.


## Daily Rejoin Module

Should the device not be joined, it will try to rejoin on 24hr interval.


## Application Outputs


### Output detection (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

## Application Inputs (settings)


### Input activation (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send 81 (hex) on lora port 2
> - Update value to 1: Send 81 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

### Input roamNetworkCount (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Number of networks to attempt joining on in case of rejoin.
> - Min: 1
> - Max: 15
> - Default: 1

The number of LoRaWan network identities this device shall have.

> The identities are based on the network key, but replacing the last digit of the network key with hexadecimal
value 0-F. In case the device needs to rejoin, it will iteratively attempt join in priority order 0 to roamNetworkCount-1.


## Application Sensors (logical sensors)


### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2
> - Mode: R-
> - Type: Enumeration

Physical button readout sensor


## Application Registers used (device controls)


### Register APP_CONFIG

> - Request current value: Send ca (hex) on lora port 2
> - Mode: RW
> - Unit: Bit mask

Enable or disable certain functions of the device, such as power on/off behaviours.


### Register DEVICE_STATE

> - Request current value: Send c8 (hex) on lora port 2
> - Mode: RW
> - Unit: Enumeration

Current application state of the device. Can be written by application to affect the devices application state.

> - DEVICE_STATE_ACTIVE_UNJOINED (running but not joined to network)
> - DEVICE_STATE_ACTIVE_JOINING (running and attempting to join network)
> - DEVICE_STATE_ACTIVE_JOINED (running and joined to network)
> - DEVICE_STATE_ACTIVE_STREAMING (running and uploading pending data packages)
> - DEVICE_STATE_ACTIVE_ON_RADIO (running and currently working with the radio)
> - DEVICE_STATE_OFF (normally not accessible from VM but possible to write to turn off the device)
> - Others Reserved by runtime

### Register GNSS

> - Request current value: Send cc (hex) on lora port 2
> - Mode: -W
> - Type: Two * 1 bytes

Trigger GNSS scans

> - Byte 0: 0 = Attempt assisted scan if device knows GPS time and has GNSS almanac. 1 = force unassisted scan.
> - Byte 1: Minimum number of found satellites to trigger an uplink


### Register GPS_TIME_MAX_AGE

> - Request current value: Send cd (hex) on lora port 2
> - Mode: RW
> - Unit: Seconds

Read/Set GPS time maximum age. Reads 0 if no GPS time is set.
Once this maximum age has passed the device will no longer trust its GPS_TIME.
Also, it will start emitting DEVICE_TIME requests on the LoRaWan network once 80% of this time has passed.


### Register JOIN_SETTINGS

> - Request current value: Send e7 (hex) on lora port 2

### Register LED

> - Request current value: Send c9 (hex) on lora port 2
> - Mode: -W
> - Unit: Enumeration

Write in order to effect the application LED (not available on all device models)


### Register LINKCHECK_TIME

> - Request current value: Send d0 (hex) on lora port 2
> Mode: RW
> Unit: seconds

Once 80% of this time has passed, the device will make all messages confirmed until it gets a confirmation.
Should this time pass without the device hearing a confirmed response, it will go to DEVICE_STATE_ACTIVE_UNJOINED.


### Register UART

> - Request current value: Send ea (hex) on lora port 2

### Register WIFI

> - Request current value: Send da (hex) on lora port 2

## Meta-Information for this application version



### Application CRC (decimal)

 > 1044255602

### Application Sensor Mask (hex)

 > 2

### Map Data for vsm-translator-open-source

```
M input roamNetworkCount 160 0xa0  1
M output detection 128 0x80  1
M input activation 129 0x81  1

```

