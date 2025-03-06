
# Application Motion-spectrum

On a device with support for accelerometer with motion spectum measurement, this application measures and reports 
approximate motion spectrum values and measured motion energy, by each octave from 1Hz to 256Hz.

There are three modes of operation
1) Interval-based motion spectrum measurement
2) Motion spectrum measurement while motion is detected
0) Motion spectrum measurement disabled (enable mode 1 or 2 at certain times by downlink)

The spectral analysis is simplified for battery and device capacity reasons, and is hence not perfect but it does give a fair assessment of energy distribution across each octave.

Upon a new impulse of motion, accelerometer is measured at a high rate over 2 seconds. In mode 2, this is repeated at approximately 2 second intervals as long as continued motion is detected.

Any change in energy or spectral content is reported over lorawan. Measurement is only active while the device is joined to a network.


## Lower Power Temperature Sensing and Reporting Module


### General Temperature Operation

> The temperature is measured every 15 minutes and then processed.

When the sensor detects an air temperature which has changed from the previous uploaded temperature by more than
the set tempHysteresis it will upload a new temp reading.


### Temperature Alarms

When a temperature is detected which exceeds the tempAlarmHighLevel the tempAlarm will be set to 1.


When a temperature is detected which is below the tempAlarmLowLevel the tempAlarm will be set to -1.


### Current Temperature Reporting

Temp alarms are cancelled when temperature is between low level and high level (with hysteresis)


### Average Temperature Reporting

When averageTempIntervalMinutes have passed, and if the average temperature has changed more than tempHysteresis degrees,
the sensor will upload a new averageTemp value.

## Slow Tracker Module

