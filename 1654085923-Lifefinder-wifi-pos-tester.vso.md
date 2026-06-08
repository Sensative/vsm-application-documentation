
# Application Lifefinder-wifi-pos-tester


## Application Outputs


## Application Inputs (settings)


### Input limitedScanChannels (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Limited Wifi Scan Channel Mask
> - Unit: Wifi scan channel mask (binary)
> - Default: 1057 (1, 6 and 11)
> - Min: 0
> - Max: 65535
The app has the option to select only certain channels for WiFi scans in the first attempts to scan, to reduce power
consumption and increase chance of finding WiFi beacons on known channels.
Should you want to scan only channel 1 and 3 you set this to binary 101, or decimal 5. Special value 0 means all channels.

### Input scanFrequency (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b0 (hex) on lora port 2
> - Update value to 1: Send b0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Periodic Positioning Frequency
> - Unit: Minutes
> - Min: 0
> - Max: 32767
> - Default: 1

Periodic positioning frequency in minutes


### Input scanTimeMs (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b1 (hex) on lora port 2
> - Update value to 1: Send b1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Time to scan per channel
> - Unit: ms
> - Min: 100
> - Max: 1000
> - Default: 300

How long time to scan per channel in milliseconds.


## Application Sensors (logical sensors)


### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2
> - Mode: R-
> - Type: Enumeration

Physical button readout sensor


## Application Registers used (device controls)


## Meta-Information for this application version



### Application CRC (decimal)

 > 1654085923

### Application Sensor Mask (hex)

 > 2

### Map Data for vsm-translator-open-source

```
M input scanFrequency 176 0xb0  1
M input scanTimeMs 177 0xb1  1
M input limitedScanChannels 184 0xb8  1

```

