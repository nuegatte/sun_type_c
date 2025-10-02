# sun_type_c

 



## Introduction

<img width="500"  alt="image" src="https://github.com/user-attachments/assets/5300cf41-55b2-48e2-9f9b-4db87107182b" /><img width="500" alt="image" src="https://github.com/user-attachments/assets/a971bd1e-8f9d-4b8d-a9b6-68ef88e31ab1" /><img width="311" height="287" alt="image" src="https://github.com/user-attachments/assets/d9ef1935-2c95-499a-b258-cb8863c3e990" /><img width="600" alt="image" src="https://github.com/user-attachments/assets/a8159745-b2f3-49a6-b5fc-ac1beba5fc3a" />




This is a DIY project that converts a rubber dome membrane keyboard Sun Type 5c into a modern keyboard keyboard with VIAL keymapping, NKRO, and as well as USB C connectivity. This project aims to provide an afforable and straightforward solution to restore a Sun Type 5c to those with amateur electronics background (me included). The process involves creating a comepletely new keyboard matrix and keyswitch from scratch, wiring each keys with diodes, as well as coding the QMK firmware and porting it to the Raspberry Pi Pico. 

## Background
The Sun Type 5c is a keyboard that was designed by Sun Microsystems and manufactured by Fujitsu for the Sun Sparcstation between 1991 to 1997. It uses a rubber dome over membrane with discrete sliders as actuators. The keyboard is typically more well built than other Fujitsu Keyboards which uses higher quality and much better designed rubber dome sheets, solid chassis construction, and as well as thick PBT keycaps for most of its keys. The additional keys on the left in constrast to a tranditional full size keyboard has led to the Sun Type 5c being one of the physically longer and larger keyboards, with a total of 119 keys.

### Why does it matter?


<img width="800" alt="image" src="https://github.com/user-attachments/assets/bb92e890-1d9a-486c-a324-d867366f18ea" />
<img   height="200" alt="image" src="https://github.com/user-attachments/assets/96e3ab91-8132-4199-bf66-5b5d03d6d229" />
<img width="500" alt="image" src="https://github.com/user-attachments/assets/c5fc3cec-33ff-49d0-b289-06b909a17179" />



The **Unix version** of Sun Type 5c is rather significant in the face of modern keyboards as its layout laid the foundation of the **Happy Hacking Keyboard's (HHKB)** layout next to the Apple M0110, which is favored by many keyboard enthusiasts and the likes of programmers as well due to its unique but well thought out key placements. 

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

## Understanding the Sun Type 5c

Disclaimer : Due to the lack of images prior modding, post-restoration images are used for references. I apologise in advance for this inconvenience, but I assure this will not affect future references. 

<img width="884" height="337" alt="Screenshot 2025-10-02 at 1 55 27 PM" src="https://github.com/user-attachments/assets/1e532a7e-ece0-4be8-81db-18caeb74a627" />

The Sun Type 5c consists of a tough and thick beige plastic top casing, with its bottom casing held together by only plastic clips.

<img width="483" height="356" alt="Screenshot 2025-10-02 at 1 55 50 PM" src="https://github.com/user-attachments/assets/f251270a-fcd2-4568-83c6-df426df80a4e" />
<img width="604" height="332" alt="Screenshot 2025-10-02 at 1 56 07 PM" src="https://github.com/user-attachments/assets/1c0c5dfc-a06a-4d2b-995b-ea58c3d536a5" />
Based on the image above, there are 5 visible tabs and 2 hidden tabs at the bottom side of the keyboard. To open the keyboard, pry open the hidden tab on rightmost/leftmost of the visible tab (refer to the image above), then slowly pry open the remaining ones.

There are also hidden clips at both left & right side of the keyboard case, pry it open the same way the previous hidden tabs are done, followed by pulling in a 90 degree angle. You will most likely hear a snapping sound, and that is normal from the clips on the top of the casing unlatching. Now your sun type 5c is opened.

Opening the case may require prying tools (i.e the back of a tweezer, and a flathead screw driver), and MORE IMPORTANTLY -- patience. 

