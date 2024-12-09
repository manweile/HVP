# HVPP
High Voltage Parallel Programmer for AVR 328P (Arduino Uno)

# History
This project is based on [Nick Gammon's High Voltage Programmer](http://www.gammon.com.au/forum/?id=12898) 

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
High Voltage Programming is actually a suite of three programs:
1. Atmega Board Detector  
    @TODO IPSUM LOREM
2. Atmega Board Programmer  
    @TODO IPSUM LOREM
3. Atmega Hex Uploader  
    @TODO IPSUM LOREM

## Versioning  
HVPP uses semantic versioning (Major.Minor.Patch)  
Major: Breaking changes Eg. new hardware incompatible with existing codebase  
Minor: Non-breaking changes Eg. new code functionality, new compatible hardware  
Patch: All other non-breaking changes Eg. Bug fixes, comments  

### Current Version
1.1.0  
- Hard coded for high voltage parallel programming
- Minor version downgrade of SdFat library  

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