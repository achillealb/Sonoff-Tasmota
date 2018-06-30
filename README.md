## Sonoff-Tasmota (kabong version with Cover Mode)

## Added Commands
setoption22 1 turns on Cover mode
setoption23 1 turns on momentary action
pulsetimeN sets open/close time required for relays N and N+1
pulsetimeX sets the gap and/or start time for movement (mine is 2 seconds), where X is the number of pairs + cover number

NOTE: pulsetime for covers is ALWAYS seconds (and not the scale used by arendst - ie 13 is 13 seconds)
IE for a 4CH, pulsetime1 is open/close time for first pair
pulsetime3 is the gap/start time for first pair.

setoption23 causes the relays act as momentary action switches and toggled for 250ms at start and end of travel time, instead of on for entire movement time
Except when moving to 0 or 100 (Open or Closed) when only the first toggle occurs and the second ignored

so for my Dual and windw windows I have
setoption22 1
setoption23 0
pulsetime1 23
pulsetime2 2

use the command
cover X
where X is ON, OFF or percentage open (5-100%)
cover 0 thru 4 are reserved as follows
0 - OFF
1 - ON (100%)
2 - Toggle between open/stop/close/stop (ie single switch)
3 - immediate stop
4 - immediate stop and set position to 0 (closed)
NOTE: You can also use a negative offset.
If you do it means turn off all relays and set position as absolute value
ie cover -50 will turn off relays and state position is 50%
NOTE: If you set STATETEXT1 to CLOSE and STATETEXT2 to OPEN, you can also use OPEN/Close as commands

Any GPIO defines as a Switch will work as follows
Switch1 Cover1 Close
Switch2 Cover1 Open
Switch3 Cover2 Close
Switch4 Cover2 Open

I configured, so if you hit any cover button while its moving, the moving will stop.


## Sonoff-Tasmota

Provide ESP8266 based Sonoff by [iTead Studio](https://www.itead.cc/) and ElectroDragon IoT Relay with Serial, Web and MQTT control allowing 'Over the Air' or OTA firmware updates using Arduino IDE.

Current version is **5.12.0b** - See [sonoff/_releasenotes.ino](https://github.com/arendst/Sonoff-Tasmota/blob/development/sonoff/_releasenotes.ino) for change information.

### ATTENTION All versions

Only Flash Mode DOUT is supported. Do not use Flash Mode DIO / QIO / QOUT as it might seem to brick your device.

See [Wiki](https://github.com/arendst/Sonoff-Tasmota/wiki/Theo's-Tasmota-Tips) for background information.

### ATTENTION Version 5 and up

These versions use a new linker script to free flash memory for future code additions. It moves the settings from Spiffs to Eeprom. If you compile your own firmware download the new linker to your IDE or Platformio base folder. See [Wiki > Prerequisite](https://github.com/arendst/Sonoff-Tasmota/wiki/Prerequisite).

Best practice to implement is:
- Open the webpage to your device
- Perform option ``Backup Configuration``
- Upgrade new firmware using ``Firmware upgrade``
- If configuration conversion fails keep the webpage open and perform ``Restore Configuration``

You should now have a device with 32k more code memory to play with.

### Version Information

- Sonoff-Tasmota provides all (Sonoff) modules in one file and starts with module Sonoff Basic.
- Once uploaded select module using the configuration webpage or the commands ```Modules``` and ```Module```.
- After reboot select config menu again or use commands ```GPIOs``` and ```GPIO``` to change GPIO with desired sensor.

<img src="https://github.com/arendst/arendst.github.io/blob/master/media/sonoffbasic.jpg" width="250" align="right" />

See [Wiki](https://github.com/arendst/Sonoff-Tasmota/wiki) for more information.<br />
See [Community](https://groups.google.com/d/forum/sonoffusers) for forum and more user experience.

The following devices are supported:
- [iTead Sonoff Basic](https://www.itead.cc/smart-home/sonoff-wifi-wireless-switch-1.html)
- [iTead Sonoff RF](https://www.itead.cc/smart-home/sonoff-rf.html)
- [iTead Sonoff SV](https://www.itead.cc/smart-home/sonoff-sv.html)<img src="https://github.com/arendst/arendst.github.io/blob/master/media/sonoff_th.jpg" width="250" align="right" />
- [iTead Sonoff TH10/TH16 with temperature sensor](https://www.itead.cc/smart-home/sonoff-th.html)
- [iTead Sonoff Dual (R2)](https://www.itead.cc/smart-home/sonoff-dual.html)
- [iTead Sonoff Pow](https://www.itead.cc/smart-home/sonoff-pow.html)
- [iTead Sonoff 4CH](https://www.itead.cc/smart-home/sonoff-4ch.html)
- [iTead Sonoff 4CH Pro](https://www.itead.cc/smart-home/sonoff-4ch-pro.html)
- [iTead S20 Smart Socket](https://www.itead.cc/smart-socket.html)
- [Sonoff S22 Smart Socket](https://github.com/arendst/Sonoff-Tasmota/issues/627)
- [iTead Sonoff S31 Smart Socket with Energy Monitoring](https://www.itead.cc/sonoff-s31.html)
- [iTead Slampher](https://www.itead.cc/slampher.html)
- [iTead Sonoff Touch](https://www.itead.cc/sonoff-touch.html)
- [iTead Sonoff T1](https://www.itead.cc/sonoff-t1.html)
- [iTead Sonoff SC](https://www.itead.cc/sonoff-sc.html)
- [iTead Sonoff Led](https://www.itead.cc/sonoff-led.html)<img src="https://github.com/arendst/arendst.github.io/blob/master/media/sonoff4ch.jpg" height="250" align="right" />
- [iTead Sonoff BN-SZ01 Ceiling Led](https://www.itead.cc/bn-sz01.html)
- [iTead Sonoff B1](https://www.itead.cc/sonoff-b1.html)
- [iTead Sonoff RF Bridge 433](https://www.itead.cc/sonoff-rf-bridge-433.html)
- [iTead Sonoff Dev](https://www.itead.cc/sonoff-dev.html)
- [iTead 1 Channel Switch 5V / 12V](https://www.itead.cc/smart-home/inching-self-locking-wifi-wireless-switch.html)
- [iTead Motor Clockwise/Anticlockwise](https://www.itead.cc/smart-home/motor-reversing-wifi-wireless-switch.html)
- [Electrodragon IoT Relay Board](http://www.electrodragon.com/product/wifi-iot-relay-board-based-esp8266/)
- AI Light or any my9291 compatible RGBW LED bulb
- H801 PWM LED controller
- [MagicHome PWM LED controller](https://github.com/arendst/Sonoff-Tasmota/wiki/MagicHome-LED-strip-controller)
- AriLux AL-LC01, AL-LC06 and AL-LC11 PWM LED controller
- [Supla device - Espablo-inCan mod. for electrical Installation box](https://forum.supla.org/viewtopic.php?f=33&t=2188)
- [Luani HVIO board](https://luani.de/projekte/esp8266-hvio/)
- Wemos D1 mini and NodeMcu

### License

This program is licensed under GPL-3.0