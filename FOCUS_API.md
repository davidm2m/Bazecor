Focus API documentation
===========================

## Concept
The Focus API is a two-way communication mechanism between the Raise and any computer software that wants to get information or configure/activate the raise's plugins.

It discovers all the EEPROM assigned positions of the memory with specific commands to update or trigger them depending on the kind of plugin that uses them.

This means for example being capable of storing the macros or to be able to trigger them through the serial interface without touching the keyboard or Bazecor.

The focus library is a part of the Keyboard's Firmware but also has a helper class created in javascript for the Bazecor, we will show here the commands for the JavaScript Focus API and how to trigger them through the serial interface also, just as an example if you want to retrieve all available commands you have to send the keyboard the string "help".

**For JavaScript:** `focus.command("help")`
**Serial Command (Unix):** `echo 'help' > /dev/ttyACM0`

The serial interface will allways end the current message by a newline feed plus a period.

## Available Methods
Running `focus.command("help")` will get you the following list of available commands:


[version](#version)
[keymap.custom](#keymapcustom)
keymap.default
keymap.onlyCustom
settings.defaultLayer
settings.valid?
settings.version
settings.crc
eeprom.contents
eeprom.free
[led.at](#ledat)
led.setAll
led.mode
led.brightness
led.theme
palette
colormap.map
idleleds.time_limit
hardware.version
hardware.side_power
hardware.side_ver
hardware.sled_ver
hardware.sled_current
hardware.layout
hardware.joint
hardware.keyscan
hardware.crc_errors
hardware.firmware
tapdance.map
macros.map
macros.trigger
hardware.flash_left_side
hardware.flash_right_side
hardware.verify_left_side
hardware.verify_right_side
[help](#help)
layer.activate
layer.deactivate
layer.isActive
layer.moveTo
layer.state
_raise.eepromVersion


### version
Returns the version of the Raise firmware stored in the keyboard's EEPROM
##### Commands
JavaScript: `focus.command("version")`
Serial Command (Unix): `echo 'version' > /dev/ttyACM0`
##### Expected output
it should give back 3 strings, 
- Bazecor Version:
  - `v0.2.4` 
- Kaleidoscope newest Git commit incorporated
  - `6bd1f81e` 
- Raise's Firmware newest Git commit
  - `fe423ce-dirty`
  - Dirty here means it was custom built with the makefile, not built automatically by travis.
### keymap.custom
This command of the focus API has two functions, when sent alone, it retrieves the whole custom keymap stored in the keyboard, when sent with the map as trailing numbers (in the same format as received) it will update the map correlationaly.
##### Commands
To retireve:
- JavaScript: `focus.command("keymap.custom")`
- Serial Command (Unix): `echo 'keymap.custom' > /dev/ttyACM0`

To set:
- JavaScript: `focus.command("keymap.custom N N N N N N N N N N N N N N N")`
- Serial Command (Unix): `echo 'keymap.custom N N N N N N N N N N N N N N N' > /dev/ttyACM0`

Being `N N N...` the 16bit numbers that represent each key assigned to that position of the keymap the numbers amount 80(keys per layer)x10(custom layers)
##### Expected output
It should give back the whole custom keymap (80 key positions for each layer and all 10 layers) if sent alone, if sent with the keymap of the same length as received, it should return a nextline, period.
### keymap.default
This command works in the same way as keymap.custom, but affecting the default layers stored in the -1 and -2 positions of the layer stack.
##### Command
To retireve:
- JavaScript: `focus.command("keymap.default")`
- Serial Command (Unix): `echo 'keymap.default' > /dev/ttyACM0`

To set:
- JavaScript: `focus.command("keymap.default N N N N N N N N N N N N N N N")`
- Serial Command (Unix): `echo 'keymap.default N N N N N N N N N N N N N N N' > /dev/ttyACM0`

Being `N N N...` the 16bit numbers that represent each key assigned to that position of the keymap the numbers amount 80(keys per layer)x2(default layers)
##### Expected output
It should give back the two default layers keymap (80 key positions for each layer for the two default layers) if sent alone, if sent with the keymap of the same length as received, it should return a nextline, period.
### keymap.onlyCustom
This command returns true or false depending on the user setting of hiding the default layers or not, it does not allow you to increment the number of available layers by start using the default ones, they are there so you can store a backup for two layers in your keyboard
##### Commands
To retireve:
- JavaScript: `focus.command("keymap.onlyCustom")`
- Serial Command (Unix): `echo 'keymap.onlyCustom' > /dev/ttyACM0`

To set:
- JavaScript: `focus.command("keymap.onlyCustom true")`
- Serial Command (Unix): `echo 'keymap.onlyCustom trure' > /dev/ttyACM0`
##### Expected output
It should return the current state of the onlyCustom boolean variable stored in the keyboard, being it true or false, when sending the value added to the command, it should return a nextline, period.
### settings.defaultLayer
This command returns the default layer the keyboard will boot in, with this you can change the default layer in which the Raise starts working to any custom layer that you want.
##### Commands
To retireve:
- JavaScript: `focus.command("keymap.defaultLayer")`
- Serial Command (Unix): `echo 'keymap.defaultLayer' > /dev/ttyACM0`

To set:
- JavaScript: `focus.command("keymap.defaultLayer 1")`
- Serial Command (Unix): `echo 'keymap.defaultLayer 1' > /dev/ttyACM0`
##### Expected output
It should return the current default layer stored in the EEPROM, if it's send with the new default layer, it should return a nextline, period.
### settings.valid?

##### Commands
##### Expected output
### settings.version
##### Commands
##### Expected output
### settings.crc
### eeprom.contents
### eeprom.free
### led.at
### led.setAll
### led.mode
### led.brightness
### led.theme
### palette
### colormap.map
### idleleds.time_limit
### hardware.version
### hardware.side_power
### hardware.side_ver
### hardware.sled_ver
### hardware.sled_current
### hardware.layout
### hardware.joint
### hardware.keyscan
### hardware.crc_errors
### hardware.firmware
### tapdance.map
### macros.map
### macros.trigger
### hardware.flash_left_side
### hardware.flash_right_side
### hardware.verify_left_side
### hardware.verify_right_side
### Help
The help command returns all the available commands in the current version of the serial protocol, the list above is taken from this command as per version 0.2.3 of Bazecor/Raise Firmware.
##### Commands
JavaScript: `focus.command("help")`
Serial Command (Unix): `echo 'help' > /dev/ttyACM0`
##### Expected output
The output of this command is a list of all available commands including itself, this list will be ended with a nextline, period trail.
### layer.activate
### layer.deactivate
### layer.isActive
### layer.moveTo
### layer.state
### _raise.eepromVersion