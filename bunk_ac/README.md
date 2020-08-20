# bunk_ac
Communes need AC too.

This is documented for an ESP8266, though it should only take minimal modification to install on an ESP32.

## Useful Commands
These are pretty specific to my setup, but with a bit of research this could work for you.

### Compile and Upload OTA to Controller
With `IP` defined and with the root of this repo as the working dir:

`arduino-cli compile --warnings all -t --fqbn esp8266:esp8266:nodemcuv2 bunk_ac/ -p /dev/ttyUSB0 -t && util/espota.py -d -i $IP -f bunk_ac/build/esp8266.esp8266.nodemcuv2/bunk_ac.ino.bin`

### Find IP of Controller

#### Remotely
Requires installation of `avahi-utils` on Debian.

`avahi-browse -ptr  "_arduino._tcp" | egrep ^= | cut -d\; -f4,8,9`

#### With Physical Access
The device prints it's IP over serial upon connection.

### Monitor Serial
This requires being plugged in (duh).

`screen /dev/ttyUSB0 115200`

## Notes
* Install `pyserial` in a Python venv and run `arduino-cli` and `arduino` from it.
* Some random async webserver stuff has to be manually installed (it's not installable through the Arduino IDE package manager)
