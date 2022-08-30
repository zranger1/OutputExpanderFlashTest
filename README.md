# OutputExpanderFlash
### What it does
This is an STM32CubeIDE project that builds alternate firmware for the Pixelblaze Output Expander board.
The new firmware works only with WS2812-protocol RGBW LEDs and allows the user to choose between normal
RGBW operation and RGB-W operation, which disables the W channel and uses RGB values from Pixelblaze to
produce white.

It's marginally useful -- mostly if you don't like the particular white your RGBW LEDs produuce and want to 
use the mixed RGB white instead, but it does provide a simple example of how to build and flash Output Expander firmware.

### What you'll need
- STM32CubeIDE from https://www.st.com/en/development-tools/stm32cubeide.html
- STM32CubeProgrammer from https://www.st.com/en/development-tools/stm32cubeprog.html
- An ST-Link V2 Programmer or emulator.  I used this one:  https://www.amazon.com/HiLetgo-Emulator-Downloader-Programmer-STM32F103C8T6/dp/B07SQV6VLZ
- Quite a lot of dupont wires or other small, easy-to-connect wiring.  
- A soldering iron & lead-free solder
- A Pixelblaze
- A Pixelblaze Output Expander board, marked v2 (2019) or newer.
- a few RGBW LEDs to test

### WARNING:  
**Modifying firmware can break your device and potentially other connected devices.** If you attempt this,
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
- Download or clone this project - https://github.com/zranger1/OutputExpanderFlashTest
- Open it in STM32CubeIDE
- Select the .ioc file and build the project


### Programming the Output Expander
Once you've successfully built the firmware, it is time to download it
to the Output Expander's flash memory!


#### Connecting STM Programmer to Output Expander
You'll be connecting the 5 SWD(Serial Wire Debug)pads on the bottom of the output expander to the
corresponding 5 line on your STM programmer. The required lines are 3.3v, GND, Data, Clock and Reset. 
If you're going to do this frequently, you might want to order some pogo pins, and 3D print or otherwise 
craft a programming jig for yourself. I just soldered short wires to the pads.

#### Programming the Output Expander
With your STM Programmer wired to the Output Expander and plugged into a
USB port in your computer, open the STM32CubeProgrammer application.  On the right hand side, you'll 
see the ST-Link configuration window. Set the configuration as follows:
- Port to SWD
- Frequency to 4000
- Mode to Under reset
- Access port to 0
- Reset Mode to Hardware reset
- Speed to Reliable
- Shard to Enabled
- Uncheck Debug in Low Power Mode

- Now click the "Refresh" icon next to the Serial Number field. Your Programmer's serial number
should be displayed.
- Click the "Connect" button.  If all is working properly, you should see a bunch of information
about the Output Expander's CPU.  Now you're ready to download the new firmware.

On the left hand side of the application, you'll see a column of icons for selecting tabs.  Choose
the "Erasing and Programming" tab (second from the top, not counting the hamburger menu).

Use the file path control to select your .elf file.  Depending on which build configuration you've chosen
it will be "pixelblaze_output_expander.elf" in either the Debug or Release subdirectory.

Once you've chosen the file, press the "Start Programming" button.  A few seconds later, your new
firmware will be successfully installed on your Output Expander.







