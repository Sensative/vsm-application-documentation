
# Application Compliance-test

## Application for setting the device in LCTT compliance test mode.

In this mode the device will run in ADR mode, and will handle compliance test according to specification
(e.g. interval messages and join behaviour).

## Application Outputs


## Application Inputs (settings)


## Application Sensors (logical sensors)


## Application Registers used (device controls)


### Register APP_CONFIG

> - Request current value: Send ca (hex) on lora port 2
> - Mode: RW
> - Unit: Bit mask

Enable or disable certain functions of the device, such as power on/off behaviours.


### Register DATA_RATE

> - Request current value: Send d4 (hex) on lora port 2

## Meta-Information for this application version



### Application CRC (decimal)

 > 1319111708

### Application Sensor Mask (hex)

 > 0

### Map Data for vsm-translator-open-source


