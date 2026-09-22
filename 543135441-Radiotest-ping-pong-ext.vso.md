
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
How long the device goes without hearing anything from the network before it gives the network up and
goes to unjoined. Any downlink starts the time again, an acknowledgement as much as a message.

It asks for an answer well before then. From half of this time on, every uplink it sends is confirmed.
From 80% on it also sends a confirmed link check of its own, even with nothing else to send, and
repeats it until something comes back. Those uplinks count towards LORA_RESEND_COUNT as well, so when
the network has really gone away the device usually unjoins through that count before this time is up.

0 turns the check off, and then reads back as 0xFFFFFFFF. Any other value outside 300-2592000 is ignored
and the previous one kept. The firmware sets it back to 86400 on every boot, so an application that
wants another value writes it in a once rule.

In the unjoined state the application's own rejoin method is used; the firmware does not rejoin by itself.


## Meta-Information for this application version



### Application CRC (decimal)

 > 543135441

### Application Sensor Mask (hex)

 > 100

### Map Data for vsm-translator-open-source

```
M input frequency 184 0xb8  1
C 543135441 # 0x205f96d1

```

