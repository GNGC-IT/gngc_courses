# Assessment Task 3: The Mechanical Systems Project

![[Copy of Robotics Banner (600 x 200 px).png]]

**Course:** Robotics & Mechatronics (Combined T & A)  
**Unit:** Unit 3 (Robotic and Mechatronic Systems)  
**Task Type:** Practical Project (Product & Mechanical Systems Focus)

## 1. Context: How this fits into our Course

- **Systems Thinking:** You will move beyond simple input-output logic to manage a "system of systems"—where mechanical energy, electronic sensing, and computational logic must synchronise perfectly.
    
- **Mechatronic Integration:** Part of the course is looking at the interaction between mechanical, electrical, and computer systems. We have focused a lot on the eletrical and computer aspects, now it's time for the mechanical.
    
- **Problem Solving in Context:** By using a "Drive" (gravity/elastic) separate from the "Control" (Microcontroller), you are emulating industrial automation where controllers monitor independent physical processes.

## 2. Project Overview

In this assessment, you will explore the intersection of classical mechanics and modern electronic control. You are tasked with designing and constructing a **Mechanical Narrative**—a system that uses stored energy (gravity, elastic, or fluid) to drive a series of complex mechanical movements, all while being monitored and regulated by a microcontroller system (**Arduino** or **Raspberry Pi Pico**).

### The Design Challenge

Select one of the following scenarios to base your project on:

- **Option 1: The Automaton Stage:** A miniature theatrical display where scenery and characters move in a timed sequence driven by a falling weight (gravity drive).
    
- **Option 2: The Kinetic Rube Goldberg:** A chain-reaction machine that performs a simple task (e.g., ringing a bell or turning a page) through a series of complex mechanical transitions.
    

## 3. Technical Requirements

### 3.1. Mechanical Systems (The "Drive")

Your machine must demonstrate at least **three** different mechanical principles from the following list:

- **Gearing:** Spur, bevel, or worm gears to change speed or torque.
    
- **Linkages:** Four-bar linkages or sliders to convert rotational motion to linear motion.
    
- **Cam & Follower:** To create custom intermittent motion paths.
    
- **Escapements:** To regulate the release of energy (essential for timed narratives).
    

### 3.2. Control Systems (The "Logic")

You must integrate either an **Arduino Uno** or a **Raspberry Pi Pico** to add "intelligence" to your mechanical system. The microcontroller must:

- **Monitor:** Use at least two sensors (e.g., IR break-beams, limit switches, or ultrasonic sensors) to detect the machine's progress.
    
- **React:** Provide feedback via an output device (e.g., an LCD status screen showing "Act 1 Complete", an RGB LED safety indicator, or a solenoid emergency brake).
    
- **Energy Harvesting (Extension):** Use a DC motor as a generator to measure the voltage produced by your machine's motion and display and/or use the energy safely.
    
## 4. Task Conditions

- **Duration:** 6 weeks of in-class time.
    
- **Mode:** Individual or Groups (Max 3). _Note: Pairs must submit separate Evidence Guides detailing their specific individual contributions._
    
- **Resources Provided:** * Access to 3D printers, laser cutters, and hand tools.

    - Arduino Uno/Raspberry Pi Pico and a standard sensor kit.
        
    - Recycled materials and scrap timber for chassis construction.
        
- **Physical Constraints:** * The machine footprint must not exceed 600mm x 600mm.
    
    - Maximum energy input: 2kg falling mass or 50N spring tension.
        
- **Integrity:** All code must be authored by the student. Any use of library code or external frameworks must be explicitly cited in the Evidence Guide.
    
- **Safety (WHS):** A basic risk assessment must be signed off by the teacher before any "energy release" tests occur. High-tension springs and heavy weights require safety shielding or tethering.

## 5. What Counts As Evidence (Submission)

**Due:** Physical Project must be handed in at the Lab before 3:30pm on _Tuesday, 2nd of June_. Digital Work is due on the same day before _10pm_

To prove your learning in practical application, you must submit:

1. **The Physical Prototype:** The full system contained within the dimension requirements.
2. **The Source Code:** Your `.ino` or `.py` file (or Arduino Online Link) submitted to Google Classroom (Evidence of your control structures and logic)
3. **Video of your working prototype:** In case of issues with the build or final construction, you are strongly recommended to include a video of the operational prototype.
4. **Project Description:** Some documentation about your build, operating instructions and a breakdown of its functionality.
    
## Rubric

|Criteria|A (Excellent)|B (High)|C (Satisfactory)|D (Partial)|E (Minimal)|
|---|---|---|---|---|---|
|**Physical Build & Structural Integrity**|Construction is exceptionally robust and professional. Minimal vibration; precise alignment of all components. Uses customised or optimised mounting.|Construction is stable and durable. Components are secured firmly. Layout is clean with logical placement of modules.|Build is functional but may have minor stability issues. Components are mostly secured using standard methods.|Build is fragile or unstable. Components are loosely attached or poorly positioned.|Construction is incomplete or fails to support the intended function.|
|**Mechanical Systems & Use of Motion**|Sophisticated use of mechanical advantage (gears, linkages, pulleys). Motion is smooth, efficient, and calibrated for specific torque/speed requirements.|Effective use of mechanical systems. Movement is consistent. Choice of mechanical components aligns well with task requirements.|Basic mechanical systems are functional. Movement is achieved but may be inefficient or jerky.|Minimal mechanical complexity. Relies on simple direct drive with little consideration for load or friction.|Mechanical systems fail to operate or show no evidence of design.|
|**Electronic Integration (Circuits)**|Circuits are expertly designed with clean cable management. Uses appropriate protection (resistors, diodes). Soldering/wiring is of professional standard.|Circuits are well-organised and reliable. Correct use of power regulation and sensor interfacing. Wiring is tidy and labelled.|Circuits are functional and safe. Basic wiring is correct but may be cluttered. Limited use of cable management.|Circuits have intermittent faults or poor connections. Wiring is disorganised and difficult to trace.|Electronics are non-functional, unsafe, or incorrectly wired.|
|**Programming Logic & Control**|Code is modular (functions/classes) and highly efficient. Implements advanced logic (PID control, interrupts, or non-blocking code). Well-documented.|Code is logically structured and reliable. Effectively handles sensor inputs and motor outputs. Clear commenting throughout.|Code achieves basic functionality. Uses standard control structures (if/else, loops) effectively. Limited commenting.|Code is repetitive or inefficient. Basic logic errors present. Relies heavily on "delay()" causing unresponsive behaviour.|Code is incomplete, non-functional, or plagiarised.|
|**Problem Solving & Iteration**|Evidence of complex troubleshooting. Systematically isolated and solved integration issues. Clear documentation of iterative testing and refining.|Identifies and resolves technical hurdles. Evidence of adjustments made based on testing results and analysis.|Solves basic problems as they arise. Documents a simple "trial and error" approach to fixing faults.|Limited problem solving. Needs significant teacher guidance to fix minor errors.|Shows no initiative in solving problems; faults remain unaddressed.|