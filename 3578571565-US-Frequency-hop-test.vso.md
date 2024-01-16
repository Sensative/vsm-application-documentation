
# Application US-Frequency-hop-test


# Application for performing FCC test case for frequency hopping.

Power on on NFC and will then perform the number of transmissions set (default 10 cycles of 64 channels
each in a psuedo-random order).


## Application Outputs


## Application Inputs (settings)


### Input count (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b9 (hex) on lora port 2
> - Update value to 1: Send b9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Current transmission count. Not intended for update but can be set in order to
prolong the current session.

> - Default: 0
> - Unit: transmissions

### Input transmitCount (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Number of transmissions to perform

> - Default: 10 * 64
> - Unit: Tranmissions


### Input transmitInterval (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b0 (hex) on lora port 2
> - Update value to 1: Send b0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Interval in seconds between transmissions

> - Default: 20
> - Unit: Seconds


## Application Sensors (logical sensors)


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

### Register HOPPING_FREQUENCY

> - Request current value: Send f9 (hex) on lora port 2

### Register NOW

> - Request current value: Send c5 (hex) on lora port 2
> - Mode: R-
> - Unit: Seconds

Current time in seconds since device powered on.


### Register RADIO_TEST_CMD

> - Request current value: Send dd (hex) on lora port 2

### Register RADIO_TEST_DATA1

> - Request current value: Send e0 (hex) on lora port 2

### Register RADIO_TEST_DATA2

> - Request current value: Send e1 (hex) on lora port 2

### Register RADIO_TEST_FREQ

> - Request current value: Send de (hex) on lora port 2

### Register RADIO_TEST_HEAD

> - Request current value: Send df (hex) on lora port 2

### Register RADIO_TEST_PARS

> - Request current value: Send e2 (hex) on lora port 2

### Register SLEEP_PERIOD

> - Request current value: Send cf (hex) on lora port 2
> - Mode: RW
> - Unit: seconds

When set to non-zero value the VM will wake up at at this interval. Make rules dependent on NOW or


## Meta-Information for this application version



### Application CRC (decimal)

 > 3578571565

### Application Sensor Mask (hex)

 > 0

### Map Data for vsm-translator-open-source

```
M input transmitInterval 176 0xb0  1
M input transmitCount 184 0xb8  1
M input count 185 0xb9  1

```

