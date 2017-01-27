# SilentStepStick
The Silent-Step-Stick is a Stepper Motor Driver Board for 2-Phase Motors based on a [Trinamic TMC 2100](http://www.trinamic.com/products/integrated-circuits/details/tmc2100/), [Trinamic TMC 2130](http://www.trinamic.com/products/integrated-circuits/details/tmc2130/) or [Trinamic TMC2208](http://www.trinamic.com/products/integrated-circuits/details/tmc2208-la/).
The driver boards are hardware compatible with [StepStick](http://reprap.org/wiki/StepStick) and [Pololu A4988](https://www.pololu.com/product/1182).

SilentStepStick          | TMC2100 (5V) | TMC2100 (3-5V) | TMC2130 (3-5V) | TMC2208 (3-5V)
------------------------ | ------------ | -------------- | -------------- | --------------
                         | [![SSS](https://github.com/watterott/SilentStepStick/raw/master/hardware/SilentStepStick_v12_5V.jpg)](http://www.watterott.com/en/SilentStepStick-TMC2100-5V) | [![SSS](https://github.com/watterott/SilentStepStick/raw/master/hardware/SilentStepStick_v12.jpg)](http://www.watterott.com/en/SilentStepStick) | [![SSS](https://github.com/watterott/SilentStepStick/raw/master/hardware/SilentStepStick-TMC2130_v10.jpg)](http://www.watterott.com/en/SilentStepStick-TMC2130) | *coming soon...*
Interface                | Step/Dir     | Step/Dir       | Step/Dir or [SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus) | Step/Dir
Configuration            | CFG Pins     | CFG Pins       | CFG Pins or [SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus) | CFG Pins or [UART](https://en.wikipedia.org/wiki/UART)
Native Microsteps*       | up to 1/16   | up to 1/16     | up to 1/256    | up to 1/256
microPlyer Microsteps    | 1/256        | 1/256          | 1/256          | 1/256
Logic Voltage ```VIO```  | 5V           | 3 - 5V         | 3 - 5V         | 3 - 5V
Motor Voltage ```VM```   | 4.75 - 46V   | 5.5 - 46V      | 5.5 - 46V      | 5.5 - 36V
Motor Phase Current      | 1.2A RMS     | 1.2A RMS       | 1.2A RMS       | 1.2A RMS
```VM``` always needed** | no           | yes            | yes            | yes
Internal V-Regulator**   | disabled     | enabled        | enabled        | enabled
RDSon                    | >=0.5 Ohm    | >=0.5 Ohm      | >=0.5 Ohm      | <=0.3 Ohm
stealthChop (quiet)      | yes          | yes            | yes            | yes
spreadCycle              | yes          | yes            | yes            | yes
coolStep                 | no           | no             | yes            | no
stallGuard               | no           | no             | yes            | no
dcStep                   | no           | no             | yes            | no

_* without interpolation (microPlyer), ** further infos [here](https://github.com/watterott/SilentStepStick/blob/master/docu/FAQ.md#what-is-the-difference-between-silentstepsticks-with-3-5v-and-5v-logic-voltage)_


## Shop
* Trinamic **TMC2100** based drivers, recommended for most applications (CFG pins for configuration)
  * [TMC2100 SilentStepStick (3-5V logic voltage)](http://www.watterott.com/en/SilentStepStick)
  * [TMC2100 SilentStepStick (3-5V logic voltage) with soldered Pin Headers](http://www.watterott.com/en/SilentStepStick-with-Pins)
  * [TMC2100 SilentStepStick (5V logic voltage)](http://www.watterott.com/en/SilentStepStick-TMC2100-5V)
  * [TMC2100 SilentStepStick (5V logic voltage) with soldered Pin Headers](http://www.watterott.com/en/SilentStepStick-TMC2100-5V-with-Pins)
* Trinamic **TMC2130** based drivers (CFG pins or SPI for configuration)
  * [TMC2130 SilentStepStick (3-5V logic voltage)](http://www.watterott.com/en/SilentStepStick-TMC2130)
* Trinamic **TMC2208** based drivers (CFG pins or UART for configuration)
  * *TMC2208 SilentStepStick coming soon...*
* Accessories
  * [SilentStepStick Protector (with flyback diodes)](http://www.watterott.com/en/SilentStepStick-Protector)
  * [Suitable Heatsink 10x10mm](http://www.watterott.com/en/Pin-heatsink-square-ICK-S-10-x-10-x-125)
  * [Suitable Heatsink 10x6mm](http://www.watterott.com/en/Heatsink-for-DIL-IC-PLCC-und-SMD-10-x-6-mm)
  * [Suitable Heatsink 8x6mm](http://www.watterott.com/en/Heatsinks-6-3x8mm)


## Features
* Hardware compatible with [StepStick](http://reprap.org/wiki/StepStick) and [Pololu A4988](https://www.pololu.com/product/1182)
* Components on bottom PCB side for better heat emission, further infos [here](https://github.com/watterott/SilentStepStick/blob/master/docu/FAQ.md#why-is-the-tmc2100-chip-on-the-bottom-pcb-side)
* Trinamic stepper motor driver (chopper drive / constant current drive)
* Step/Dir interface with up to 256 microsteps and interpolation
* Motor current: up to **1.2A RMS** continuously (active cooling required)
* **microPlyer** - microstep interpolator for increased smoothness of microstepping
* **stealthChop** - for quiet operation and smooth motion
* **spreadCycle** - highly dynamic motor control chopper
* Extra features of **TMC2130**:
  * SPI configuration interface (up to 4MHz)
  * up to 256 native microsteps (without interpolation)
  * **coolStep** - current control for energy savings
  * **stallGuard** - sensorless motor load detection
  * **dcStep** - load dependent speed control


## Hardware and Software
* [FAQ (Frequently Asked Questions)](https://github.com/watterott/SilentStepStick/blob/master/docu/FAQ.md)
* [Schematics + Layout](https://github.com/watterott/SilentStepStick/tree/master/hardware) (PDF files include additional infos)
* [Arduino Examples](https://github.com/watterott/SilentStepStick/tree/master/software)
* [Eagle CAD Part](https://github.com/watterott/Eagle-Libs)


## Reviews and Tests

* Review from Thomas Sanladerer

  [![SilentStepStick/TMC2100 Review](http://img.youtube.com/vi/g6Bxoqr8QlY/0.jpg)](https://www.youtube.com/watch?v=g6Bxoqr8QlY)

  [![SilentStepStick/TMC2100 Review Update](http://img.youtube.com/vi/mYuZqx8xwTg/0.jpg)](https://www.youtube.com/watch?v=mYuZqx8xwTg)

* Review from Peter Recktenwald

  [![SilentStepStick/TMC2100 Review](http://img.youtube.com/vi/P3ebhi-vZRY/0.jpg)](https://www.youtube.com/watch?v=P3ebhi-vZRY)

* Review from Georg Mill

  [<img src="http://blog.georgmill.de/wp-content/uploads/2015/06/steppermotor_intro.jpg" width="400" height="225">](http://blog.georgmill.de/2015/06/18/schrittmotor-test-5-treiber-im-vergleich/)

* Review from Moritz Walter

  [<img src="https://hackadaycom.files.wordpress.com/2016/09/tmc_thumb1.jpg" width="400" height="400">](http://hackaday.com/2016/09/30/3d-printering-trinamic-tmc2130-stepper-motor-drivers-shifting-the-gears/)

* What is Trinamic spreadCycle and stealthChop?

  [![Trinamic spreadCycle and stealthChop](http://img.youtube.com/vi/Q0sJlGh9WNY/0.jpg)](https://www.youtube.com/watch?v=Q0sJlGh9WNY)

* What is Trinamic stallGuard and coolStep?

  [![Trinamic stallGuard and coolStep](http://img.youtube.com/vi/Prw7wNa20Gk/0.jpg)](https://www.youtube.com/watch?v=Prw7wNa20Gk)

* More Tests and Reviews on [YouTube](https://www.youtube.com/results?search_query=SilentStepStick)
