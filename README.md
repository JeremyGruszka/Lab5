Lab5
====

####Day 1 lab work

Questions:
1. How long will it take the timer to roll over? 16ms (line 56)
2. How long does each timer count last?
3. Fill out the following picture with lines from the for loop in their locations.

![alt text](https://raw.githubusercontent.com/JeremyGruszka/Lab5/master/Day1.PNG "Day 1")

The following two charts I got by plugging my IR sensor into an oscilloscope.  For the day 1 lab work, I used the DFEC remote #10.

|__Pulse__|__Duration__|__Timer A counts__|
|:-----|:-----|:-----|
|Start logic 0 half-pulse|9.02 ms|8902|
|Start logic 1 half-pulse|4.48 ms|4411|
|Data 1 logic 0 half-pulse|600 us|587|
|Data 1 logic 1 half-pulse|1.68 ms|1642|
|Data 0 logic 0 half-pulse|600 us|587|
|Data 0 logic 0 half-pulse|540 us|587|
|Stop logic 0 half-pulse|until next packet|until next packet|
|Stop logic 1 half-pulse|until next packet|until next packet|

|__Button__|__Code (not including start and stop bits)__|
|:-----|:-----|
|0|01011001101001100000101011110101|
|1|01011001101001100101101010100101|
|2|01011001101001100111101010000101|
|3|01011001101001100111001010001101|
|Power|01011001101001101110101000010101|
|Vol+|01011001101001100100001010111101|
|Vol-|01011001101001100101001010101101|

####Day 2 lab work

The purpose of day 2 lab work was to demonstrate to your instructor that your code can receive and decode button presses from the remote control.  The required functionality was to turn an LED on and off with one button on the remote, and turn another LED on and off with a different button.

I was able to achieve required functionality using the remote for the TV in my room.  I was not sure how to prove that the code worked, so if you would like me to bring in the remote and show you that the code works, I can.

In order to achieve required functionality, I had to first debug timing sequences into 1's and 0's and store them in a packet of data.  Here is the code I wrote to do that:

```
pulseDuration = TAR;
if ((pulseDuration > minLogic0Pulse) && (pulseDuration < maxLogic0Pulse)) //puts a logic 0 into the IrPacket
{
IrPacket = (IrPacket << 1) | 0;
}
if ((pulseDuration > minLogic1Pulse) && (pulseDuration < maxLogic1Pulse)) //puts a logic 1 into the IrPacket
{
IrPacket = (IrPacket << 1) | 1;
}
```

The next thing I had to do was to determine which button the IrPacket held data for and turn on or off an led based on that information.  I turned on the green led with the volume up button, turned off the green led with the volumen down button, turned on the red led with the channel up button, and turned off the red led with the channel down button.  Here is the code I wrote to do that:

```
void main(void) 
{
  initMSP430(); // Setup MSP to process IR and buttons
  while(1) 
  {
    while(newIrPacket == FALSE); //waits for a new IrPacket
    if (IrPacket == VOL_UP) P1OUT |= BIT6; //turns on green led
    if (IrPacket == VOL_DW) P1OUT &= BIT6; //turns off green led
    if (IrPacket == CH_UP) P1OUT |= BIT0; //turns on red led
    if (IrPacket == CH_DW) P1OUT &= BIT0; //turns off red led
    newIrPacket = FALSE;
  } // end infinite loop
} // end main
```

I had constants for both these portions of code that I just wrote, here they are:

```
#define	averageLogic0Pulse	550
#define	averageLogic1Pulse	1650
#define	averageStartPulse	4500

#define	minLogic0Pulse	averageLogic0Pulse - 100
#define	maxLogic0Pulse	averageLogic0Pulse + 100
#define	minLogic1Pulse	averageLogic1Pulse - 100
#define	maxLogic1Pulse	averageLogic1Pulse + 100
#define	minStartPulse	averageStartPulse - 100
#define	maxStartPulse	averageStartPulse + 100

#define	VOL_UP	0xE0E0E01F
#define	VOL_DW	0xE0E008F7
#define	CH_UP	0xE0E048B7
#define	CH_DW	0xE0E0D02F
```

Getting this required functionality was quite possibly the most frustrating thing I have ever had to do in my time at the academy.  While the code is very simple, it was just not working.  I knew I had written good code because I have roughly 4 years of programming experience under my belt and I knew that the code I wrote should have been working.  After hours of staring at my code and playing with it, trying to get it to work and failing, I went to Dr. Coulston for help.  He cleaned up my code a little bit and made it a little bit easier to read, but didn't really change all that much fundamentally.  He tested the code with the remote in his office and it worked.  After seeing that it worked, I thanked him for his help and went down to the lab to adjust my values for the remote I was using.  However, once I got down to the lab, the program was no longer working.  I knew I changed nothing in between Dr. Coulston's office and the lab, so I figured it must be the remote I was using.  I tried 5 different remotes provided by the DFEC, but none worked.  In a panic, I went to Captain Trimble's office to see if she could figure out what was going on.  She could not figure out what was wrong in the time she had left in her office, so I gave up for the night and decided that I would work on it diligently on Veteran's Day, knowing that if I could not get the darn program to work, I would fail the class.  I woke up Veteran's day and went to work.  I tried running my program one last time with a remote I had in my room, and it worked! By the grace of God, my program liked the remote I had in my room.  I think the program I had written worked all along, I just happened to keep using remotes that didn't work, and that's why I could not get the results I wanted out of my program.

I did not attempt A functionality because of the distressing ordeal I went through trying to get required functionality to work.
