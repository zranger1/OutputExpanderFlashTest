### What you'll need:
- STM32CubeIDE from https://www.st.com/en/development-tools/stm32cubeide.html
- STM32CubeProgrammer from https://www.st.com/en/development-tools/stm32cubeprog.html
- An ST-Link V2 Programmer or emulator.  I used this one:  https://www.amazon.com/HiLetgo-Emulator-Downloader-Programmer-STM32F103C8T6/dp/B07SQV6VLZ
- Quite a lot of dupont wires or other small, easy-to-connect wiring.  
- A soldering iron & lead-free solder
- A Pixelblaze
- A Pixelblaze Output Expander board, marked v2 (2019) or newer.
- a few RGBW LEDs to test

### WARNING:  
Modifying firmware can break your device and potentially other connected devices. If you attempt this,
you are solely and completely responsible for the outcome. So go slowly and be careful. Triple check polarity,
disconnect everything else from your output expander when programming and... try to keep the cat away
from your work area. 

### Building the firmware
#### From Scratch
- Clone or download the original OutputExpanderFirmware project from https://github.com/simap/pixelblaze_output_expander.
- Create an empty directory for your project-to-be
- Create a project in your new empty directory by having STM32CubeIDE "Import an existing STM32CubeMX configuration file (.ioc)" from
the expanderboard2.ioc file in pixelblaze_output_expander/firmware.
- Copy the Core and Drivers directories from pixelblaze_output_expander/firmware to your new project.  Just
drag each directory on over to the new location.

Try building your new project in STM32CubeIDE - you should now be able to successfully compile.


#### From OutputExpanderFlashTest
I've 


### Connecting STM Programmer to Output Expander
You'll be connecting the 5 SWD(Serial Wire Debug)pads on the bottom of the output expander to the
corresponding 5 line on your STM programmer. The required lines are 3.3v, GND, Data, Clock and Reset. 
If you're going to do this frequently, you might want to order some pogo pins, and 3D print or otherwise 
craft a programming jig for yourself. I just soldered short wires to the pads.

<picture of wired expander board>
