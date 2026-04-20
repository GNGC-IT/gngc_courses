# Electrical Foundations & High-Power Actuation

**Focus:** Ohm's Law, Power, and Relays 
**Goal:** Students understand _why_ microcontrollers need help driving heavy loads and learn to wire a relay safely.

## Lesson 1: Ohm's Law & Microcontroller Limits**
    

> [!hint] Ohm's Law
> - Ohm's Law ($V = I \times R$) - Voltage is equal to Current times Resistance
> - Power ($P = V \times I$).

### **The Problem** 

When you break down the [[Project Two - Smart Watering System]] assessment, you'll see that you're required to ensure that the power systems of your project are accuratly calculated in order to ensure the arduino doesn't..._blow up_. Microcontrollers have very specific power requirements to ensure that their onboard systems get exactly the current they need, but also they are designed to have a very low power draw to be as efficient as possible. Throwing a 5 - 12V DC motor into the mix, or devices that use _inductive load_ isn't good for our little microcontrollers, and this care for understanding current also applies to the inputs and outputs we use in our projects.

> [!note]- Examples of Current Needs
> - LEDs - Rated for a max of 20mA _(that's milliamps)_
> - DHT11's - 0.3mA to 2.5mA
> - The Arduino itself generally allows for up to 40mA from a single I/O and a max of 200mA across the entire circuit!

**Enter, Ohm's Law! **

There are a few fundamental laws about circuit’s that we can use to analyse circuits for troubleshooting and during the design process. Ohm’s Law is one of these! It states that _“the electric current through a conductor between two points is directly proportional to the voltage across the two points.”_  

![[ohms_triangle.png]] 
_(image as stolen from:_ [Electronic's Tutorials](https://www.electronics-tutorials.ws/dccircuits/dcp_2.html))

A couple of words to explain there. **Proportional** is a fancy way of saying "equals to".  What this means is, your voltage should be equal to the current in your circuit, times any resistance in the circuit. _Remember that energy cannot be created or destroyed? Well, here it is._ Want to make sure your LED is only getting the current it needs? Use Ohm’s Law to get the right level of resistance in your circuit!

To test your understanding of Ohm’s Law, try to calculate the current of a 12V circuit with two 330Ω resistors manually, and then use a [calculator](https://www.allaboutcircuits.com/tools/ohms-law-calculator/) to confirm your findings.

### Challenge 
Calculate the current draw of a 5V DC pump vs. the maximum output of an Arduino digital pin (~40mA). Prove mathematically that wiring a pump directly to the board will fry the microcontroller.



## Lesson 2: Isolation & Relays
    
**Theory (T-Course Focus):** Introduce inductive loads and mechanical/optical isolation. Explain how a relay uses a tiny electromagnet (Arduino side) to pull a high-power physical switch (Pump side).
        
**Practical:** Wire a 5V Relay module. Write a basic script to make the relay "click" on and off every 5 seconds.

```
const int relayPin = 4; // Pin connected to the relay IN pin

void setup() {
  pinMode(relayPin, OUTPUT);
  // Keep relay OFF initially (assuming active-low module)
  digitalWrite(relayPin, HIGH); 
}

void loop() {
  digitalWrite(relayPin, LOW);  // Turn relay ON
  delay(2000);                 // Wait 2 seconds
  digitalWrite(relayPin, HIGH); // Turn relay OFF
  delay(2000);                 // Wait 2 seconds
}
```

## Lesson 3: WHS & "Wet Zone" Briefing
    
**Theory:** Risk Assessment matrix for "Project Oasis". Brainstorm the hazards of mixing conductive liquids (water) with electronics.
        
**Practical:** Establish class rules for the "wet zones" (e.g., Arduinos must be elevated, pumps submersed before power is applied).