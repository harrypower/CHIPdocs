# What is needed!
* Windows 10 machine!
* USB A to micro B cable
* USB charger for power
* USB to uart cable with jumper wires(PL2303 USB to Serial cable)
* Internet connection
* Chrome browser (updated), on windows machine, only for flashing
* Wifi router for connecting CHIP to network
* Jumper wire for CHIP to enter flashing mode
* Putty for windows installed and working

# What will it do!
This will setup CHIP for use with software i use for programing in Gforth and c/c++ and a wifi connection to ssh into headlessly!

# Flashing the CHIP for headless use!
* [CHIP's online docs for flashing](http://docs.getchip.com/chip.html#flash-chip-with-an-os)

Need to get driver for flashing so open up chrome browser and go to the following page and install the driver!
* [CHIP chrome flasher](http://flash.getchip.com/)
Place jumper wire connecting Pin 7 and Pin 39 on header U14 (FEL pin and GND). The image shows this!
![Fel mode wiring](uboot_fel_jumper.jpg)

Now plug the USB micro B end into CHIP and the other USB end into windows computer!  Note ensure you have the above web page open
for the flashing process.  Once connected and powered the web page will change and show a message about reading CHIP.
If this process does not return shortly then the USB cable is not going to work find a new one. Also restarting Chrome seems to work sometimes if issues continue!
Once the CHIP has been identified you are given options for what to flash onto the CHIP.  Pick Headless OS then press
the flash button at the bottom of the new window that pops up! This will take some time just let it continue (5 to 10 min).
Note there maybe messages from windows about USB device not detected just ignore them!  
The pop up window should tell you when it is done and if all is ok with flashing!
