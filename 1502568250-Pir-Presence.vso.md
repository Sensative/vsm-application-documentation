
# Application Pir-Presence


## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


## Application Outputs


### Output batteryPercent (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: % (estimated)

Estimated remaining % of battery in this unit based on measured use time and power for MCU, Radio, Sensors
Position Scans, and potential collateral power use.


## Application Inputs (settings)


### Input PirAvgTrim (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Value
> - Default: 0x03
> - SkipDefaultCheck: true
> - Min: 0
> - Max: 63

AVG_TMOS
0xX0 => 8
0xX1 => 4
0xX2 => 2
0xX3 => 1

AVG_T
0x0X => 2
0x1X => 8
0x2X => 32
0x3X => 128
0x4X => 256
0x5X => 512
0x6X => 1024
0x7X => 2048


### Input PirCmd (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Value
> - Default: 0
> - Min: 0
> - Max: 0xffffffff


### Input PirHystPresence (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Value
> - Default: 0x32
> - SkipDefaultCheck: true
> - Min: 0
> - Max: 127

Hysteresis configuration value for presence detection algorithm


### Input PirLpf1 (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Value
> - Default: 0x04
> - SkipDefaultCheck: true
> - Min: 0
> - Max: 63

LPF_M
0b00xxx000 => ODR/9
0b00xxx001 => ODR/20
0b00xxx010 => ODR/50
0b00xxx011 => ODR/100
0b00xxx100 => ODR/200
0b00xxx101 => ODR/400
0b00xxx110 => ODR/800

LPF_P_M
0b00000xxx => ODR/9
0b00001xxx => ODR/20
0b00010xxx => ODR/50
0b00011xxx => ODR/100
0b00100xxx => ODR/200
0b00101xxx => ODR/400
0b00110xxx => ODR/800


### Input PirLpf2 (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Value
> - Default: 0x22
> - SkipDefaultCheck: true
> - Min: 0
> - Max: 63

LPF_A_T
0b00xxx000 => ODR/9
0b00xxx001 => ODR/20
0b00xxx010 => ODR/50
0b00xxx011 => ODR/100
0b00xxx100 => ODR/200
0b00xxx101 => ODR/400
0b00xxx110 => ODR/800

LPF_P
0b00000xxx => ODR/9
0b00001xxx => ODR/20
0b00010xxx => ODR/50
0b00011xxx => ODR/100
0b00100xxx => ODR/200
0b00101xxx => ODR/400
0b00110xxx => ODR/800


### Input PirPresenceTheshold (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b9 (hex) on lora port 2
> - Update value to 1: Send b9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Value
> - Default: 200
> - SkipDefaultCheck: true
> - Min: 0
> - Max: 32767

Presence threshold for presence detection algorithm


### Input PirResetAlgo (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Value
> - Default: 0
> - Min: 0
> - Max: 1

Reset algo trigger


### Input PirResetInDarkMinutes (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send bb (hex) on lora port 2
> - Update value to 1: Send bb 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Minutes
> - Default: 0 (Off)
> - Min: 0
> - Max: 65535

Minutes when dark to reset if false detected occupied


### Input PirResetLuxTreshold (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send ba (hex) on lora port 2
> - Update value to 1: Send ba 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Lux
> - Default: 0 (Off)
> - Min: 0
> - Max: 65535

Lux treshold to detect room is dark to reset if false detected occupied


### Input PirSamplingRate (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Index in list
> - Default: 3 (1Hz)
> - Min: 0
> - Max: 16

Sampling rate
1 => 0.25Hz
2 => 0.5Hz
3 => 1Hz
4 => 2Hz
5 => 4Hz
6 => 8Hz
7 => 15Hz
8 => 30Hz


## Application Sensors (logical sensors)


### Sensor AMBIENT_LIGHT

> - Request current value: Send 0b (hex) on lora port 2
> - Unit: lux

Measured and calibrated lux reading

### Sensor PIR

> - Request current value: Send 2a (hex) on lora port 2

## Application Registers used (device controls)


## Meta-Information for this application version



### Application CRC (decimal)

 > 1502568250

### Application Sensor Mask (hex)

 > c00

### Map Data for vsm-translator-open-source

```
M input PirSamplingRate 160 0xa0  1
M input PirLpf1 161 0xa1  1
M input PirLpf2 162 0xa2  1
M input PirAvgTrim 163 0xa3  1
M input PirCmd 184 0xb8  1
M input PirResetAlgo 164 0xa4  1
M output batteryPercent 165 0xa5  1
M input PirPresenceTheshold 185 0xb9  1
M input PirHystPresence 166 0xa6  1
M input PirResetLuxTreshold 186 0xba  1
M input PirResetInDarkMinutes 187 0xbb  1
C 1502568250 # 0x598f5f3a

```

