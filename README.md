ECE382_Lab2
===========
created by Austin Bolinger
ECE 382: Lab 2
Start Date: 08 SEP 14
Edited: 14 SEP 14
Edited: 14 SEP 14
End Date: 19 SEP 14

Lab 2 is Crptography. Decoding an encoded message given a key or not given a key.

#Objective
The purpose of this lab is to understand subroutines. We will also us call by value or call by reference to pass arguments to the subroutines. encryption for this lab will be a simple XOR function given a key. A message will be given in ROM. It will be encoded with the key that is also given in ROM. Using XOR functions and subroutines, I must decode the message and store it in RAM.

#Prelab

###Pseudo Code
o	Type encrypted message in ROM

o	Type key in ROM

o	Set apart RAM storage for results

o	Set up registers as pointers for encryption, decryption, and the key

o	Sub 1

-	Read in message

-	Read in Key

-	Call Sub 2

-	End of message jump

o	Sub 2

-	XOR key with message

o	End 



###Flow Chart
![Flow Chart](https://github.com/Austinbolinger/ECE382_Lab2/blob/master/flowChart.JPG?raw=true "Flow Chart")

