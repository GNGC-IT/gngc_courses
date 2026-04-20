# Unit 1 Terms

**Actuator** A component of a machine that is responsible for moving and controlling a mechanism or system, such as the water pump or servo motor in the Smart Planter.

**Brownout** An intentional or unintentional drop in voltage in an electrical power supply system. In microcontrollers, this can cause the system to reset or behave unpredictably.

**Kirchhoff’s Laws** Fundamental laws in circuit analysis.

- **Current Law (KCL):** Total current entering a junction equals the total current leaving.
    
- **Voltage Law (KVL):** The sum of all electrical potential differences around any closed loop is zero.

**Input** - sensors or systems which give information _to_ the microcontroller.

**MCU (Microcontroller Unit)** A small computer on a single integrated circuit (e.g., Arduino or ESP32) that serves as the "brain" of the automated system, reading sensors and controlling actuators.

**Non-blocking Code** A programming technique (often using `millis()` instead of `delay()`) that allows a program to continue running other tasks while waiting for a specific time interval to pass.

**Ohm’s Law** A formula used to calculate the relationship between voltage (V), current (I), and resistance (R) in an electrical circuit: $V = I \times R$.

**Output** Systems which are given instructions from the Arduino to perform actions and/or provide feedback to a user. (e.g. Servos, Screens, Motors, LEDs)

**PWM (Pulse Width Modulation)** A method of reducing the average power delivered by an electrical signal by effectively chopping it up into discrete parts. Commonly used to control motor speeds or LED brightness.

**Threshold** The specific value at which a programmed action is triggered (e.g., "If soil moisture drops below 30%, turn on the pump").