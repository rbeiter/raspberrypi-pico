
This example switches to the XOSC using the on board 12MHz crystal.

As written the LED will change state every 10 seconds.  If you comment
out the clock_init() call then it will use the ring oscillator, which
could drift that fast but is probably going to be slower so the 
LED state change will be longer than 10 seconds.

This program runs from SRAM, I used the flash_nuke.uf2 program from
the pi folks, and press the reset button or use the reset command on
openocd then copy notmain.uf2 over.
