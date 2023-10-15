
# Application Gnss-autonomous-test


## Application Outputs


### Output bestSatellites (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

### Output numSatellites (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output scanCount (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

## Application Inputs (settings)


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


### Register LED

> - Request current value: Send c9 (hex) on lora port 2
> - Mode: -W
> - Unit: Enumeration

Write in order to effect the application LED (not available on all device models)


### Register NOW

> - Request current value: Send c5 (hex) on lora port 2
> - Mode: R-
> - Unit: Seconds

Current time in seconds since device powered on.


### Register SATELLITE_BEST_SNR

> - Request current value: Send ec (hex) on lora port 2

### Register SATELLITE_COUNT

> - Request current value: Send ce (hex) on lora port 2
> - Mode: R-
> - Unit: integer

Reads as the number of satellites seen in the last GNSS scan.


### Register SLEEP_PERIOD

> - Request current value: Send cf (hex) on lora port 2
> - Mode: RW
> - Unit: seconds

When set to non-zero value the VM will wake up at at this interval. Make rules dependent on NOW or


### Register WIFI

> - Request current value: Send da (hex) on lora port 2

## Meta-Information for this application version



### Application CRC (decimal)

 > 584652534

### Application Sensor Mask (hex)

 > 2

### Map Data for vsm-translator-open-source

M output numSatellites 160 0xa0  1
M output bestSatellites 184 0xb8  1
M output scanCount 185 0xb9  1