<img width="329" height="287" alt="Screenshot 2025-10-02 at 1 56 29 PM" src="https://github.com/user-attachments/assets/1beaf300-4702-4586-9efb-3c4e18098916" />


Aged, brittle plastics are the biggest enemies of vintage hardwares, and my Sun Type 5c was ultimately a victim of this curse. The plastic tabs that holds the clip on the side of my keyboard's casing snapped off during my first opening attempt. 
It is advised to refrain from opening the keyboard as much as possible, unless it is required. My best advice is to do everything all at once before final reassembly.

Once opened, you see the internals which is held together in 

 
## Tools and Materials 
This section discusses tools and materials used and the reasoning behind it.

 
### Tools Involved
- Soldering tools
  - For soldering components   
- QMK Toolbox, VIAL
  - For building and compiling firmware
  - [Proper VIAL setup video by Joe Scotto, this helps. A LOT.](https://www.youtube.com/watch?v=O8pdUPqPG3k)
- C language, JSON
  - For configurating matrix layout and coding QMK firmware
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
  - Pre-insulated, only conductive on tinned parts.
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
- Clear nail polish
 
## Project Flow
1. [Improving key feel](#improving-key-feel)  
2. [Creating a reliable actuating mechanism](#creating-a-reliable-actuating-mechanism)  
3. [Designing matrix](#designing-matrix)  
4. [Wiring columns and Rows](#wiring-columns-and-rows)  
5. [Firmware](#firmware)  
6. [Test](#test)  
 
### Improving key feel

<img height="130" alt="image" src="https://github.com/user-attachments/assets/e07fa357-e861-4e50-9cae-0365739f0f08" />
<img height="130" alt="image" src="https://github.com/user-attachments/assets/8ffa866c-b7b6-42a7-84c1-5d809d6f0a92" />


Just like any other rubber dome over membrane keyboard, the Sun Type 5c's rubber dome are of a dome shaped cone with a protrusion on the underside. While this ensures enough pressure is applied to complete the circuit, drawbacks like mushy key feel may contribute to subjective discomforts when typing. 

#### **The solution? Trim the bump off!**
<img  height="200" alt="image" src="https://github.com/user-attachments/assets/16f16d81-d5cb-4509-b161-bb75887440dd" />

With the help of a wire cutter, the underside bump is trimmed off for every domes (Example on the image above). The result key feel yielded longer key travel, stronger tactility, and vastly reduced mushiness. In addition to the opaque rubber domes used in constrast to translucent silicone domes used in modern counterparts like the Sun Type 7, the structure of the domes itself is already much stiffer, contributing to the solid bottom out. However, it is unclear whether the color and materials affect the overall tactility of the rubber domes in this case, so take that statement with grain of salt.
 ______________
### Creating a reliable actuating mechanism
Before matrix design, it is important to create a reliable actuating mechanism to ensure the enhanced key feel does not go in vain. Moreover, this actuating mechanism is also aimed to emulate the standard mechanical keyboard's nature that allows for key overtravel, which is the tendency of a switch to actuate when pressed halfway.  
 
Before getting started, certain questions may have already been raised:  

1. Why don’t you just utilise the membrane traces and directly rewire it to your liking?  
    - The Sun Type 7's membrane traces operate through sandwiching a hole-punched spacing membrane in between the column and row membrane.  
      <img height="190" alt="image" src="https://github.com/user-attachments/assets/fcb03604-acc0-4f48-accc-309909035f8f" /><img height="190" alt="image" src="https://github.com/user-attachments/assets/51f83a9e-d980-4dbf-a8e8-fffca29f7017" />  
    - While it is easier to directly rewire the matrix like so, it would be impractical to fit dozens of SMD diodes in between the membrane.  
    - Moreover, the lack of underside bumps from the modded rubber domes does not provide sufficient pressure to register keys.  

2. How do you ensure the reliability of this mechanism created from ground up?  
    - Concerns like oxidation, aging and mechanical wear are expected.  
    - Most static traces will be coated in clear nail polish to ensure maximum airtight seal.  
    - Not only that, the proposed mechanisms will also be stress tested for at least 5 minutes to ensure reliability and ideal key feel is achieved without compromising the original key feel.  
      - Due to the lack of key switch stress testing machine, 5 minutes will be the maximum time used.  

The next section discusses the proposed mechanism for actuating key switches. While the methods are different, the premise remains the same:  
- All of the column and row traces will be constructed onto a single membrane layer, which is on top of the topmost membrane.  
- The traces are of exposed copper foil tapes, requiring a conductive agent to close the circuits to register keys.  
  <img width="593" height="420" alt="image" src="https://github.com/user-attachments/assets/fd5154bc-4134-4490-bd17-8de2c33d0d8f" />  
- The purpose of the proposed mechanism is to simply connect the circuits in the most efficient way.  
- Proposed mechanisms will be discussed, and why they are not suited as the final design.  
______________
#### *Proposed Solution*
______________
**Conductive pads (Rejected)**

<img width="396" height="213" alt="image" src="https://github.com/user-attachments/assets/303c1a0b-eb26-48e6-bce2-c23979267ff5" />

- The initial solution was to attach conductive pads to the underside of the domes.
- However, due to the cohesive nature of the dome sheets, gluing conductive pads may not be a viable solution.
- Using safer silicone based glues proved futile as conductive pads came loose from stress tests.
- Using cyanacrylate based adhesives (super glue) may badly alter key feel, as well as deteriotating the molecular structure of the dome sheet.
- Not only that, full key press is required for actuation, making key overtravel impossible.
- Varied pad placements caused inconsistencies in key actuation.
- Hence, this option is abandoned.
______________

**Topre capacitive springs (Rejected)**

<img  height="200" alt="image" src="https://github.com/user-attachments/assets/0f4bb781-37fa-48ac-8479-27cf6cd058c4" />
<img  height="200" alt="image" src="https://github.com/user-attachments/assets/884113d8-4cc7-4df4-9a41-2eac673d8874" />


- This solution utilised a trimmed Topre capactivie spring that precisely fit the rubber dome's dimension.
- Rather than capacitive sensing, this remains an electrical contact mechanism.
- The goal is to perform actuation through conducting the circuit with the collapse of the metal spring.
- The results yielded impressive key overtravel and solid bottom out.
- Despite initial success, stress tests proved that this solution requires precise spring trimming and placements to prevent short circuits.
- Moreover, the spring greatly obstructs key feel as it introduces unnnecessary padding that reduces tactility.
- Hence, this option is abandoned.
______________

**DIY copper foil actuator (Approved)**

<img  height="200" alt="image" src="https://github.com/user-attachments/assets/e974330c-068b-46c3-93e2-ca634987672b" /> 
<img  height="200" alt="image" src="https://github.com/user-attachments/assets/8854e82a-4e5f-4fcd-8898-6d2805f40af5" />
 

- Inspired by Fujitsu's leaf spring mechanical switches, this copper foil actuator design uses a single side conductive copper foil soldered directly onto the row circuit pads.
<img   height="200" alt="image" src="https://github.com/user-attachments/assets/b65c2627-ea8d-4775-bb28-d2960e4197d1" />
<img   height="200" alt="image" src="https://github.com/user-attachments/assets/b1d154f9-01d1-4ed0-ad85-15ca00ab5be5" />

- The copper foil actuator is a non sticky single sided conductive pad constructed by sticking the adhesive side of both copper and kapton tape together, which is then trimmed and folded according to the illustration below :
  - <img width="300"   alt="image" src="https://github.com/user-attachments/assets/764e0d61-a588-40f9-82ed-ecb9d148487e" />
  - <img width="300"   alt="image" src="https://github.com/user-attachments/assets/cf1e7763-5261-4f1b-b055-91316b410c08" />
  - <img width="300" alt="image" src="https://github.com/user-attachments/assets/fbc5f19c-ee46-44a2-927f-18d225388885" />
- Measurements in the illustration are recommended ones, off centered measurements due to size and precision constraints may be omited as long as the differences are small.
- The result lead to decent key overtravel, and stress tests are passed.
- Not only that, the key feel is virtually unaffected as the foil pads are thin enough to neglect any potential tactility reduction.
- Hence, this option is approved.
- The only caveat is that 119 of the same foil pads are required to make this project possible, and creating extras are recommended due to its small size.

______________

## Designing matrix

Matrix design basics :
- There are column pins and row pins
- Both of them combine altogether to form a grid of key combinations
- The shape of the physical matrix is not determined by its tabulated counterpart:
  - You can have a 12 by 12 matrix grid and let it share the physicial form factor of a full size keyboard/
  - That is if you can configure the traces from column to row to diodes (if any) efficiently.
  - This discipline may fall under the practise of PCB design
  - However, due to technological constraints, the entirety of the matrix is handwired.
  - Such tradeoffs may be countered with the usage of enameled wires to ensure flexible circuit design and required insulation.
- The number of usable GPIOs on your selected microcontroller limits the number of columns and rows in your keyboard matrix.

 ______________________

### Initial and Final design 

The main objective of the matrix design is to achieve the following : 
- The combined column, row, LED indicator pinouts do not exceed that of the Raspberry Pi Pico (26 usable GPIOs)

#### **Initial Design**
<img  height="250" alt="image" src="https://github.com/user-attachments/assets/12173f1b-9895-43af-a54c-6e42490cce39" />

- Direct, straightforward waffle matrix pattern
- This matrix requires a total of 30 GPIO (24 columns, 6 rows) to function properly, excluding the 3 LED indicator pins

- Pros
  - Physically tidy matrix layout, easy diode arrangement.

- Cons
  - Exceeds the number of available GPIOs of the Raspberry Pi Pico (only 26)
  - Unnecessarily huge matrix grid with many unused grid slots
    - 24 * 6 = 144 keys
    - Since the Sun Type C requires only 119 keys, this leaves 25 extra unused keys, deeming it wasteful  
  - Further planning shows that this layout is not exactly suitable due to the keyboard's build 

__________________________
#### **Final Design**
<img  height="250" alt="image" src="https://github.com/user-attachments/assets/4a44695d-da12-4ba9-86b1-a1243d8d5ebb" />

- Features an unconventional physical matrix that is designed with extensive planning
- The diagram above shows a redesigned matrix that is derived from the initial design
- For the sake of clear illustration, only columns of the matrix will be displayed based on the diagram above
- This matrix requires a total of 22 GPIO (11 columns, 11 rows) to function properly, excluding the 3 LED indicator pins

- Pros
  - Space saving matrix that requires less GPIOs (22 total, 25 if including LED indicators)
  - Ideal for implementation onto Raspberry Pi Pico
   

- Cons
  - Confusing to code with, but still applicable


### Tabulated form
<img  height="250" alt="image" src="https://github.com/user-attachments/assets/4a44695d-da12-4ba9-86b1-a1243d8d5ebb" />
<img  height="250" alt="image" src="https://github.com/user-attachments/assets/1b53fb11-d81a-4a0c-8a51-ae5d5b8a55bd" />

- The table above shows the corresponding elements of each keys along with their row and column numbers.
- The red dot marks the first element of each column, which the blue one resembles the second one.
  - For example, the first element of column 1 based on the matrix diagram corresponding to the table is [Help] (Row 1, Column 1)
  - Followed by the 2nd element of column 1, which is [M1] (Row 2, Column 1), and so on...




_______________

## Wiring columns and rows


- col2row
- explain diode placements

### Pinout to Microcontroller

### Wiring indicator LEDs

_______________

## Firmware
- keyboard layout editor
- basic vial setup
- matrix setup
- compiling firmware (directory and whatnots)
- flashing firmware


## Challenges and limitations

### Challenges
 - actuating mechanism from scratch
   - most time consuming part, due to intense testing
 - matrix design
   - due to pin constraints
 - diode placements
   - most challenging part, due to limited space
 - soldering on a membrane
   - heat control 
 - wiring method
   - copper pen was initially used
   - abandoned due to high resistance
   - enamel wire instead
 - short circuiting
   - excess flux not cleaned up
   - lack of insulation
    - nail polish
 - bad soldered joints
   - resoldering  
 - bad contact pads
   - only fixed to place w/ tape
   - under the assumption of easy-to-replace foil pads for easy repair
   - only to be a conductivity issue
   - directly soldering
   - clean excess flux to prevent short circuit

 ### Limitations
 - 16 macros only
 - No BT
   