This module enables slow tracking through WIFI scanning or GNSS scans (if device supports GNSS scanning).
For proper functioning of GNSS enabled devices, the GNSS almanac and device time needs to be kept up-to-date,
for instance through NFC application or through enabling the vsm-mqtt-client (https:


When the button is pressed, a wifi scan will be done.


Daily when the device is joined, it will attempt a wifi scan.


Weekly, when the device is joined, it will attempt a GNSS scan (provided the device supports GNSS scanning).


# Module Motion Spectrum

Calculates an approximation of motion spectrum (over 2s) when the device detects motion.
Depending on the motion spectrum mode it may generate a continuous signal (e.g. sample every ~2 s)
or on approximately 1 minute intervals until motion is no longer detected.

The data is reported as percentage of energy in each octave with band pass. The filters are at approximately
1Hz, 2Hz, 4Hz, 8Hz, 16Hz, 32Hz, 64Hz, 128Hz and 256Hz. Sample rate is approximately 800Hz.


The module only estimates spectrum information while joined (to avoid measuring
transportation or while in stock).

The module reports motion spectrum values when they have changed (but not when the device stops moving - which would
otherwise just report a bunch of zeros and increase the data use).
Instead a moving report is sent to indicate the change of motion state.

No spectral data will be transmitted if the total energy is less than (motionThreshold_m_s2*motionThreshold_m_s2),
this is in order to avoid transmission of unnecessary data when using the single-shot polled mode. If the accelerometer
triggered in any wake-on-motion mode, it will likely have exceeded that energy already.


Join on NFC field

Join every 24 hours if not joined

## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


## ADR dampening and limiting module

Adaptive LoRaWan data rate dampening and limiter module, allows to limit both adaptability rate and worst data rate / output power.
This is intended for fixed-mount devices where radio conditions are not expected to change rapidly.


## Orientation tracking module

Reports any updates to orientation in accX, accY and accZ when they happen,
>
> This functionality is reliable only in Spectrum Reporting Modes 0 and 1.
>

## Application Outputs


### Output accX (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.001
X acceleration

Updated when a change happens, and also when the device has been still for a while (~1 minute).

XYZ is normally dominated by the gravitation, so by taking the three XYZ components you will
be able to determine the orientation of the device. An accelerating device (e.g. subject to
vibration etc may gove strange values)
> - Unit: m/s/s

### Output accY (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.001
Y acceleration

Updated when a change happens, and also when the device has been still for a while (~1 minute).

XYZ is normally dominated by the gravitation, so by taking the three XYZ components you will
be able to determine the orientation of the device. An accelerating device (e.g. subject to
vibration etc may gove strange values)
> - Unit: m/s/s

### Output accZ (confirmed)

> - Size: 2 bytes
> - Translation factor: 0.001
Z acceleration

Updated when a change happens, and also when the device has been still for a while (~1 minute).

XYZ is normally dominated by the gravitation, so by taking the three XYZ components you will
be able to determine the orientation of the device. An accelerating device (e.g. subject to
vibration etc may gove strange values).
> - Unit: m/s/s

### Output acc_128hz (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output acc_16hz (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output acc_1hz (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

Outputs are estimated energy distribution per octave (%) and total energy level for the measured motion.


### Output acc_256hz (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output acc_2hz (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output acc_32hz (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output acc_4hz (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output acc_64hz (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output acc_8hz (confirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output acc_energy_sum_mms2_square (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1

### Output averageTemp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit:C

The average temperature uploaded with a resolution 0.01C.


### Output batteryPercent (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: % (estimated)

Estimated remaining % of battery in this unit based on measured use time and power for MCU, Radio, Sensors
Position Scans, and potential collateral power use.


### Output motion (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1

### Output temp (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Unit: C

The temperature uploaded with a resolution of 0.01 C

> Accuracy is limited by accuracy of temperature sensor in the product. Refer to datasheet.

### Output tempAlarm (confirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Enumeration
> -- No alarm: 0
> -- High alarm: 1
> -- Low alarm: -1

Confirmed uplink which will indicate if one of the set limits are exceeded


## Application Inputs (settings)


### Input averageTempIntervalHours (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Average Temp Interval
> - Unit: Hours
> - Min: 1h
> - Max: 127h
> - Default: 2h

The interval at which average temperature is uploaded (provided that it has changed more than tempHysteresis).


### Input enableXYZ (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a9 (hex) on lora port 2
> - Update value to 1: Send a9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
Enable XYZ reporting
> - UI: Enable XYZ orientation change reporting
> - Unit: Boolean
> - Default: 0
> - Min: 0
> - Max: 1

### Input maxPowerIndex (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a8 (hex) on lora port 2
> - Update value to 1: Send a8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Max Power Index
> - Unit: LoraWan power index (0-16)
> - Min: 0
> - Max: 16
> - Default: 14

maximum power index to use for LoRaWan traffic, including join. Default setting disables DR0

### Input motionPollIntervalMinutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Poll interval for single shot mode (e.g. instead of motion triggered, use the single-shot mode)
Can only to be together with motionSpectrumMode=3

> - UI: Motion Poll Interval
> - Unit: minutes
> - Default: 10
> - Min: 1
> - Max: 127

### Input motionSpectrumMode (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*

Accelerometer mode

Modes to use:

1 - Interval measurement while moving (default).
2 - Constant measurement while moving.
3 - Fixed interval measurement, set the motionPollIntervalMinutes to wanted measurement interval.

Note: 0 will put accelerometer in wake on motion, without measuring spectrums.

> - UI: Spectrum Reporting Mode
> - Unit: enumeration
> - Default: 1
> - Min: 0
> - Max: 3

### Input motionThreshold_m_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.001
> - Request current value: Send b3 (hex) on lora port 2
> - Update value to 1: Send b3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
Wakeup sensitivity

For wake-on-motion modes (0-2) this sets the wakeup level.
For the single-shot mode, the square of this determines the amount of energy required to
transmit a spectrum analysis over LoRaWan (for energy and bandwidth saving).

> - UI: Motion threshold
> - Unit: m/s/s
> - Default: 0.2
> - Min: 0.05
> - Max: 2

### Input powerIndexFilterFactor (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a7 (hex) on lora port 2
> - Update value to 1: Send a7 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: LoRaWan power filter factor
> - Unit: Integer
> - Min: 1
> - Max: 50
> - Default: 3

Low pass filter factor. 1 = no low-pass filter. 2 = filter factor 1 (fast) ... 10 = very slow.
When the built-in ADR function propose a new power index, this filter factor is employed in a low pass filter.
If the filter value is set to 1 the algorithm will use its proposed new value (if below or at max).

### Input tempAlarmHighLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Alarm High Level
> - Unit: C
> - Min: -127
> - Max: 127
> - Default: 60

The high level for temperature alarm. Set higher than tempAlarmLowLevel or the alarm function is disabled.


### Input tempAlarmLowLevel (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Alarm Low Level
> - Unit: C
> - Min: -128
> - Max: 126
> - Default: 2

The low level for temperature alarm. Set lower than tempAlarmHighLevel or the alarm function is disabled.


### Input tempHysteresis (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 0.01
> - Request current value: Send b2 (hex) on lora port 2
> - Update value to 1: Send b2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - UI: Temperature Hysteresis
> - Unit:C
> - Min: 0.1
> - Max: 127
> - Default: 2

The hysteresis for temperature readings. If temperature changes lower than this value are detected
no report will be generated (saves battery and radio air time).


## Application Sensors (logical sensors)


### Sensor ACC_128HZ

> - Request current value: Send 27 (hex) on lora port 2

### Sensor ACC_16HZ

> - Request current value: Send 24 (hex) on lora port 2

### Sensor ACC_1HZ

> - Request current value: Send 20 (hex) on lora port 2
Accelerometer spectral analyzer results

### Sensor ACC_256HZ

> - Request current value: Send 28 (hex) on lora port 2

### Sensor ACC_2HZ

> - Request current value: Send 21 (hex) on lora port 2

### Sensor ACC_32HZ

> - Request current value: Send 25 (hex) on lora port 2

### Sensor ACC_4HZ

> - Request current value: Send 22 (hex) on lora port 2

### Sensor ACC_64HZ

> - Request current value: Send 26 (hex) on lora port 2

### Sensor ACC_8HZ

> - Request current value: Send 23 (hex) on lora port 2

### Sensor ACC_ENERGY_SUM

> - Request current value: Send 29 (hex) on lora port 2

### Sensor ACC_X

> - Request current value: Send 1a (hex) on lora port 2
Current accelerometer reading

### Sensor ACC_Y

> - Request current value: Send 1b (hex) on lora port 2
Current accelerometer reading

### Sensor ACC_Z

> - Request current value: Send 1c (hex) on lora port 2
Current accelerometer reading

### Sensor AIR_TEMPERATURE

> - Request current value: Send 04 (hex) on lora port 2
> - Unit: CentiCelcius

Air temperature sensor (logical)

### Sensor BUTTON

> - Request current value: Send 01 (hex) on lora port 2
> - Mode: R-
> - Type: Enumeration

Physical button readout sensor


### Sensor MOTION

> - Request current value: Send 16 (hex) on lora port 2
> - Type: Enumeration

Motion sensor reading, one of
- 0 : Unknown
- 1 : Still (less than register MOTION_CONTROL mm/s2 acceleration change detected through last minute)
- 2 : Moving (more than register MOTION_CONTROL mm/s2 acceleration change detected through last minute)
- 3 : Shocked (more than 4m/s2 change in acceleration detected through last minute)

### Sensor NFC_FIELD

> - Request current value: Send 08 (hex) on lora port 2
> - Type: Boolean

NFC field present sensor (logical)


## Application Registers used (device controls)


### Register GPS_TIME_MAX_AGE

> - Request current value: Send cd (hex) on lora port 2
> - UI:   Device Time Max Age
> - Mode: RW
> - Unit: Seconds
> - Default: 0
> - Min: 0
> - Max: 4294967295
Once this maximum age has passed the device will no longer trust its GPS_TIME and GNSS scans become autonomous.
Also, it will start emitting DEVICE_TIME requests on the LoRaWan network once 80% of this time has passed.
Typically the clock drift is a few seconds per 24 hrs. Gps time should be correct within 30s for good assisted scans.
Outdoor use tends to increase clock drift.


### Register TX_POWER_RANGE

> - Request current value: Send d8 (hex) on lora port 2
Set the power index range for fast ADR, LSB = lowest, MSB = highest
Range for each is 16 (DR0/Max power) - 0 (regions best), mixing up
highest and lowest does not matter (firmware always use the highest of the two as the max).
There is a high impact on power consumption to turn this up (lower battery time).

> - UI:   TX Power Range
> - Mode: RW
> - Min: 0
> - Max: 65535
> - Unit: 2 bytes


## Meta-Information for this application version



### Application CRC (decimal)

 > 1548534003

### Application Sensor Mask (hex)

 > 1c4003ff

### Map Data for vsm-translator-open-source

```
M output temp 176 0xb0  0.01
M output averageTemp 177 0xb1  0.01
M input tempHysteresis 178 0xb2  0.01
M input averageTempIntervalHours 160 0xa0  1
M output tempAlarm 128 0x80  1
M input tempAlarmLowLevel 161 0xa1  1
M input tempAlarmHighLevel 162 0xa2  1
M input motionThreshold_m_s2 179 0xb3  0.001
M input motionSpectrumMode 163 0xa3  1
M output acc_1hz 129 0x81  1
M output acc_2hz 130 0x82  1
M output acc_4hz 131 0x83  1
M output acc_8hz 132 0x84  1
M output acc_16hz 133 0x85  1
M output acc_32hz 134 0x86  1
M output acc_64hz 135 0x87  1
M output acc_128hz 136 0x88  1
M output acc_256hz 137 0x89  1
M output acc_energy_sum_mms2_square 184 0xb8  1
M output motion 164 0xa4  1
M input motionPollIntervalMinutes 165 0xa5  1
M output batteryPercent 166 0xa6  1
M input powerIndexFilterFactor 167 0xa7  1
M input maxPowerIndex 168 0xa8  1
M output accX 144 0x90  0.001
M output accY 145 0x91  0.001
M output accZ 146 0x92  0.001
M input enableXYZ 169 0xa9  1

```

