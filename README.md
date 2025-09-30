# sun_type_c

## Table of Contents
- [Introduction](#introduction)
- [Background](#background)
  - [Why does it matter?](#why-does-it-matter)
- [Problem Statement](#problem-statement)
- [Project Scope](#project-scope)
- [Tools and Materials](#tools-and-materials)
  - [Tools Involved](#tools-involved)
  - [Materials Involved](#materials-involved)



## Introduction

<img width="500"  alt="image" src="https://github.com/user-attachments/assets/5300cf41-55b2-48e2-9f9b-4db87107182b" /><img width="500" alt="image" src="https://github.com/user-attachments/assets/a971bd1e-8f9d-4b8d-a9b6-68ef88e31ab1" /><img width="311" height="287" alt="image" src="https://github.com/user-attachments/assets/d9ef1935-2c95-499a-b258-cb8863c3e990" /><img width="600" alt="image" src="https://github.com/user-attachments/assets/a8159745-b2f3-49a6-b5fc-ac1beba5fc3a" />




This is a DIY project that converts a rubber dome membrane keyboard Sun Type 5c into a modern keyboard keyboard with VIAL keymapping, NKRO, and as well as USB C connectivity. This project aims to provide an afforable and straightforward solution to restore a Sun Type 5c to those with amateur electronics background (me included). The process involves creating a comepletely new keyboard matrix from scratch, and wiring each keys with diodes, as well as coding the QMK firmware and porting it to the Raspberry Pi Pico. 

## Background
The Sun Type 5c is a keyboard that was designed by Sun Microsystems and manufactured by Fujitsu for the Sun Sparcstation between 1991 to 1997. It uses a rubber dome over membrane with discrete sliders as actuators. The keyboard is typically more well built than other Fujitsu Keyboards which uses higher quality and much better designed rubber dome sheets, solid chassis construction, and as well as thick PBT keycaps for most of its keys. 

### Why does it matter?


<img width="800" alt="image" src="https://github.com/user-attachments/assets/bb92e890-1d9a-486c-a324-d867366f18ea" />
<img   height="200" alt="image" src="https://github.com/user-attachments/assets/96e3ab91-8132-4199-bf66-5b5d03d6d229" />
<img width="500" alt="image" src="https://github.com/user-attachments/assets/c5fc3cec-33ff-49d0-b289-06b909a17179" />



The **Unix version** of Sun Type 5c is rather significant in the face of modern keyboards as its layout laid the foundation of the **Happy Hacking Keyboard's (HHKB)** layout, which is favored by many keyboard enthusiasts and the likes of programmers as well due to its unique but well thought out key placements. 

For someone who owns a HHKB and favors full sized keyboards, the Sun Type 5c seems like an ideal choice for my daily usage. However, getting it to work may not be that simple.


## Problem Statement
<img width="400" alt="image" src="https://github.com/user-attachments/assets/48235314-45c7-4c55-ba33-5bb866324295" />

As a legacy device, the Sun Type 5c uses a proprietary protocol that is only compatible with Sun Systems, and its 8-pin mini-DIN connector is incompatible with the more common PS/2 ones.

<img  height="280" alt="image" src="https://github.com/user-attachments/assets/5352a48e-91a1-4bb9-8fa9-f806d98cd10f" />

Athough building a TMK converter with an Arduino Pro Micro is a common solution, my Sun Type 5c arrived without its cable connector, leaving the controller pinouts even more ambiguous. After countless attempts to test pinouts and search of detailed documentation on this keyboard's stock controller, creating a simple converter was not feasible. 

Even if the such a converter is successful, common issues like 2KRO, lack of proper key overtravel would occur due to the nature of rubber dome membrane mechanisms. Not only that, TMK firmware requires reflashing the firmware when it comes to remapping the keys, despite supporting 8 remappable layers at once. Subjective drawbacks like mushy keyfeel also prevents the project from achieving the intended results. 

## Project Scope
The scope of the project includes the following : 
- A USB-C compatible Sun Type 5c, addressed as 'Sun Type C' from now on
- Creating a keyboard matrix from scratch that supports full NKRO (N-Key rollover)
- Supports QMK, VIAL for remapping on the fly
- Runs on Raspberry Pi Pico RP2040
- Up to 10 layers for remappability, as well as 36 macros.
- Improved rubber dome key feel (Less mushiness, better overtravel, etc.)
- Challenges and limitations faced in this project

This project does not cover how QMK entirely works, but it will include the steps to get the firmware flashed into the Pi Pico.
This project also does not cover detailed overview on the keyboard itself.

## Tools and Materials 
This section discusses tools and materials used and the reasoning behind it.

### Tools Involved
- Soldering tools
  - For soldering components   
- QMK Toolbox, VIAL
  - For building and compiling firmware
  - [Proper VIAL setup video by Joe Scotto, this helps. A LOT.](https://www.youtube.com/watch?v=O8pdUPqPG3k)
- C, JSON
  - For coding matrix layout and QMK firmware
- Multimeter, Ruler, Cutting Knife, Wire Cutter, Tweezers
  - For measuring, cutting and arranging components

### Materials involved


- 5mm, 10mm copper tape w/ conductive adhesive
  -  <img height="50" alt="image" src="https://github.com/user-attachments/assets/20b9be9d-349d-46d0-b40a-d578d7c2a318" />
  - For Matrix wiring, as well as copper foil actuator

 

- Kapton tape
  - <img   height="50" alt="image" src="https://github.com/user-attachments/assets/b1499819-00ec-4ab1-a901-ef3b33149d7f" />
  -  Basic insulation purposes
 

- [1N4148 Series SMD Diode (SOD-523)](https://my.mouser.com/c/semiconductors/discrete-semiconductors/diodes-rectifiers/?mounting%20style=SMD%2FSMT&series=1N4148)
  - <img height="50" alt="image" src="https://github.com/user-attachments/assets/4326e5fd-5dcd-442c-819d-58d29b3b8e1c" />
  - For NKRO implementation
  - Compact size that fits between cramped spaces of the keyboard
  - Directly soldered onto the keyboard membrane.    
- 1k Ohm resistor
  - For indicator LEDs 
- 0.05mm, 0.1mm enameled copper wire
  - <img   height="50" alt="image" src="https://github.com/user-attachments/assets/d8520e5f-dcb1-43f3-b7bd-a36468a461be" />
  - For wiring row to diode wiring, as well as wiring to controller
  - Fits cramped spaces between keyboard parts
- Raspberry Pi Pico RP2040 (USB-C version)
  - <img height="50" alt="image" src="https://github.com/user-attachments/assets/3f5a9160-0dfb-42ba-aedd-c7e3615e5c47" />
  - Most convenient flashing method (Drag and Drop)
  - Sufficient number of usable GPIOs for full size keyboard (26 GPIOs)
  - USB-C detachable
- 20cm USB-C extension cable (Female to Male)
  - <img height="80" alt="image" src="https://github.com/user-attachments/assets/94d8a425-2f70-451d-83ba-8819354200f2" />
  -  Preserves lifespan of the original Pi Pico's USB-C port
  - Allows modularity between cable repair/chip repair routines
    
