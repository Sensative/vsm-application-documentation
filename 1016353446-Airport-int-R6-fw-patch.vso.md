
# Application Airport-int-R6-fw-patch


## Motion Triggered Tracking

This application has an emphasis on WiFi scanning for positions, although it also
supports GNSS scans (GPS and Beidou).

Each time motion is detected, or when motion has stopped, the app will start a "scan train".
1) After 1 minute, a limited wifi scan will be run. If it finds the required numnber of WIFI
MAC addresses, these will be uplinked and the scan train stops.
2) At a set minute, a second limited wifi scan will be run. Again, if the required number
of MAC addresses are found, they will be uplinked and the scan train stops.
3) After a set period, a full wifi scan will be run. Again, if the required number
of MAC addresses are found, they will be uplinked and the scan train stops.
4) After a set period, a GNSS scan will be run. At this time the scan train stops.

There is a scan budget allowance every 15 minutes. Should the scan budget run out during
the scanning train, the remaining scans will stop unless the budget is once again filled.

> For correct functioning of the GNSS functionality
> it is recommended to run the vsm-mqtt-client in the backend to keep clocks in sync
> and GNSS almanac updated on the devices.

NFC can be used to manually trigger a join attempt
There is a daily rejoin attempt should the device not be joined.
Should the device have been joined since app start, and it is no longer joined it will try a few
quick join attempts before resuming to the 24 hour rejoin regime.

## Battery Reporting Module

Battery remaining esimates are measured on a weekly basis.


## Application Outputs


### Output abandonedCart (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean
Uplinked after abandonedCartTime_minutes minutes.
Should be compared to device position on server to see if it's in a corall or not.

### Output accelerometerStateDebug (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Integer
When motionDebugEnable is active, this value represents the 3DAccelerometers internal state.
0 = UNKNOWN, 1 = STILL, 2 = MOVING, 3 = SHOCKED.

### Output batteryPercent (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: % (estimated)

Estimated remaining % of battery in this unit based on measured use time and power for MCU, Radio, Sensors
Position Scans, and potential collateral power use.


### Output motionCount (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Unit: Motion count (Integer)
Uplinked on an hourly basis should the number of detected motions have changed. It is the accumulated number of
motions detected by the sensor since it was started. This reporting is enabled by setting the input
motionCountEnabled to a value other than 0.

### Output motionDebug (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Unit: Boolean
When motionDebugEnable is active, this bit represents the apps motion state.
0 = still, 1 = moving.

## Application Inputs (settings)


### Input abandonedCartTime_minutes (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b3 (hex) on lora port 2
> - Update value to 1: Send b3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Minutes
> - Min: 0
> - Max: 127
> - Default: 0 (Off)
How many minutes after the device stops moving before it reports itself as having been abandoned.

### Input fullScanChannels (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b9 (hex) on lora port 2
> - Update value to 1: Send b9 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Wifi scan channel mask (binary)
> - Default: 0 (all channels)
If the application fails to collect the required number of gateways ()
Should you want to scan only channel 1 and 3 you set this to binary 101, or decimal 5.

### Input fullWifiScan_minutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a4 (hex) on lora port 2
> - Update value to 1: Send a4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Minutes
> - Min: -1
> - Max: 127
How many minutes to wait after transition to try a full WIFI scan? Set to -1 to disable.
Avoid the value 1 since there is a hard-coded scan which will occur at minute 1
after change between moving and not moving and vice versa.
> Note the minimumWifiCount setting, which may cancel a scan before reaching this scan stage.
> Avoid setting this to the same value as fullWifiScan_minutes to create a deterministic scan sequence.

### Input gpsScan_minutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a5 (hex) on lora port 2
> - Update value to 1: Send a5 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Minutes
> - Min: -1
> - Max: 127
How many minutes to wait after transition to try a GNSS scan? Set to -1 to disable.
Avoid the value 1 since there is a hard-coded scan which will occur at minute 1
after change between moving and not moving and vice versa.
> Avoid setting this to the same value as fullWifiScan_minutes to create a deterministic scan sequence.
> Note the minimumWifiCount setting, which may cancel a scan before reaching this scan stage.

### Input limitedScanChannels (unconfirmed)

> - Size: 4 bytes
> - Translation factor: 1
> - Request current value: Send b8 (hex) on lora port 2
> - Update value to 1: Send b8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Wifi scan channel mask (binary)
> - Default: 0 (all channels)
The app has the option to select only certain channels for WiFi scans in the first attempts to scan, to reduce power
consumption and increase chance of finding WiFi beacons on known channels.
Should you want to scan only channel 1 and 3 you set this to binary 101, or decimal 5.

### Input maxBudget (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b2 (hex) on lora port 2
> - Update value to 1: Send b2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Positioning budgetary unit
> - Min: 1
> - Max: 32767
> - Default: 100
Limit the budget for scans. Each positioning scan consumes one budgetary unit.

### Input minimumWifiCount (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a3 (hex) on lora port 2
> - Update value to 1: Send a3 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Wifi MAC address count
> - Min: 1
> - Max: 15
How many wifi MAC addresses to find to be satisfied that the scan sequence should stop.

### Input motionCountEnabled (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a6 (hex) on lora port 2
> - Update value to 1: Send a6 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Boolean
> - Default: 0 (false)
Set to non-zero to enable reporting the number of motions detected. See motionCount.

