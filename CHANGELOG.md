# Changelog
### 2026-02-10

* [*][All chips] The power-saving mode (PSM) in the firmware has been improved to provide additional energy savings. The changes are especially noticeable for CC2530 chips, which consume an excessively large amount of power in active mode.
* [*][All chips] The time interval for sending periodic reports has been reduced.
* [*][All chips] The mode for checking queued commands has been improved.
* [*][All chips] Compatibility of custom converters with the new ZHA in Home Assistant 2026.2.

### 2025-10-23

* [+][All chips] Added the "Internal use" option for outputs to disable periodic reports while using data in internal automation (group switches, display output, etc.).
* [-][CC2530] Fixed a GPIO outputs initialization bug where the saved state was not taken into account (appeared in recent versions).
* [-][All chips] Remote interval configuration did not work if the configuration contained only sensors without GPIO.
* [-][Configurator] The preset for the LED informer did not load, and therefore the firmware could not be built.

### 2025-08-21

* [*] Fixed an issue when the device would hang with the periodic report was disabled.
* [+] CC2530: Optimized the GPIO initialization process at startup. This may eliminate the relay click on some devices (this issue was not observed on CC2652).

### 2025-03-21

* [*] Fixed an issue with sending battery status in certain firmware configurations for the remote control.
* [*] Fixed issue with remote configuration of report intervals (previously, the control unit could completely disable reports).

### 2025-03-19

* [*] Fixed the issue with reading data from MAX31855, MAX31865
* [*] Fixed operation in Z2M with some configurations.
* [+][CC2652] Added support for displays (7-segment, LCD, OLED based on SSD1306). It is now possible to display values both from connected sensors and those sent from the smart home.

### 2025-01-24

* [+][CC2652] The 16-channel firmware supports up to 16 sensors now.
* [*] Update the French translation.

### 2024-12-14

* [-][All chips] Fixed an issue in the LED firmware that appeared after 2024-04-06. The firmware was almost non-functional.
* [-][All chips] Fixed an issue with pca9685 and x9c100 that appeared after 2024-04-06.
* [-][All chips] Fixed an issue with the pulse switch.
* [-][Configurator] Fixed the creation of a converter for some sensors for ZHA.
* [*][Configurator] Improved external converter generation for upcoming Z2M v2.

### 2024-10-27

* [-][Configurator] Fixed an error while creating an external converter for firmware with a GPIO output type, different from "General".

### 2024-09-30

