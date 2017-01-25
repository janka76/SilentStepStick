# Frequently Asked Questions

## Is the SilentStepStick 100% compatible with a StepStick or Pololu A4988?
The SilentStepStick is hardware/pin compatible with StepStick and Pololu A4988 drivers.
However the TMC2100 has different and more settings, which can be set via the CFG/MS pins and the **DIR pin is inverted** (direction).
The TMC2100 config pins also know three states: low (GND), high (VIO) and open (unconnected).
[SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus) is used on the TMC2130 for the configuration and so the controller board must have SPI on the CFG pins.


## What is the difference between SilentStepSticks with 3-5V and 5V logic voltage?
The SilentStepSticks with a variable logic voltage (VIO) of 3-5V use the internal linear regulator of the TMC21x0 to generate from the motor voltage (VM) a 5V voltage for the internal digital and analog circuit (about 20mA).
Because it is a linear voltage regulator the power dissipation depends on the motor voltage (high motor voltage = high power dissipation/heat).
The 5V logic SilentStepSticks do not use the internal voltage regulator of TMC21x0 and therefor only a 5V supply voltage for VIO is possible and VM has not to be present before VIO.
Further infos about power-up and down can be found [here](https://github.com/watterott/SilentStepStick/blob/master/docu/FAQ.md#what-to-consider-when-turning-the-power-supply-on-or-off).

Power dissipation of the internal voltage regulator:
* 0.1W @ VM=12V
* 0.3W @ VM=24V
* 0.6W @ VM=36V
* 0.8W @ VM=45V


## Where can I find more information on the settings and operation modes?
More information can be found in the [SilentStepStick schematics](https://github.com/watterott/SilentStepStick/tree/master/hardware) and [TMC2100 datasheet](http://www.trinamic.com/products/integrated-circuits/details/tmc2100/) / [TMC2130 datasheet](http://www.trinamic.com/products/integrated-circuits/details/tmc2130/).

For most cases the **1/16 stealthChop** mode (CFG1=open, CFG2=open, CFG3=open) is suitable.
If you have problems like step losses then you can use a higher current setting in stealthChop with automatic power-down (open/unconnected EN pin)
or you can use the more powerful **1/16 spreadCycle** mode (CFG1=GND, CFG2=open, CFG3=open).

#### Infos and Installation Guides for 3D Printers
* [General (English)](http://reprap.org/wiki/TMC2100)
* [General (German)](http://reprap.org/wiki/TMC2100/de)
* [General (French)](http://reso-nance.org/wiki/materiel/silentstepstick/accueil)
* [General (Russian)](http://3deshnik.ru/blogs/akdzg/chto-zhe-delat-belami-tmc2100)
* [General (Japanese)](http://3dp0.com/silentstepstick)
* [Assembly Guide (English)](https://www.youtube.com/watch?v=L2xNXTQO8xc)
* [RAMPS (English)](http://www.instructables.com/id/Install-and-configure-SilentStepStick-in-RAMPS-TMC/)
* [Ultimaker UMO + TMC2100 (English)](https://ultimaker.com/en/community/11571-step-by-step-installation-of-silentstepstick-drivers-on-umo)
* [Ultimaker UMO + TMC2130 (English)](https://ultimaker.com/en/community/20090-step-by-step-installation-of-sss-tmc2130-on-umo)

#### Boards with USB Power Supply
Only applicable for SilentStepSticks with variable 3-5V logic voltage (VIO):
If you use a control board with USB power supply (like Arduino + RAMPS) then always ensure that the motor voltage (VM) is present, when you connect the board via USB.
Otherwise the TMC21x0 is not powered via the internal voltage regulator and a high current can flow into VIO or the IOs and this can damage the internal logic.
As safety workaround you can disconnect the 5V signal in the USB cable, so that the board cannot be powered over USB.

#### RAMPS 1.4 and RUMBA Notes
If you remove all jumpers (or open all switches) for MS1+MS2+MS3, then the SilentStepStick TMC2100 driver will be in 1/16 spreadCycle mode (CFG1=GND, CFG2=open, CFG3=open), because there is a pull-down resistor on MS1 on the RAMPS.
But if you have not an original [RAMPS 1.4](http://reprap.org/wiki/RAMPS_1.4) or [RUMBA](http://reprap.org/wiki/RUMBA), then your schematics can be different and you have to check the MS-Pin configurations on you board.
We recommend the TMC2100 SilentStepStick with 5V for RAMPS and RUMBA boards, because they use 5V logic.


## How to set the stepper motor current?
The best way to set the motor current is by measuring the voltage on the ```Vref``` pin (0...2.5V) and
adjusting the voltage with the potentiometer.
The maximum motor current is 1.77A RMS and is set via the 0.11Ohm sense resistors.

```Irms = (Vref * 1.77A) / 2.5V = Vref * 0.71```

```Vref = (Irms * 2.5V) / 1.77A = Irms * 1.41 = Imax```

```Vref``` -> Voltage on Vref pin (TMC21x0 pin 23 AIN_IREF)

```Irms``` -> RMS (Root Mean Square) current per phase (Irms = Imax / 1.41)

```Imax``` -> Maximum current per phase (Imax = Irms * 1.41)

**Example:**
A voltage of 1.0V on Vref sets the motor current to 0.71A RMS.

**Note:**
On some stepper motor drivers the maximum current (e.g. A4988) is set via Vref and on others the RMS current (e.g. TMC2100).
The TMC21x0 has an automatic thermal shutdown if the driver gets to hot.


## What to consider when turning the power supply on or off?
**Power on:**

*SilentStepSticks with variable 3-5V logic voltage:*
The motor voltage VM should come up first and then the logic voltage VIO, because the internal logic of the TMC21x0 driver is powered from VM.

*SilentStepSticks with 5V logic voltage:*
There is no special power up sequence needed.

Only after the logic voltage VIO is present and stable, the driver inputs (STEP, DIR, EN, CFG1...) can be driven with a high level.

A step pulse (moving) should only be done after the motor voltage VM is present and stable.

Because the motor voltage VM is a strong power supply with a high voltage, also ensure that there cannot occur voltage spikes on power up.
See [Pololu: Understanding Destructive LC Voltage Spikes](https://www.pololu.com/docs/0J16/all).

**Power off:**

*SilentStepSticks with variable 3-5V logic voltage:*
The logic voltage VIO should turned off at first and then the motor voltage VM, because the internal logic of the TMC21x0 driver is powered from VM.

*SilentStepSticks with 5V logic voltage:*
There is no special power off sequence needed.

If the motor is running/moving, then it is not allowed to switch off the power supply. Always make sure that the motor stands still on shutting down, otherwise the TMC21x0 driver can get damaged.

An **emergency stop** can be realized, when the EN/CFG6 pin is set to VIO (high). This will switch off all power drivers and will put the motor into freewheeling.
See also: [SilentStepStick Protector with flyback diodes](https://github.com/watterott/SilentStepStick#shop)


## The motor makes noise in spreadCycle mode when it is not moving?
A motor supply voltage of 12V is in most cases to low and in general the sound gets quieter if the motor supply voltage is above 18V.


## How to control the TMC21x0 stepper motor driver?
The SilentStepStick has a normal step+direction interface.
You set the direction with the DIR pin and on every pulse on the STEP pin the motor will move one step.
Here you can find an [Arduino example](https://github.com/watterott/SilentStepStick/tree/master/software) and [Arduino library](http://www.airspayce.com/mikem/arduino/AccelStepper/) (interface=DRIVER).


## Is it possible to connect the CFG pins from different SilentStepSticks?
It is possible to connect the CFG pins from two or more driver boards.
However then the pin state can only be GND (low) or VIO (high). The open state (unconnected) is not possible in this configuration.


## Why is the TMC2100 chip on the bottom PCB side?
The TMC2100 or TMC2130 chip has a thermal pad on the bottom which is soldered to the PCB.
So the thermal resistance via the chip bottom is better than via the top.
That is why the chip is on the bottom PCB side.
A heat sink can be placed directly on the PCB.
Further infos [here](https://www.youtube.com/watch?time_continue=145&v=mYuZqx8xwTg).
