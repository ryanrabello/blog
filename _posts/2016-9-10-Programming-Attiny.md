---
layout: post
title: Programming ATtiny chips with arduino IDE v 1.6 on OSX
author: Ryan Rabello
---

A few days ago I found a ATtiny2313 lying around my home. For a while now I've been working on a project that I wanted to convert from breadboard to PCB.  I thought that this IC would be a great chip to do just that.

##### Ingredients
* **Arduino Uno** (you can use any of the other boards supported by the [Arduino ISP](https://www.arduino.cc/en/Tutorial/ArduinoISP))
* **ATtiny2313** (you can use any other ATtiny chip that is supported by the [arduino-tiny](https://code.google.com/archive/p/arduino-tiny/) library.)
* **10 μF Capacitor** (if your using an Arduino Uno)

##### Arduino ISP
**1.** Plug in your arduino that you want to use to program the ATtiny.

**2.** Select the board you are using from the dropdown `Tools -> Board`.

**3.** Open the the example sketch 'ArduinoISP' from `File -> Examples -> ArduinoISP`.

**4.** I used an older tutorial so the wiring is a bit different for my chip, so I told the Arduino to use the old pins with the following line of code.

```c++
#define USE_OLD_STYLE_WIRING true
```

I put it right under the `#define PROG_FLICKER true` snippet of code.

**5.** Compile and upload the program to the arduino.

**6.** Connect the 10μF Capacitor with the negative side to the arduino with the negative side to ground and the other side to reset.

##### Setup Arduino IDE
**1.** Download the arduino-tiny library [here](https://code.google.com/archive/p/arduino-tiny).

**2.** Follow the instructions in the README to the T.

**3.** I got a couple of errors after setting up the arduino tiny library. Save yourself an hour of googling with the list below.

* If your getting an error about the location of the `emptyXXXX.hex` file you may need to move all the files in `bootloaders/empty` to `bootloaders`. The bootloaders folder should be located at `~/Documents/Arduino/hardware/tiny/avr`
* I got an error like this `"avr-g++": executable file not found in $PATH` and fixed it by adding the line `compiler.path={runtime.tools.avr-gcc.path}/bin/`to the `platfrom.txt` under the line that lies and looks like `# Default "compiler.path" is correct...`. Thank you [tutorial](http://www.technoblogy.com/show?190D).

##### Connect and Program the ATtiny
**1.** Connect the ATtiny to the arduino according to the following diagram.
![arduino to ATtiny diagram](http://www.ernstc.dk/arduino/2313.png)
This picture was found in [this tutorial](http://www.ernstc.dk/arduino/2313.htm).

**2.** Open the blink sketch `Files -> Examples -> Basics -> Blink` or whatever sketch you would like to upload. (be aware of the limited memory capacity of these smaller chips.

**2.** Select the correct ATtiny device from `Tools -> Board` the board I used is the `ATtiny2313 @ 1MHz`. (See the arduino tiny setup if you don't see the ATtiny that you have.)

**3.** Select `Tools -> Programmer -> Arduino as ISP`. (Don't spend 30 minutes having the programmer set to 'ArduinoISP'. Your welcome)

**4.** Upload your sketch using `Sketch -> Upload using programmer`. (The IDE should understand what you are trying to do and it may work if you just use the normal upload button).

##### YAY!! Blinking light

I was really excited to be able to program the chip but I immediately began running into issues. First of all the memory available of on the ATtiny2313 is really puny (2kb). Then the Arduino library takes up about half of that so you only have a little bit left for programming. Furthermore the ATtiny2313 processor doesn't support `analogread()` (which doesn't really make sense because it has a comparator and two analog in pins). Regardless I would recommend another type of ATtiny chip for any projects that use analog functionality.