* [-][All chips] Calibration function for ACS712 restored.
* [-][All chips] Reporting of ADC value (raw) was fixed.
* [-][All chips] Manual reading of the UART sensor analog value did not work [(#309)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/309).
* [-][All chips] The firmware no longer returns an error when the higher-level system tries to set the periodic report interval while this function is disabled in the configuration. It simply ignores it quietly.
* [+][All chips] Added binding capability to a group when the PTVO device is the command source [(#156)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/156).
* [*][CC2530] HC-SR04 sensor is now unavailable in the router mode.
* [-][Configurator] The "Disable periodic On/Off reports" option was not saved  [(#310)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/310).
* [-][Configurator] Configuration for outputs 8-16 was not loaded correctly from the file.
* [*][Configurator] Other minor improvements.

### 2024-08-19

* Corrections only concern the creation of custom quirks for ZHA
* [+][Configurator] Added compatibility with the new version of ZHA in HA.
* [*][Configurator] When a switch was present on the first output, an incorrect device signature was formed, causing the quirk not to connect.
* [*][Configurator] Fixed quirk generation for air quality sensors [(#287)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/287)
* [*][Configurator] Fixes related to a quirk for UART sensors [(#279)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/279).

### 2024-07-19

* [-][CC2652] Using UART or sensors with this interface could cause the device to freeze [(#257)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/257).
* [-][All chips] It was not possible to set two different I2C or SPI sensors on different pins consecutively [(#296)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/296).
* [+][Configurator] Added additional configuration checks before saving to a HEX file.
* [+][Configurator] Added a correctness check for the settings of some sensors [(#298)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/298).

### 2024-05-23

* [*][Soil Moisture Sensor][CC2652] Calibration performed to ensure more accurate readings when the supply voltage changes.
* [*][All Chips] Pulse switch. Now, correctly restores state after power loss [(#280)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/280).
* [+][All Chips] Pulse switch. Added new settings for state on boot and when a linked button is pressed.
* [+][All Chips] Pulse switch. Added the ability to set the interval for automatic return of the logical state in milliseconds [(#262)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/262).
* [+][All Chips] Ultrasonic sensor. Added a new device model [(#274)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/274).
* [-][All Chips] CO2 concentration readings are now transmitted in the correct format.
* [+][All Chips] Added option to disable transmission of GPIO output states with periodic reports. When this option is enabled, the state is transmitted only at startup and when the state changes. This saves bandwidth, especially with numerous outputs.

### 2024-04-29

* Updated CHANGELOG.md
* [-][All chips] The previously added ultrasonic sensors were malfunctioning.
* [-][All chips] Additional options for TMP102 were not working.
* [-][All chips] Some values from devices with multiple sensors and many readings, like PZEM, might not have been reaching the coordinator.
* [-][All chips] UART sensor did not change status to "Off" when the level sensor value was set to 0.
* [*][All chips] For PZEM, the AC frequency is no longer read as a constant value.
* [+][All chips] Now, for PZEM, the firmware sends a voltage value of 0 if there is no response from the sensor (phase loss).
* [+][All chips] Now, values for current, voltage, energy, power, and CO2 are sent using standard clusters, that should improve compatibility with smart home systems. Note that the standard electricity measurement cluster is not fully supported by all tested systems. It might be more convenient to (re)create a custom converter for z2m and zha.
* [+][All chips] Added a preset for LifeControl MCLH03 socket.
* [+][All chips] Scale and shift coefficients have been added to the flower sensor firmware to adjust a result to specific conditions.

### 2024-04-06

* [-][All chips] Data from BH1750 was delayed by one report. [(#270)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/270)
* [+][All chips] Now, for endpoints, whenever possible, their type is indicated (for example, a switch or light control). This improves compatibility with some home automation systems. Those using ZHA will need to rebuild the converter after updating the firmware.
* [-][All chips] Missing clusters have been added for SCD40, PMSX003, and MHZ19.
* [*][All chips]The binding commands On/Off/Toggle are only sent for single clicks.

### 2024-04-06

* Create LICENSE
* Delete LICENSE

### 2024-03-19

* [-][CC2652] Polling for queued commands may freeze the device for several seconds.
* [-][CC2652] Some i2c sensors didn't work. [(#265)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/265)
* [-][CC2652][PSM] Device with inputs may freeze when it starts.
* [-][All chips][PSM] Sensor power control pin didn't work properly is some configurations. [(#261)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/261)
* [-][All chips][LED] It is not possible to control brightness for a non-default RGB order.
* [+][All chips] Added support for new ultrasonic range sensors (MaxSonar, URM06, URM07, JSN-sr04t and their clones). [(#267)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/267)
* [+][All chips] The separate firmware has been added for keypads. Up to 32 buttons in total. Binding and extended customization for the first 16 buttons. Power-saving mode. Everything is adjustable.
* [+][All chips] The ability to control the light level, color, and color temperature through binding has been added. Single and long clicks are supported.
* [*] Some other minor changes and improvements.

### 2024-01-14

* [*][Configurator] Fixes in ZHA converters
* [*][Configurator] Some improvements in converters for Z2M to make it compatibile with the latest version.
* [*][Configurator] Some improvements in converters for ZHA.

### 2023-12-12

* [*][All chips] Improved operation of "UART sensor" (especially when there are many in the configuration).
* [*][All chips] Improved firmware operation when "External sensor power control" is present in the configuration.
* [-][All chips] Restored operation with multiple bi-stable relays in one configuration.
* [+][All chips] Added the ability to set a divider for Waterius counters.
* [-][All chips] Sometimes, LED effects could hang.
* [*][CC2530][PSM] Improved power consumption when working with certain I2C sensors.
* [*][Configurator] Minor fixes and improvements in the configurator.

### 2023-11-17

* [*] Updated the Chinese translation.

### 2023-11-15

* [+] Added new translations
* [+] Now, you can create customer converters (quirks) for ZHA
* [+] Some other minor improvements in the firmware configuration program.
* [+] Added new translations
* [+] Now, you can create customer converters (quirks) for ZHA
* [+] Some other minor improvements in the firmware configuration program.

### 2023-11-02

* Small bugfixes related to custom converter creation for SCD40
* [All chips] Added fast reading from a single DS18B20 on the bus (useful for PSM devices).
* [All chips][Premium] Added support for air quality sensors PM1006 and PMSx003 series (not available in a СС253x router firmware).
* [All chips] Other minor fixes in the configuration program.

### 2023-09-21

* Small fixes the UART sensor protocol implementation.

### 2023-09-18

* Fixed problem related to the new UART sensor (#233, #234)

### 2023-09-15

* [All chips] Values from DS18B20 was not displayed in Z2M in some cases.
* [CC2530] Removed the CCS811 sensor from the router firmware.
* [All Chips] Fixed problem with reading MHZ19 data [(#224)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/224).
* [All Chips] Fixed problem with HX711 calibration in Z2M [(#229)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/229).
* [All chips] Now, you can configure parity and number of stop bits for UART.
* [All chips] Added the new sensor type "UART sensor" for easier data processing from an external MCU.
* [CC2652] Fixed an issue with toggling (flicking) of random real pins (even if they are not defined in a configuration) when there are virtual pins in the configuration.
* [All chips] Other minor improvements and optimizations.

### 2023-08-08

* Fixed problem with communication with multiple I2C devices on the same bus [(#217)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/217)
* The program didn't add a converter for the "Internal temperature" sensor [(#218)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/218)

### 2023-08-02

* [All chips] Fixed an issue with the auto-change function in the Pulse Switch.
* [All chips] Fixed the INA219 sensor polling issue.
* [All chips] Added support for the INA226 sensor.
* [All chips][PSM] Optimized reporting and sleep speed.
* [All chips] For the DS18B20 sensor, returned back the sensor's ID if the firmware auto-detects sensors on the bus.

### 2023-05-28

* Fixed problem with temperature sensor's values.

### 2023-05-24

* ATTENTION! This version contains changes that are incompatible with a previous version. You cannot fully use a configuration from the previous version in the new version.
* [All chips] Now, the firmware uses standard Zigbee clusters for temperature, pressure, humidity, and illuminance sensors. It improves compatibility with high-level systems like HA (probably, you'll need to (re)create a custom converter for your device in Z2M) [(#166)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/166).
* [All chips] All temperature sensors are joined into two groups: 1-wire (e.g, DHT22) and 2-wire (I2C), where a sensor type defined as a parameter. Now, the firmware does not try to detect a sensor type and uses your setting. It allows using some Chinese clones of these sensors.
* [All chips] Now, all temperature sensors are polled without detecting their presence.
* [All chips][LED] Added the CCT mode for PWM (color temperature control for the white color) [(#194)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/194).
* [CC2652P7] Added the new chip type. Advantages: more RAM and flash memory. All functions are compatible with CC2652P.
* [CC2651R] Added the new chip type. Advantages: lower power consumption and price. Disadvantages: lower RAM capacity. All functions are almost compatible with CC2652R, but the firmware for LED is limited to 200 LEDs. You can use this chip as an alternative to СС2530, but do not try to add many functions to a single module.
* [CC26XX] Added new sensors SHT40 [(#60)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/60), HDC2080 [(#101)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/101), HX711 [(#186)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/186), X9C103 [(#137)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/137).
* [All chips] Fixed a problem with saving multi-click settings to a HEX file [(#199)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/199).
* [Configurator] Fixed a problem with saving a custom converter with configurable inputs [(#204)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/204).

### 2023-02-07

* Release 2023-02-07
* [*][CC2652] Fixed problem with starting on CC2652RB. [(#176)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/176)
* [*][CC2652][OTA] Improved compatibility between PSM and OTA.
* [*][CC2652][OTA] Improved power consumption in PSM with OTA.
* [+][All chips] Added support for multi-clicks on inputs, linked to outputs where a single click changes an output state, and multi-clicks will be sent to a coordinator to execute additional actions. (#52, #169)
* [*][All chips] Small improvement in controlling a PWM output with a linked button and the selected "On/Off" mode. Now, the first long click changes the level up, and the secondary long click moves the level down. [(#152)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/152)
* [+][All chips] Added a mode when the "Pulse switch" output automatically changes the "On/Off" state after the specified interval. For example, you can now implement a motion detection sensor that resets after a time.  (#153, #174)
* [*][All chips] Other minor improvements and bug fixes. [(#172)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/172).

### 2023-01-13

* #New version release 2023-01-13
* [All chips] Added options to set minimum and maximum limits of a PWM signal (by default, 0 and 255). It can be useful if control servo motors with limited PWM pulse width [(#99)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/99).
* [All chips] Added an option to configure an offset (shift) for PWM outputs. It may help to control LED outputs with low sensitivity for short PWM impulses.
* [All chips][LED] Added a possibility to configure RGB order for WS2812B strips [(#167)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/167). By default, it is GRB.
* [All chips][LED] Added support for RGBW and RGBWW modes with color temperature control [(#168)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/168). Checked with the GledOpto bulb (look at the corresponding preset).
* [All chips][LED] Fixed color control using Hue/Saturation commands [(#163)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/163).
* [All chips][LED] All LED lamps and strips, after flashing, start switched off.
* [All chips][LED] All PWM control channels of RGB, RGBW or RGBWW lamps start at the same time. It prevents blinking of some LEDs when the lamp if off, and you connect power.
* [СС2652] Added the SCD40/41 sensor [(#81)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/81).
* [СС2652][OTA] Added support for some new flash modules [(#162)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/162).
* [All chips] Now, you can link a rotary encoder to a LED or PWM outputs and crease a versatile dimmer device [(#155)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/155).
* [All chips] Other minor fixes and improvements.

### 2022-10-20

* relese 2022-10-20
* [-][All chips][PSM] The previous version didn't send a battery state to a coordinator.
* [-][All chips] MODBUS data source didn't send data to a coordinator.
* [-][All chips] Fixed a bug in the MODBUS custom converter (recreate if you use it).
* [*][All chips] Optimized data transfer to a coordinator.
* [+][All chips][LED] Added options to define the initial state for auto bright and effect changing.
* [*][All chips][LED] Now, if auto bright changing is on, you can switch off a LED output.

### 2022-10-07

* [-][All Chips] Z2M cannot send commands to a device after coordinator restart (SLS is not affected, I didn't this problem with other coordinators).
* [-][CC2652][PSM] The device didn't sleep after the first report if the report interval was more than 30 minutes.
* [-][CC2652][PSM] Slightly reduced power consumption in sleep mode.
* [*][All Chips] The remote setting of the reporting interval has been slightly changed. Now the firmware takes a value from the maxInterval field [(#149)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/149)

### 2022-09-13

* [*][All chips][LED] Added color temperature control from a bound device or MQTT. Note: the default converter for Z2M does not support this feature.
* [-][All chips][LED] Improved visual effects remote control.
* [-][All chips][PSM] The firmware need less time to switch to the sleep state (less battery power consumption).
* [*][All chips] Improved HLW8032 support.
* [-][CC2530][LED] The configurator cannot save to a HEX file in some cases.

### 2022-09-06

* [+][All chips][LED] Added the new "LED: set active pattern" output that activates the configured effect using the "On/Off" command.
* [-][All chips][LED] The firmware didn't save the last selected color.
* [-][All chips][LED] GPIO inputs didn't work in the free version.
* [-][All chips][LED] LED strips didn't work on some pins.
* [+][All chips][LED] A linked button can be configured to change brightness or on/off of a LED strip.
* [-][All chips] The firmware didn't restore RF signal level after resetting to factory default settings.
* [*][All chips] Improved sending commands to bound devices.

### 2022-08-05

* [-][All chips] The previous version added a bug with the "Pull-down" option.
* [-][CC2652][LED] Added the missed I2C SCL output type.
* [*][CC2652] Improved periodic checking for commands in the PSM mode.
* [+] Added more checks in the configuration utility.

### 2022-08-03

* Updated README.md
* 1. Updated README.md
* 2. Improved color control in the LED firmware.

### 2022-07-21

* Big update from 2022-07-21.
* [-][All chips] I've improved sending data to a coordinator. Previously, the firmware may use all available memory and a device stopped working or disconnect from a network.
* [+][All chips] I've added a new firmware for LED supporting WS2812B LED strips, color control, color patterns and effects, and color control for LEDs with 3-channel PWM controls (RGB). More info: https://ptvo.info/zigbee-configurable-firmware-features/led-firmware/

### 2022-06-29

* [-][CC2652] Fixed problem reading 1-wire compatible sensors (i.e., DHT22).
* [+][CC2652] Added a warning message if the SBL feature is disabled in the generated firmware.
* [+] Added the "On/Off" cluster for a pulse generator.

### 2022-05-30

* [-] Single, double, triple clicks worked incorrectly in PSM mode.
* [-][CC2652] Unable to configure a report interval remotely.

### 2022-05-11

* [+][CC2652P] It is possible to configure power amplifier control pins for some non-reference boards like EBYTE E72
* [*][CC2652] Fixed memory leak in the router mode.

### 2022-05-04

* [*][PSM] Fixed and optimized a transition process when the device lost connection with a coordinator.
* [+] Added the ability to link the same virtual pin to several outputs if required.
* [*][CC2652] Now a router can report the LQI value for child devices [(#112)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/112).
* [+][CC2652] Changed to the latest SDK 6.10, which in theory should solve the problem freezed routers.
* [*][CC2652][PSM] The device did not go to sleep when communication with the coordinator was lost [(#115)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/115).

### 2022-04-07

* [-][CC2652] Binding didn't work. The device may freeze or reboot.

### 2022-04-05

* Small design fix
* [*] Watchdog timer didn't work. Please note, this timer does not work in the PSM mode at all.
* [-] Settings for a group switch not saved in the 16-channel version.
* [-][CC2530] Receiving of group commands didn't work.

### 2022-04-04

* [-] Solved problem with loading a configuration from a preset.
* [+] Add a possibility to configure a command that the firmware sends to a bound device. Early, the device sent On/Off only [(#104)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/104).
* [-] Groups didn't work properly on end devices.
* [*] Changed reading from the US100 sensor in the PSM mode. Previously, the sensor returned a wrong value after the first reading.
* [-] Resolved  a problem with editing of an endpoint list for a group switch [(#105)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/105).

### 2022-02-26

* Fixed problem with SBL for CC2652.
* Fixed problem with saving a custom converter.

### 2022-02-25

* [-]: ADC 1.15V didn't work with external power control [(#95)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/95).
* [-]: Waterius. Unable to read 2nd channel [(#97)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/97).
* [-]: internal temperature cannot be negative [(#90)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/90).
* [-]: CC2652 in router mode may become fully unresponsive [(#92)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/92). I've updated ZStack SDK from v5.10 to v5.40.
* [-]: buffer overflow when a coordinator reads an attribute value.
* [-]: CC2652P chips work only as CC2652R1 (the wrong library used when compiling firmware for CC2652P).
* [-]: The firmware didn't autodetect DS18B20 sensors if there are two or more endpoints with DS18B20.
* [+]: RF signal level configuration (initial and remote) in the Premium version through a configured sensor on an output.
* [+]: It is possible to select a role type for GPIO outputs (e.g., general GPIO, contact sensor, etc.). This feature requires a custom converter for Z2M.

### 2022-01-14

* Fixed problems with PCA9685 [(#83)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/83).
* Added "Transition time" and "Linked input" parameters similar to a standard PWM output.
* Improved the Firmware Configurator's interface. Added a horizontal scroll bar that appears if a configuration contains many parameters.
* Added loading of SBL parameters from HEX for СС2652 [(#85)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/85).

### 2022-01-10

* Added missed exposes for custom converters for HLW8032 and ultrasonic distance sensors.
* SBL is enabled by default for СС2652/CC1352.
* The old version didn't save the SBL checkbox state.
* Added a template for Sonoff 3 USB Dongle

### 2021-12-30

* Added the "Shift" parameter for ADC inputs to implement a scaling function like A*X + B.
* MHZ 19: added calibration for the span point.
* Added premium "Real-time clock" and "Cron scheduler" premium functions.
* Fixed a problem with freezing devices with many sensors and frequent reports.
* СС2652: fixed a problem with sending from UART to Zigbee with a fixed packet ending byte.

### 2021-11-26

* All changes are for СС2652
* improved signal strength for СС2652P
* fixed a problem when routers can directly bind without a coordinator

### 2021-11-21

* Small fixes related to UART.
* fixed a problem with generating a custom converter for CCS811.
* added the 5th PWM output in the Premium version for multi-channel light control.
* added low-frequency PWMs with frequencies from 4 to 480 Hz [(#32)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/32).
* For CC2530:
* fixed the problem with saving and restoring the last state for PWM outputs (#58, #72).
* added PWM on pins P03, P04, P05, P06 in the Premium version.
* the low-frequency PWM works on pins P03, P04, P05, P06, and it is incompatible with UART.
* fixed the problem with saving settings of the PA control pins to a file [(#73)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/73).
* For СС2652
* Now, it is possible to select a pull-up mode for pin 30.

### 2021-11-11

* INA219: fixed problem with converting a voltage higher than 16V.
* For CC2652
* added a possibility to use any pins for UART (look at the docs).
* fixed a bug with sending data to UART.
* fixed problem with a limited number of endpoints (not more than 5).
* fixed a delay with sending data to a coordinator in the PSM mode.

### 2021-11-04

* added rotary encode support [(#63)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/63)
* added the interlock mode [(#64)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/64)
* added ultrasonic sensors HC-SR04, US-100, and similar (#42, #51).
* For CC2652 only:
* improved RF signal level for CC2652P2 in the router mode.
* fixed a large delay problem while receiving commands from a coordinator in the EndDevice firmware.
* minor bug fixes.

### 2021-04-27

* Few improvements in PWM. Now, you can set a transition time between states and select a linked button's mode.
* Improved the power-saving mode. I've confirmed that a sensor may consume 1 µa and 0.4µa if there are no periodic reports.
* UART allows you to set a custom data packet's delimiter.
* Fixed a bug in Pulse Switch.
* Improved an RF signal level in chips without an amplifier.

### 2021-03-22

* Added sensors HTU21D, HDC1080, SHT20, SHT30, SHTC3.
* Improved the I2C interface
* Counter: added options to select a debounce interval for fast and slow counters.
* Counter: you can set any initial value remotely.
* Added virtual pins (P30-P37) that you can use in your configuration (for example, for internal temperature or voltage sensors). Therefore, you can use real pins on a chip for other purposes.
* Fixed problem with a wrong internal temperature in PSM.

### 2021-02-15

* Improved code for INA219, INA3221 sensors. Added the inverted mode for hardware PWM.

### 2021-01-14

* Added ACS758. Control of PWM outputs with switch inputs. Status LED modes. Added a scale factor for ADC. Minor bugfixes.

### 2020-11-13

* Added version number to the configuration utility [(#9)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/9)
* Fixed problem reading some settings from a HEX file [(#10)](https://github.com/ptvoinfo/zigbee-configurable-firmware/issues/10)

### 2020-10-29

* Added firmware for end devices (without routing).

### 2020-08-31

* Fixed a problem with the restoring of a saved state for inverted pins.
* Added the possibility to create four hardware PWM.

### 2020-08-08

* Initial uploading

