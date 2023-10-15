
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

## Application Registers used (device controls)


### Register APP_CONFIG

> - Request current value: Send ca (hex) on lora port 2

### Register DEVICE_STATE

> - Request current value: Send c8 (hex) on lora port 2

### Register GNSS

> - Request current value: Send cc (hex) on lora port 2

### Register LED

> - Request current value: Send c9 (hex) on lora port 2

### Register NOW

> - Request current value: Send c5 (hex) on lora port 2

### Register SATELLITE_BEST_SNR

> - Request current value: Send ec (hex) on lora port 2

### Register SATELLITE_COUNT

> - Request current value: Send ce (hex) on lora port 2

### Register SLEEP_PERIOD

> - Request current value: Send cf (hex) on lora port 2

### Register WIFI

> - Request current value: Send da (hex) on lora port 2

## Meta-Information for this application version



### Application CRC (decimal)

 > 3099888482

### Application Sensor Mask (hex)

 > 2

### Map Data for vsm-translator-open-source

M output numSatellites 160 0xa0  1
M output bestSatellites 184 0xb8  1
M output scanCount 185 0xb9  1

