# HVPP
High Voltage Parallel Programmer for AVR 328P (Arduino Uno)

# History
This project is based on [Nick Gammon's High Voltage Programmer](http://www.gammon.com.au/forum/?id=12898)   
with source code repo at: [Nick Gammon](https://github.com/nickgammon/arduino_sketches)

Learning about Arduino development over the years has had successes and failures.
One of the more annoying failures is debugging an Arduino Uno - it is so very easy to "brick" an Uno! 

# Concept 
## High Voltage Parallel Programming 
HVPP applies 12V to the RESET pin of an Uno mcu (Atmega328P) for the duration of a programming session.  
It is called "parallel" because when sending data to the chip, all 8 bits (ie. fuses) are read from or written to at once.  

### Pros
This allows you to recover when fuses are incorrectly set or cleared.  
Some examples are:
1. DWEN and lockbits set: debugWIRE not usable.
2. DWEN set, SPIEN cleared: stuck in debugWIRE mode, cannot use SPI.
3. Clock configuration change.
4. Program the internal flash and EEPROM.
5. Disabled RESET pin.

### Cons
You ***must*** remove the mcu from it's circuit and place it into a special programming jig.

## Design 
High Voltage Programming is actually a suite of two programs:
1. Atmega Board Detector  
    [Sketch to detect Atmega chip types](http://www.gammon.com.au/forum/?id=11633)  

2. Atmega Board Programmer  
    [Atmega bootloader programmeer](http://www.gammon.com.au/bootloader)

## Versioning  
HVPP uses semantic versioning (Major.Minor.Patch)  
Major: Breaking changes Eg. new hardware incompatible with existing codebase  
Minor: Non-breaking changes Eg. new code functionality, new compatible hardware  
Patch: All other non-breaking changes Eg. Bug fixes, comments  

### Current Version
1.1.0  
- Hard coded for high voltage parallel programming
- Minor version downgrade of SdFat library  

### Planned Versions
2.0.0
- modify code to allow use of Mega 2560
- modify jig to allow use of Mega 2560  
-  
1.2.0
- modify board programmer control options
  - remove lilypad option
  - consolidate continue, quit, verify, and program options  
  - 
### Previous Versions
1.0.0
- programming jig built per N.Gammon design  

# Bill of Materials
| Item                      | Count | Link                                                                        | Part Number          |
| :------------------------ | :---: | :-------------------------------------------------------------------------- | :------------------- |
| Atmel-ICE Debugger        | 1     | [Digikey Atmel-ICE Basic](https://www.digikey.ca/en/products/detail/microchip-technology/ATATMEL-ICE-BASIC/4753381) | ATATMEL-ICE-BASIC-ND | 
| Arduino Uno Board         | 1     | [Mouser](https://www.mouser.ca/ProductDetail/474-DEV-11021)                 | 474-DEV-11021        |
| 28 pin ZIF Socket         | 1     | [Solarbotics](https://www.solarbotics.com/product/42050)                    | 42050                |
| P-Channel MOSFET FQP27P06 | 1     | [Sparkfun](https://www.sparkfun.com/products/10349)                         | COM-10349            |
| 2N3904 NPN Transistor     | 1     | [Sparkfun](https://www.sparkfun.com/products/521)                           | COM-00521            |
| 22 kOhm resistor          | 21    | [Sparkfun Resistor Kit]()                                                   | ABC-NNNNN            |
| 1 kOhm resistor           | 22    | [Sparkfun Resistor Kit]()                                                   | ABC-NNNNN            |
| 10 nF Ceramic Capacitor<br>100 nF Ceramic Capacitor|1<br>1| [Sparkfun](https://www.sparkfun.com/products/13698)      | KIT-13698            |
| DC Barrel Jack            | 1     | [Mouser](https://www.mouser.ca/ProductDetail/474-PRT-10811)                 | 474-PRT-10811        |
| Breadboard Power Supply   | 1     | [Sparkfun Breadboard Power Supply](https://www.sparkfun.com/products/13032) | PRT-13023            |
| Solderless Breadboard     | 1     | [Sparkfun](https://www.sparkfun.com/products/12002)                         |  PRT-12002           |

# Hardware Tools
[Atmel-ICE Basic](https://www.microchip.com/en-us/development-tool/atatmel-ice)  is a development tool for debugging and programming ARM® Cortex®-M based SAM and AVR microcontrollers with on-chip debug capability.  

# Software Tools  
## AVR Programming (Optional)
[AVRDUDE](https://github.com/avrdudes/avrdude/) is a program for downloading and uploading the on-chip memories of Microchip’s AVR microcontrollers.  
[AVRDUDESS](https://github.com/ZakKemble/AVRDUDESS?tab=readme-ov-file) is GUI for AVRDUDE.  

Using AVRDUDE/AVRDUDESS will require using a hardware programmer/debugger like Atmel-ICE.   
You will also need to know what fuse programming is and how to set the fuses for the Uno.  

[ATmega328P](Docs/Info/ATmega48A-PA-88A-PA-168A-PA-328-P-DS-DS40002061A.pdf)

## CAD
[Fritzing](https://fritzing.org/) is be no means the best CAD program, but it is free ( and still cheap even when you buy the licensed version), easy enough to learn, and reasonably well supported.  
[Eagle](http://eagle.autodesk.com/) and [KiCad](https://www.kicad.org/) are far more powerful, but steeper learning curve options.

## IDES
[Arduino](https://docs.arduino.cc/software/ide/)  
Using the Arduino IDE is somewhat optional.   
It easier to install libraries and boards via the Arduino IDE than Microchip Studio with Visual Micro extension for the simple fact of the extension installation and setup overhead.  
That said, once you do have the extension installed, there is no need to use the Arduino IDE again.  

[Microchip Studio Download](https://www.microchip.com/en-us/tools-resources/develop/microchip-studio)    
[Setting Started with Microchip Studio](Docs/MicrochipStudio/Getting-Started-with-Microchip-Studio-DS50002712B.pdf)  
[Microchip Studio User Guide](Docs/MicrochipStudio/Microchip-Studio-UserGuide-DS50002718.pdf)  
Microchip Studio is Microchip's (formerly Atmel) IDE for AVR/ARM applications, based on Visual Studio.  

[Getting Started with Microchip Studio](https://ww1.microchip.com/downloads/aemDocuments/documents/MCU08/ProductDocuments/UserGuides/Getting-Started-with-Microchip-Studio-DS50002712B.pdf)  
[Microchip Studio user Guide](https://ww1.microchip.com/downloads/aemDocuments/documents/MCU08/ProductDocuments/UserGuides/Microchip-Studio-UserGuide-DS50002718.pdf)  

## Extensions
[Visual Micro](https://www.visualmicro.com/)  
[Visual Micro Table of Contents](https://www.visualmicro.com/page/User-Guide.aspx?doc=index)  

Visual Micro is an extension (plugin/add-on) for Microsoft Microchip Studio 7 that allows any Arduino project to be developed, compiled, and then uploaded to any Arduino board, while taking benefit of the powerful features of Microchip Studio.  
Visual Micro works alongside, and is compatible with, the Arduino development environment, using the same libraries, source code, and development tools.  
The difference lies in Visual Micro's user interface which provides an advanced and professional development environment, and allows for more advanced development than the existing Arduino IDE.

## Important Arduino IDE Setup
*The Arduino AVR Board Library has a known bug in versions greater than 1.82:*  
 
[Downgrade Arduino AVR Boards to 1.82](https://github.com/LubomirJagos/LabVIEW-Universal-Transcriptor/issues/3)

To workaround, use Arduino IDE tools > Board > Board Manager to select Arduino AVR Boards.  
Select version 1.8.2 from drop down list.  

***DO NOT UPDATE THIS BOARD WHEN YOU OPEN THE ARDUINO IDE AND GET THE UPDATE INFO DIALOG BOX***

## Important Visual Micro Setup
Visual Micro comes with it's own set of issues.  
One of the most frustrating is the **compilation flags are hard coded in the platform.txt file installed by the extension AND the Arduino IDE**,  
( which contains definitions for the CPU architecture used - compiler, build process parameters, tools used for upload, etc.).  

This is fine for beginning users coming the Arduino IDE - the whole point is to make development easier.  
Why Visual Micro elected to use the hard coded approach baffles me - doing so means that any compiler flags you want to set in Microchip **are overridden - by both VisualMicro and Arduino!!.**   

So if you want to compile a non-optimized max debug level hex file, you *can't*.  

The platform.txt files are located at :  
*C:\Program Files (x86)\Atmel\Studio\7.0\Extensions\\{extension id}\Micro Platforms\mpide\hardware\arduino\\*  
*C:\Users\\{user name}\AppData\Local\Arduino15\packages\arduino\hardware\avr\1.8.2\\*  

The default flags are -g -Os (minimal debgug level and optimize for size).  
For example, to compile a max debug level no optimization build, comment out original line:  
```
compiler.c.flags=-c -g -Os -w -ffunction-sections -fdata-sections -MMD
```
and add:  
```
compiler.c.flags=-c -g3 -Og -w -ffunction-sections -fdata-sections -MMD
```  
likewise, do the same for the cpp compile flag:   
```  
compiler.cpp.flags=-c -g -Os -w -fno-exceptions -ffunction-sections -fdata-sections -MMD
```  
and add:  
```   
compiler.cpp.flags=-c -g3 -Og -w -fno-exceptions -ffunction-sections -fdata-sections -MMD
```  
***Change these as you see fit when you are ready for a production build.***   

# Project
## Third party Libraries
All of the 3rd libraries party need installation, and version definitely matters.

SdFat  
[SFat](https://github.com/greiman/SdFat)  
v.1.1.4  

```c++
#include <SdFat.h>
```  

## Project Fritzing  
The Atmega328 mcu goes in the zero insertion force socket
![HVPP Breadboard](/Docs/Images/HVP_Uno_bb.png)  

## Project Schematic  
![HVPP Schematic](/Docs/Schematics/HVP_Uno_schem.png)  

## Usage
### ATmega Board Detector

```
Opening port
Port open
VMDPR_
Atmega chip detector.
Written by Nick Gammon.
Version 1.20
Compiled on Dec  9 2024 at 15:29:20 with Arduino IDE 108010.
Activating high-voltage PARALLEL programming mode.
Signature = 0x1E 0x95 0x0F 
Processor = ATmega328P
Flash memory size = 32768 bytes.
LFuse = 0xFF 
HFuse = 0xDE 
EFuse = 0xFD 
Lock byte = 0xCF 
Clock calibration = 0xA1 
Bootloader in use: Yes
EEPROM preserved through erase: No
Watchdog timer always on: No
Bootloader is 512 bytes starting at 7E00

Bootloader:

7E00: 0x11 0x24 0x84 0xB7 0x14 0xBE 0x81 0xFF 0xF0 0xD0 0x85 0xE0 0x80 0x93 0x81 0x00 
7E10: 0x82 0xE0 0x80 0x93 0xC0 0x00 0x88 0xE1 0x80 0x93 0xC1 0x00 0x86 0xE0 0x80 0x93 
7E20: 0xC2 0x00 0x80 0xE1 0x80 0x93 0xC4 0x00 0x8E 0xE0 0xC9 0xD0 0x25 0x9A 0x86 0xE0 
7E30: 0x20 0xE3 0x3C 0xEF 0x91 0xE0 0x30 0x93 0x85 0x00 0x20 0x93 0x84 0x00 0x96 0xBB 
7E40: 0xB0 0x9B 0xFE 0xCF 0x1D 0x9A 0xA8 0x95 0x81 0x50 0xA9 0xF7 0xCC 0x24 0xDD 0x24 
7E50: 0x88 0x24 0x83 0x94 0xB5 0xE0 0xAB 0x2E 0xA1 0xE1 0x9A 0x2E 0xF3 0xE0 0xBF 0x2E 
7E60: 0xA2 0xD0 0x81 0x34 0x61 0xF4 0x9F 0xD0 0x08 0x2F 0xAF 0xD0 0x02 0x38 0x11 0xF0 
7E70: 0x01 0x38 0x11 0xF4 0x84 0xE0 0x01 0xC0 0x83 0xE0 0x8D 0xD0 0x89 0xC0 0x82 0x34 
7E80: 0x11 0xF4 0x84 0xE1 0x03 0xC0 0x85 0x34 0x19 0xF4 0x85 0xE0 0xA6 0xD0 0x80 0xC0 
7E90: 0x85 0x35 0x79 0xF4 0x88 0xD0 0xE8 0x2E 0xFF 0x24 0x85 0xD0 0x08 0x2F 0x10 0xE0 
7EA0: 0x10 0x2F 0x00 0x27 0x0E 0x29 0x1F 0x29 0x00 0x0F 0x11 0x1F 0x8E 0xD0 0x68 0x01 
7EB0: 0x6F 0xC0 0x86 0x35 0x21 0xF4 0x84 0xE0 0x90 0xD0 0x80 0xE0 0xDE 0xCF 0x84 0x36 
7EC0: 0x09 0xF0 0x40 0xC0 0x70 0xD0 0x6F 0xD0 0x08 0x2F 0x6D 0xD0 0x80 0xE0 0xC8 0x16 
7ED0: 0x80 0xE7 0xD8 0x06 0x18 0xF4 0xF6 0x01 0xB7 0xBE 0xE8 0x95 0xC0 0xE0 0xD1 0xE0 
7EE0: 0x62 0xD0 0x89 0x93 0x0C 0x17 0xE1 0xF7 0xF0 0xE0 0xCF 0x16 0xF0 0xE7 0xDF 0x06 
7EF0: 0x18 0xF0 0xF6 0x01 0xB7 0xBE 0xE8 0x95 0x68 0xD0 0x07 0xB6 0x00 0xFC 0xFD 0xCF 
7F00: 0xA6 0x01 0xA0 0xE0 0xB1 0xE0 0x2C 0x91 0x30 0xE0 0x11 0x96 0x8C 0x91 0x11 0x97 
7F10: 0x90 0xE0 0x98 0x2F 0x88 0x27 0x82 0x2B 0x93 0x2B 0x12 0x96 0xFA 0x01 0x0C 0x01 
7F20: 0x87 0xBE 0xE8 0x95 0x11 0x24 0x4E 0x5F 0x5F 0x4F 0xF1 0xE0 0xA0 0x38 0xBF 0x07 
7F30: 0x51 0xF7 0xF6 0x01 0xA7 0xBE 0xE8 0x95 0x07 0xB6 0x00 0xFC 0xFD 0xCF 0x97 0xBE 
7F40: 0xE8 0x95 0x26 0xC0 0x84 0x37 0xB1 0xF4 0x2E 0xD0 0x2D 0xD0 0xF8 0x2E 0x2B 0xD0 
7F50: 0x3C 0xD0 0xF6 0x01 0xEF 0x2C 0x8F 0x01 0x0F 0x5F 0x1F 0x4F 0x84 0x91 0x1B 0xD0 
7F60: 0xEA 0x94 0xF8 0x01 0xC1 0xF7 0x08 0x94 0xC1 0x1C 0xD1 0x1C 0xFA 0x94 0xCF 0x0C 
7F70: 0xD1 0x1C 0x0E 0xC0 0x85 0x37 0x39 0xF4 0x28 0xD0 0x8E 0xE1 0x0C 0xD0 0x85 0xE9 
7F80: 0x0A 0xD0 0x8F 0xE0 0x7A 0xCF 0x81 0x35 0x11 0xF4 0x88 0xE0 0x18 0xD0 0x1D 0xD0 
7F90: 0x80 0xE1 0x01 0xD0 0x65 0xCF 0x98 0x2F 0x80 0x91 0xC0 0x00 0x85 0xFF 0xFC 0xCF 
7FA0: 0x90 0x93 0xC6 0x00 0x08 0x95 0x80 0x91 0xC0 0x00 0x87 0xFF 0xFC 0xCF 0x80 0x91 
7FB0: 0xC0 0x00 0x84 0xFD 0x01 0xC0 0xA8 0x95 0x80 0x91 0xC6 0x00 0x08 0x95 0xE0 0xE6 
7FC0: 0xF0 0xE0 0x98 0xE1 0x90 0x83 0x80 0x83 0x08 0x95 0xED 0xDF 0x80 0x32 0x19 0xF0 
7FD0: 0x88 0xE0 0xF5 0xDF 0xFF 0xCF 0x84 0xE1 0xDE 0xCF 0x1F 0x93 0x18 0x2F 0xE3 0xDF 
7FE0: 0x11 0x50 0xE9 0xF7 0xF2 0xDF 0x1F 0x91 0x08 0x95 0x80 0xE0 0xE8 0xDF 0xEE 0x27 
7FF0: 0xFF 0x27 0x09 0x94 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0x04 0x04 

MD5 sum of bootloader = 0xFB 0xF4 0x9B 0x7B 0x59 0x73 0x7F 0x65 0xE8 0xD0 0xF8 0xA5 0x08 0x12 0xE7 0x9F 
Bootloader name: optiboot_atmega328

First 256 bytes of program memory:

00: 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 
...
F0: 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 

Programming mode off.
```

### ATmega Board Programmer
```
Activating high-voltage PARALLEL programming mode.
Signature = 0x1E 0x95 0x0F 
Processor = ATmega328P
Flash memory size = 32768 bytes.
LFuse = 0xFF 
HFuse = 0xDE 
EFuse = 0xFD 
Lock byte = 0xEF 
Clock calibration = 0xA1 
Type 'L' to use Lilypad (8 MHz) loader, or 'U' for Uno (16 MHz) loader ... **U**

Using Uno Optiboot 16 MHz loader.
Bootloader address = 0x7E00
Bootloader length = 512 bytes.
Type 'Q' to quit, 'V' to verify, or 'G' to program the chip with the bootloader ... **G**

Erasing chip ...
Writing bootloader ...
Committing page starting at 0x7E00
Committing page starting at 0x7E80
Committing page starting at 0x7F00
Committing page starting at 0x7F80
Written.
Verifying ...
No errors found.
Writing fuses ...
LFuse = 0xFF 
HFuse = 0xDE 
EFuse = 0xFD 
Lock byte = 0xEF 
Clock calibration = 0xA1 
Done.
Programming mode off.
Type 'C' when ready to continue with another chip ... **C**
``` 

Select Uno again  

```
Using Uno Optiboot 16 MHz loader.
Bootloader address = 0x7E00
Bootloader length = 512 bytes.
Type 'Q' to quit, 'V' to verify, or 'G' to program the chip with the bootloader ... **V**

Verifying ...
No errors found.
Done.
Programming mode off.
Type 'C' when ready to continue with another chip ... **C**
```  

Select Uno again  

```
Using Uno Optiboot 16 MHz loader.
Bootloader address = 0x7E00
Bootloader length = 512 bytes.
Type 'Q' to quit, 'V' to verify, or 'G' to program the chip with the bootloader ... **Q**
```
