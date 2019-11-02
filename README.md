# Lock Controller - Hardware - WIP

This is a **Work In Progress**.

This the hardware design for a simple bluetooth-enabled lock controller device. It is a KiCad project.

The software for this device is in a [separate repo](https://github.com/jpablo128/lockcontroller-software).

This system is based on the AT90S2313, a very old and unsupported part (it's probably easy to redesign it for a similar, more modern alternative, like the attiny2313).


## Description
The system will allow to control a simple sliding lock using bluetooth. We will reuse parts from an old CD-drive, namely the stepper motor and the linear drive (mechanics that convert the rotary motion into linear motion). Other hardware parts present in the system:

- a toggle switch, to manually cause the lock to open or close.
- two infrared slot switches, to detect the end positions of the lock.
- two leds, one red and one green, to indicate if the lock is open or closed (stationary), or opening or closing (blinking).
- the bluetooth module (to be determined).


The at90s2313 pins are used as follows:

- Pin  2: RXD (connected to TXD of BT module or arduino)
- Pin  3: TXD (connected to RXD of BT module or arduino)
- Pin  6: INT0/PD2 push button (toggle open/close)
- Pin  8: PD4: input IR barrier 1
- Pin  9: PD5: input IR barrier 2
- Pin 12: PB0, motor control W2-0 (W=winding) these really go to the L293
- Pin 13: PB1, motor control W2-1
- Pin 14: PB2, motor control W1-0
- Pin 15: PB3, motor control W1-1
- Pin 16: PB4: output enable/disable L293
- Pin 17: PB5: green led output
- Pin 18: PB6: red led output

An L293D quad half h-bridge IC is used to drive the motor.

The mechanical bounce of the switch will be eliminated by software.

The system is supposed to allow receiving commands through the serial port. Ultimately, this will be done with a Bluetooth module, so the lock can be remote-controlled. During development, however, it should be possible to test the serial connection with an Arduino.

## Current version
Only the tentative schematic is done at this point. The different parts of the circuit are being  tested on the test board.

## Notes
On the test board, the basic circuit works without capacitors connected to the crystal. We should be using 18pF to 22pF capacitors (the avr doesn't work at all with bigger capacitors).
