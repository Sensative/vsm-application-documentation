
# Application US-Frequency-hop-test


# Application for performing FCC test case for frequency hopping.

Power on on NFC and will then perform the number of transmissions set (default 10 cycles of 64 channels
each in a psuedo-random order).

SF10 (0a), BW7 (07), 14dBm (0e)


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


## Meta-Information for this application version



### Application CRC (decimal)

 > 3999624005

### Application Sensor Mask (hex)

 > 0

### Map Data for vsm-translator-open-source

```
M input transmitInterval 176 0xb0  1
M input transmitCount 184 0xb8  1
M input count 185 0xb9  1

```

