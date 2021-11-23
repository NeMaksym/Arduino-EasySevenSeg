![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![author](https://img.shields.io/badge/author-MaksymNetreba-informational.svg)
# Easy SevenSeg
Arduino library that significantly simplify connection process and usage of a seven-segment display (single-digit type)

### Supported digits
![zero](https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/7-segment_abcdef.svg/20px-7-segment_abcdef.svg.png)
![one](https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/7-segment_bc.svg/20px-7-segment_bc.svg.png)
![two](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f8/7-segment_abdeg.svg/20px-7-segment_abdeg.svg.png)
![three](https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/7-segment_abcdg.svg/20px-7-segment_abcdg.svg.png)
![four](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b0/7-segment_bcfg.svg/20px-7-segment_bcfg.svg.png)
![five](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9b/7-segment_acdfg.svg/20px-7-segment_acdfg.svg.png)
![six](https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/7-segment_acdefg.svg/20px-7-segment_acdefg.svg.png)
![seven](https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/7-segment_abc.svg/20px-7-segment_abc.svg.png)
![eight](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ab/7-segment_abcdefg.svg/20px-7-segment_abcdefg.svg.png)
![nine](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/7-segment_abcdfg.svg/20px-7-segment_abcdfg.svg.png)

### Supported letters
![a](https://upload.wikimedia.org/wikipedia/commons/thumb/2/28/7-segment_abcefg.svg/20px-7-segment_abcefg.svg.png)
![b](https://upload.wikimedia.org/wikipedia/commons/thumb/1/19/7-segment_cdefg.svg/20px-7-segment_cdefg.svg.png)
![c](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2d/7-segment_adef.svg/20px-7-segment_adef.svg.png)
![d](https://upload.wikimedia.org/wikipedia/commons/thumb/3/33/7-segment_bcdeg.svg/20px-7-segment_bcdeg.svg.png)
![e](https://upload.wikimedia.org/wikipedia/commons/thumb/8/89/7-segment_adefg.svg/20px-7-segment_adefg.svg.png)
![f](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a6/7-segment_aefg.svg/20px-7-segment_aefg.svg.png)

## Installation
### Either use Library Manager
In Arduino IDE **Sketch -> Include Library -> Manage Libraries...**.
Then find "Easy SevenSeg"
### Or import as Zip
On GitHub repository **Code -> Download Zip**

In Arduino IDE **Sketch -> Include Library -> Add .ZIP Library...**. Then select downloaded archive

## Usage
### In code
```cpp
#include "EasySevenSeg.h"   // Include

EasySevenSeg myDisplay;     // Initialize

myDisplay.begin();          // Begin (setups Arduino pins)

myDisplay.printDigit(1);    // Print 0 to 9
myDisplay.printLetter("A"); // Print A to F (accepts upper- and lowercase)
```

### Display types
There are two types of seven-segment displays.

Look at the picture below. The display has 10 pins in total. Pins #3 and #8 are common.
The other eight pins are responsible for a single segment each
*(yeah, it calls "seven-segment" mostly because of the historical reason)*.

Get back to the common pins. Depending on what they are we can distinguish two display types:

- **Common anode** display (common pins are +). 
  - It means, in order to highlight the segments, the common pins must be "+" (e.g., 5V or HIGH)
    and the segment pins must be "-" (e.g., GND or LOW)
- **Common cathode** display (common pins are -). 
  - It means, in order to highlight the segments, the common pins must be "-" (e.g., GND or LOW)
    and segment pins must be "+" (e.g., 5V or HIGH)
    
**Note 1:** The library is designed for the "common cathode" type.
If anyone wants to implement a "common anode", you are welcome to make a pull request.

**Note 2:** Segments are simple LEDs under the hood. In order to keep them safe,
don't forget to use resistors when connecting each of them to "+". 220Ω will be enough.

![Display pinout](https://lastminuteengineers.com/wp-content/uploads/arduino/7-Segment-Common-Anode-Common-Cathode-Pinout.png)

### Connect to Arduino
The `begin()` method setups appropriate Arduino pins as OUTPUT.

#### Default pins
By default (if no arguments passed to the method) you may use the following pins:
    
- display pin 1 == 1A on Arduino
- display pin 2 == 2A on Arduino
- display pin 4 == 4A on Arduino
- display pin 5 == 5A on Arduino
- display pin 6 == 6 on Arduino
- display pin 7 == 7 on Arduino
- display pin 9 == 9 on Arduino
- display pin 10 == 10 on Arduino

#### Custom pins
On the other hand, you may set up your own pin values. Just pass them to the `begin(int 1pin, ... int 10pin)` method. 
Keep in mind, pins #3 and #8 are omitted, since they are common (see "display types" above).

