---
title: Electronics Notes
category: "notes"
cover: electronics_thumbnail.jpg
---


microprocessor
- basically a typical computer with GPIO pins that allow for fun stuff
- used in applications where intense processing is required
- used for a large variety of not predefined tasks
- it runs an operating system
- separate CPU, ROM, RAM, Serial Interface, Timers, I/O ports connected externally
- high computational power
- higher cost 
- higher power consumption
- example: raspberry pi

microcontroller
- designed for a specific task, task to be performed in predefined
- all elements (CPU, ROM, RAM, Serial Interface, Timers, I/O ports) required for a specific task are limited and therefore integrated in a single chip
- much smaller
- lower cost
- lower power consumption
- example: arduino
- arduino features
    - real time operating system
    - a simple two part programable interface
        - setup()
        - loop()
    - built in analog to digital converter, useful for analog signals

lighting sensors tend to be analog
- need analog to digital converter

circuit — Your circuit is the collection of all the connections you’ve made, using wires, resistors, LEDs, buttons, GPIO and other pins, etc. It can be closed (like when you press a button, and a signal is able to traverse from one end to the other), or it can be open (a button is not pressed, or there’s some other break in the circuit).

high/low (in the context of raspberry pi) — GPIO pins have two states, you can call them on or off, high or low, 1 or 0, etc. A pin is set "high" when it's outputting 3.3v or reading in 3.3v (fit’s 5V for arduino, otherwise specified for other electronics), and "low" when it's off. The python GPIO library calls these two states GPIO.HIGH and GPIO.LOW, and the library also helps you determine which state a pin is in.

Rising Edge — The moment a GPIO pin changes to a HIGH state.

Falling Edge — The moment a GPIO pin changes to a LOW state.

Bouncetime — You can specify a time during which repeat events will be ignored. For example, you can specify a bouncetime of 500 ms. That means that if you press a button multiple times in under half a second (or maybe the button's a bit loose and registers a click multiple times), subsequent clicks after the first one will be ignored.

Output — Pins can be set to read input or send output, but not both at once. If a pin is set to output, the Pi can either send out 3.3 volts (HIGH), or not (LOW or 0 volts).

Input — If a pin is set to input, then the circuit must be closed for it read that input. In my case, that means pressing the button down in order to read HIGH or 1 (since I'm connected to 3.3v... if my pin were connected to ground, it'd read LOW or 0 when closed).

Floating — When you should be using a pull down or pull up resistor, but aren't, the status is said to be "floating". That is, the pin and any wires connected to it pick up on random radiation and electromagnetic signals from the environment. When the circuit is open, it's not HIGH or LOW, but somewhere in between.

Pull Down — When you have a circuit that connects 3.3v to a GPIO pin, it'll read HIGH when the circuit is closed. When it's open, it could read anything. You need a "pull down" resistor connecting your circuit to ground, so that it reads LOW when the circuit is open. 

Pull Up — Similarly, if you have a circuit connecting your GPIO pin to ground when it's closed, it'll read LOW. You need a "pull up" resistor so that, when it's open, it defaults to the HIGH state.

resistor — think restrictor of current, limits the current flow,  usually to safeguard components.  

voltage — think pressure of electricity.

current — think flow of electricity. 

capacitor — stores charges and only lets out a bit.

diode — allows current to flow in one direction but not another.

driver circuit — They are usually used to regulate current flowing through a circuit or to control other factors such as other components, some devices in the circuit. An example would voltage regulator that keeps an attached component operating within a broad range of input voltages.

voltage regulator — a system designed to automatically maintain a constant voltage level.

gain — in electronics is the measure of the ability of a two port circuit to increase the power or amplitude of a signal from input to the output port by adding energy converted from some power supply to the signal. Can apply to voltage gain, current gain, and power (energy) gain.

open drain output - it is very common in integrated circuits for an output to be open drain. Open drain outputs require pullup resisters in order for the output to be able to properly output high. Otherwise the output pin can only output either low (ground) or float (undefined).