### Input motionDebugEnable (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a8 (hex) on lora port 2
> - Update value to 1: Send a8 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Boolean
Enables reporting of internal motion states.

### Input motionReleaseDelay (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send ab (hex) on lora port 2
> - Update value to 1: Send ab 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Integer
How long the app waits for a new motion interrupt before transitioning to the still state.

### Input movingMotionThreshold_mm_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b1 (hex) on lora port 2
> - Update value to 1: Send b1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: mm/s2
> - Min: 5 mm/s2
> - Max: 10000 mm/s2
> - Default: 50 mm/s2
The accelerometer threshold to use for redetection of motion while currently in motion. **If set too low it means the device will
believe it is in constant motion and will not trigger a chain of position scans when still** It is recommended
to start from high values and then decrease should sensitivity be too low.


### Input movingWifiScanAgain_minutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a2 (hex) on lora port 2
> - Update value to 1: Send a2 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Minutes
> - Min: -1
> - Max: 127
How many minutes to wait after transition to try again while moving? Set to -1 to disable.
Avoid the value 1 since there is a hard-coded scan which will occur at minute 1
after change between moving and not moving and vice versa.

### Input quarterlyScanBudget (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a0 (hex) on lora port 2
> - Update value to 1: Send a0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Positioning budgetary unit
> - Min: 1
> - Max: 127
How many scans are added to the budget per 15 minutes?

### Input quickRejoinBudgetMax (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b4 (hex) on lora port 2
> - Update value to 1: Send b4 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Integer
Max number of quick rejoins before reverting back to daily rejoin attempts

### Input singleWifiScanAgain_minutes (unconfirmed)

> - Size: 1 bytes
> - Translation factor: 1
> - Request current value: Send a1 (hex) on lora port 2
> - Update value to 1: Send a1 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: Minutes
> - Min: -1
> - Max: 127
How many minutes to wait after transition to try again while not moving? Set to -1 to disable.
Avoid the value 1 since there is a hard-coded scan which will occur at minute 1
after change between moving and not moving and vice versa.

### Input stillMotionThreshold_mm_s2 (unconfirmed)

> - Size: 2 bytes
> - Translation factor: 1
> - Request current value: Send b0 (hex) on lora port 2
> - Update value to 1: Send b0 00 00 00 01 (hex) on lora port 2
> - *Note: It is highly recommended to ensure that you use higher level applications to update settings so that the correct version of this application is used as reference (these data may change or differ between sensors)*
> - Unit: mm/s2
> - Min: 5 mm/s2
> - Max: 10000 mm/s2
> - Default: 50 mm/s2
The accelerometer threshold to use for detection of motion while stationary. **If set too low it means the device will
believe it is in constant motion and will not trigger a chain of position scans when still** It is recommended
to start from high values and then decrease should sensitivity be too low.


## Application Sensors (logical sensors)


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


### Register BATTERY_PERCENT

> - Request current value: Send f4 (hex) on lora port 2
Percent of (non-zero) battery capacity used
> - Mode: R-
> - Unit: mAh

### Register LINKCHECK_TIME

> - Request current value: Send d0 (hex) on lora port 2
> Mode: RW
> Unit: seconds
> Min: 300
> Max: 2592000
> Default: 86400
Once 80% of this time has passed, the device will make all messages confirmed until it gets a confirmation.
Should this time pass without the device hearing a confirmed response, it will go to DEVICE_STATE_ACTIVE_UNJOINED.


### Register STREAMING_RATE

> - Request current value: Send d6 (hex) on lora port 2
> - Mode: RW
> - Unit: Seconds

The average rate at which the device streams data, e.g. delay between lora transactions.
Actual rate is randomized at this value +- 50% to avoid potential repeat collisions, for instance if the device is
triggered by sound or acceleration.

### Register TX_POWER_RANGE

> - Request current value: Send d8 (hex) on lora port 2
Set the power index range for fast ADR, LSB = lowest, MSB = highest
Range for each is 0 (DR0/Max power) - 16 (regions best), mixing up
highest and lowest does not matter (firmware always use the highest of the two as the max).
> - Mode: RW
> - Min: 0
> - Max: 65535
> - Unit: Seconds

## Meta-Information for this application version



### Application CRC (decimal)

 > 1016353446

### Application Sensor Mask (hex)

 > 400100

### Map Data for vsm-translator-open-source

```
M input stillMotionThreshold_mm_s2 176 0xb0  1
M input movingMotionThreshold_mm_s2 177 0xb1  1
M input limitedScanChannels 184 0xb8  1
M input fullScanChannels 185 0xb9  1
M output motionCount 186 0xba  1
M input quarterlyScanBudget 160 0xa0  1
M input maxBudget 178 0xb2  1
M input singleWifiScanAgain_minutes 161 0xa1  1
M input movingWifiScanAgain_minutes 162 0xa2  1
M input minimumWifiCount 163 0xa3  1
M input fullWifiScan_minutes 164 0xa4  1
M input gpsScan_minutes 165 0xa5  1
M input motionCountEnabled 166 0xa6  1
M input abandonedCartTime_minutes 179 0xb3  1
M output abandonedCart 167 0xa7  1
M input quickRejoinBudgetMax 180 0xb4  1
M input motionDebugEnable 168 0xa8  1
M output motionDebug 169 0xa9  1
M output accelerometerStateDebug 170 0xaa  1
M input motionReleaseDelay 171 0xab  1
M output batteryPercent 172 0xac  1

```

