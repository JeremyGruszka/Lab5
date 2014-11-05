Lab5
====
##Lab 5

####Day 1 labwork

Questions:
1. How long will it take the timer to roll over? 16ms (line 56)
2. How long does each timer count last?
3. Fill out the following picture with lines from the for loop in their locations.

![alt text](https://raw.githubusercontent.com/JeremyGruszka/Lab5/master/Day1.PNG "Day 1")

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
