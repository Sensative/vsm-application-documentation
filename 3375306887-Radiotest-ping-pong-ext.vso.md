
# Application Radiotest-ping-pong-ext


## Application Outputs


## Application Inputs (settings)


### Input frequency (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

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


## Meta-Information for this application version



### Application CRC (decimal)

 > 3375306887

### Application Sensor Mask (hex)

 > 100

### Map Data for vsm-translator-open-source

```
M input frequency 184 0xb8  1

```

