upload_K28_smt_contained is used to setup K28 SMT v1.1 7/2019

AVRDUDE version 5.10 download: http://download.savannah.gnu.org/releases/avrdude/
USBtinyISP driver download: https://learn.adafruit.com/usbtinyisp/drivers

The batch file runs series of commands using command prompt in windows
The whole folder titled K28_code needs to be copied to the local PC from the network drive to function properly

If the code is changed, a new hex file needs to be generated using the Arduino IDE
Sketch -> Export Compiled Binary



PRE-SETUP:

- Connect K28 using the jig provided (This contacts 6 pins needed for software changes: 5V, GND, SCK, MISO, 	MOSI, RESET
- Connect programmer to the PC
- Open device manager in windows and you should see libusb-win32 devices
	This verifies the USBtiny programmer is detected and the drivers are working correctly




SETUP USING BATCH FILE (RECOMMENDED):

- Copy the folder titled "K28_Code" to your desktop from the network drive: "Z:\Shop\Mason R&D\K28 Surface 	Mount\Programming"
- Open the folder and run "upload_K28_cmt_contained"
- Press space or any other key to walk through automated setup process

 


SETUP USING ARDUINO IDE & COMMAND PROMPT (ALTERNATIVE):

Tools -> Programmer -> USBtinyISP
Tools -> Board -> Arduino Nano
Tools -> Processor: ATmega328p (Not old bootloader)

- Tools -> Burn Bootloader
- Sketch -> Upload using programmer
- Open command prompt in Windows and type: avrdude -c usbtiny -p m328p -U lfuse:w:0x62:m
	This resets the fuse to use the internal oscillator
- Also in command prompt type: avrdude -c usbtiny -p m328p -U lfuse:r:-:h
	This check the fuse bits to ensure it has been reset.
	Low fuse bit "lfuse" should read 0x62 if it worked