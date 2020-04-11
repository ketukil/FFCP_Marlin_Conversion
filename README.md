# FlashForge Creator Pro Marlin conversion

Quick guide on converting *[FlashForge Creator Pro](https://www.flashforge.com/consumer/detail/Creator%20Pro?id=4)* running Sailfish firmware to the *[Marlin](https://github.com/MarlinFirmware/Marlin)* firmware. Not intended for faint of heart. This guide is not 100% complete and it stands here a reference for future development.

DISCLAIMER: By using this guide you are fully aware of the risks involved by such modifications. I hereby take no responsibility for any loss and/or damage to property and/or personnel involved. DO THIS ON YOUR OWN RISK.

## Tools

* [AVRDUDESS](https://github.com/zkemble/AVRDUDESS)
* [Visual Studio Code](https://code.visualstudio.com)
  * [PlatformIO](https://marketplace.visualstudio.com/items?itemName=platformio.platformio-ide)
* [git](https://git-scm.com/downloads)

## Programmers

Any compatible programmer such as *[USBasp](https://www.fischl.de/usbasp/)* or *[ArduinoISP](https://www.arduino.cc/en/tutorial/arduinoISP)* will be sufficient for this modification. I recommend using *[AVRDUDESS](https://github.com/zkemble/AVRDUDESS)* as this will make this task easier.

## Procedure

### Preparation

First thing is to gain access to the motherboard of your 3D printer. Easily achieved by loosening screws on the printers bottom. Once that is done and cover carefully removed you can proceed to the following steps.

1. Flash ATmega8U2 (USB to UART) firmware
    1. Locate "8U2 ICSP" 6-pin header connector
    2. Connect the programmer to the header
    3. flash [MEGA-dfu_and_usbserial_combined.hex](https://github.com/arduino/ArduinoCore-avr/tree/master/firmwares/atmegaxxu2)
2. Flash ATmega2560 (main micro controller) bootloader
   1. Locate "1280 ICSP" 6-pin header connector
   2. Connect the programmer to the header
   3. flash [stk500boot_v2_mega2560.hex](https://github.com/arduino/ArduinoCore-avr/tree/master/bootloaders/stk500v2)

Note: All preparation flashing is done by AVRDUDESS.

If all flashing was successful restart the board by pressing the reset button near USB connector. Now your board is ready to receive Marlin firmware.

### Flashing Marlin

Under the assumption that you've installed VSCode, PlatformIO and git clone Marlin git repository to your desired folder by navigating to it, right click - Git Bash Here, once in terminal invoke a command

```bash
git clone https://github.com/MarlinFirmware/Marlin.git
```

Now fire up Visual Studio Code and open a Marlin firmware folder with it. Go through the Configuration.h and Configuration_adv.h and configure things you desire. Compile the code and upload it to your FF_CreatorBoard.

Happy printing.
ketukil