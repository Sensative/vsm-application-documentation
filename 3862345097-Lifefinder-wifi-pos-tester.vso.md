
# Application Lifefinder-wifi-pos-tester


## Application Outputs


## Application Inputs (settings)


### Input scanFrequency (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b0 (hex) on lora port 2
> - Update value to 1: Send b0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

## Application Sensors (logical sensors)


### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2
> - Mode: R-
> - Type: Enumeration

Physical button readout sensor


## Application Registers used (device controls)


## Meta-Information for this application version



### Application CRC (decimal)

 > 3862345097

### Application Sensor Mask (hex)

 > 2

### Map Data for vsm-translator-open-source

```
M input scanFrequency 176 0xb0  1

```

