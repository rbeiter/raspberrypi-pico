
This is attempt four or so before success.  Went back to basics
went back to the datasheet not the SDK document example.  Was
super simple this time to get it running.  

Currently using the pioasm assembler provided by the sdk, I may
create my own to not be dependent on that one.  


.program squarewave

set pindirs, 1
; Set pin to output
 again:
 set pins, 1 [30] ; Drive pin high and then delay for one cycle
 set pins, 0 [29]; Drive pin low
 jmp again ; Set PC to label `again`

Modification of their example.  This turns on the pin for 30 PIO
clocks and off for 30 pio clocks in a loop.

    PUT32(PIO0_SM0_CLKDIV_RW,0xFFFF0000);

State Machine 0 (SM0) has a clock divisor of 65535 (or is it 65536?
I think the former).  So between the divide by 30 and the
divide by 65535 that is long enough to see the led blink.

The state machine pin is tied to GPIO25 which is the led.  That pin
is set for function 6 which is PIO0.

Basically straight out of the databook.  The periopheral clock setting
as you can see does not seem to matter.  If you uncomment clock_init
then it makes it a 12Mhz clock and in theory it will blink faster (
the internal clock has a very wide range so technically it could be
almost 12MHz but is probably between 4 and 8).



Added a preliminary quick and dirty assembler to generate the pio
instructions.

