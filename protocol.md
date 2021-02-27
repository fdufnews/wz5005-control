## Command / response structure

Each command seems to be exactly 20 bytes long.

Commands trigger a response from the device. The response has the exact same structure, except command parameters are substituted with response values.

Here's a byte breakdown of contents of a message:

| Bytes | Meaning |
| :-: | - |
| 1 | Header; Static value |
| 2 | Device number |
| 3 | Command |
| 4-19 | Command arguments / response values |
| 20 | Checksum byte |

### Header

Always set to the same value (TODO: Determine what it is)

### Device number

There's a command to set a device's number - I haven't tested this, but it seems we can have multiple devices on the serial bus.
In this case this byte should tell them which one we are talking to.

### Command 

Number if the command we want to issue. Check the commands table for possible values.

### Command arguments

If a command takes arguments (e.g. set voltage, set device number) - this is where we place them.

Unused arguments should be set to 0x00.

### Checksum

Single-byte checksum value. Not yet tested, but most likely the device will reject commands with bad checksums. TODO: Determine checksum algo.
