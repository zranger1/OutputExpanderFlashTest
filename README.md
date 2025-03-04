## OutputExpanderFlash "ChangeTimingForV2" Branch
### What it does
This is an STM32CubeIDE project that builds alternate firmware for the v2 Pixelblaze Output Expander board.
Note that this version of the firmware WILL ONLY WORK WITH V2 boards. If you have a v1 or v3, you can use
the same method to adjust timing, but you'll have to modify the code for the appropriate branch yourself. 

This branch contains code that allows you to adjust the timing of the WS2812B data signal to work with LEDs
that may not be compatible with the default timing.  Instructions on how to calculate values for a particular
timing are included in the code comments in `Core/Src/main.c`.  The "working" code is in 'Core/Src/app.c'.
The values shown in the code are configured to replicate the 1.3us/2.6us timing that was available on the v2
Pixelblaze. 

### What you'll need
- STM32CubeIDE from https://www.st.com/en/development-tools/stm32cubeide.html
- STM32CubeProgrammer from https://www.st.com/en/development-tools/stm32cubeprog.html
- An ST-Link V2 Programmer or emulator.  I used this one:  https://www.amazon.com/HiLetgo-Emulator-Downloader-Programmer-STM32F103C8T6/dp/B07SQV6VLZ
- Either a compatible programming jig or some dupont wires and a steady hand with a soldering iron.
- A Pixelblaze
- A Pixelblaze Output Expander board, marked v2 (2019) or newer.
- a few LEDs to test
- A logic analyzer or oscilloscope to verify that the timing is correct is very, very helpful.

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
- Download or clone this project. Be sure to download the "ChangeTimingForV2" branch.
- Open it in STM32CubeIDE
- Select the .ioc file and build the project

### Programming the Output Expander
Once you've successfully built the firmware, it is time to download it
to the Output Expander's flash memory!

#### Connecting STM Programmer to Output Expander
You'll be connecting the 5 SWD(Serial Wire Debug)pads on the bottom of the output expander to the
corresponding 5 line on your STM programmer. The required lines are 3.3v, GND, Data, Clock and Reset. 
If you're going to do this frequently, you might want to order some pogo pins, and 3D print or otherwise 
craft a programming jig for yourself. 

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
- Shared to Enabled
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







