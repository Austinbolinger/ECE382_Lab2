ECE382_Lab2
===========
created by Austin Bolinger
ECE 382: Lab 2
Start Date: 08 SEP 14
Edited: 14 SEP 14
Edited: 14 SEP 14
End Date: 19 SEP 14

Lab 2 is Cryptography. Decoding an encoded message given a key or not given a key.

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

#Test Cases
###Required Functionality
Encrypted Message:
0xef,0xc3,0xc2,0xcb,0xde,0xcd,0xd8,0xd9,0xc0,0xcd,0xd8,0xc5,0xc3,0xc2,0xdf,0x8d,0x8c,0x8c,0xf5,0xc3,0xd9,0x8c,0xc8,0xc9,0xcf,0xde,0xd5,0xdc,0xd8,0xc9,0xc8,0x8c,0xd8,0xc4,0xc9,0x8c,0xe9,0xef,0xe9,0x9f,0x94,0x9e,0x8c,0xc4,0xc5,0xc8,0xc8,0xc9,0xc2,0x8c,0xc1,0xc9,0xdf,0xdf,0xcd,0xcb,0xc9,0x8c,0xcd,0xc2,0xc8,0x8c,0xcd,0xcf,0xc4,0xc5,0xc9,0xda,0xc9,0xc8,0x8c,0xde,0xc9,0xdd,0xd9,0xc5,0xde,0xc9,0xc8,0x8c,0xca,0xd9,0xc2,0xcf,0xd8,0xc5,0xc3,0xc2,0xcd,0xc0,0xc5,0xd8,0xd5,0x8f
Key:0xac
###B Functionality
Encrypted Message:
0xf8,0xb7,0x46,0x8c,0xb2,0x46,0xdf,0xac,0x42,0xcb,0xba,0x03,0xc7,0xba,0x5a,0x8c,0xb3,0x46,0xc2,0xb8,0x57,0xc4,0xff,0x4a,0xdf,0xff,0x12,0x9a,0xff,0x41,0xc5,0xab,0x50,0x82,0xff,0x03,0xe5,0xab,0x03,0xc3,0xb1,0x4f,0xd5,0xff,0x40,0xc3,0xb1,0x57,0xcd,0xb6,0x4d,0xdf,0xff,0x4f,0xc9,0xab,0x57,0xc9,0xad,0x50,0x80,0xff,0x53,0xc9,0xad,0x4a,0xc3,0xbb,0x50,0x80,0xff,0x42,0xc2,0xbb,0x03,0xdf,0xaf,0x42,0xcf,0xba,0x50,0x8f
Key: 0xacdf23
Notice the key is longer than one byte.
###A Functionality
0x35,0xdf,0x00,0xca,0x5d,0x9e,0x3d,0xdb,0x12,0xca,0x5d,0x9e,0x32,0xc8,0x16,0xcc,0x12,0xd9,0x16,0x90,0x53,0xf8,0x01,0xd7,0x16,0xd0,0x17,0xd2,0x0a,0x90,0x53,0xf9,0x1c,0xd1,0x17,0x90,0x53,0xf9,0x1c,0xd1,0x17,0x90
Notice no key.


#Hardware Schematic

![MSP430G2553](http://www.kerrywong.com/blog/wp-content/uploads/2012/03/MSP430G2ExtProg3.jpg?raw=true "MSP430G2553")

![MSP430G2553 Schematic](http://cnx.org/resources/485bbea47ead3338e654ae805f15bc09/graphics3.png?raw=true "MSP430G2553 Schematic")

#CODE
###Required Functionality Code
https://github.com/Austinbolinger/ECE382_Lab2/blob/master/requiredFunctionality.txt

My understanding of the code took a while to develop. I did not understand why I needed to push and pop things until I realized that it would make sense to build good coding habits. The point of this lab was to use subroutines. So I was surprised when I saw how little code I for each routine. I recognized that this functionality would require pointers like last lab. This time I focused on the subroutines as requested. 

###B Functionality Code
https://github.com/Austinbolinger/ECE382_Lab2/blob/master/BFunctionality.txt

I mimicked the decrementing message length code but for the key in order to add the key loop. But, this time I added extra code to reset the key length to the original length when the decremented counter reached zero.


###A Functionality Code
https://github.com/Austinbolinger/ECE382_Lab2/blob/master/AFunctionality.txt

A functionality was hard. I decided to brute force the attack and look for patterns. Dr. York tried explaining to me the fact that there was two patterns, an odd byte and even byte pattern. And, for the life of me, I did not understand. I finally figured it out though.


#Debugging/Testing
When debugging the required functionality, I found that I did not understand the addressing order. I was using pointers but it took me awhile and a few EI sessions to finally see that my pointers were locations as I wanted and that I needed another register for the value at that location. After that my result was correct. My next task was to create a quick method to find the length of the message. So I added a label and a stop code to use a quick subtraction method to find the length of the message. I also added a quick decrementing loop to run the entire length of the message.

When debugging the B functionality, I found out I had the same problem as in the required functionality. I was pointing to the address location and not storing the correct code. I later found out after finding the answers to the first two codes that my code was faulty because it only worked with code that had odd byte numbered keys. I then changed my stop code from .word to .byte. Problem solved.

When debugging the A functionality code, I spent way too much time not understanding the problem. After Dr. York finally realized why I was just getting periods for every other letter, my progress turned for the better. He explained how there are many more codes in ascii than just letters, and if the computer does not have a letter for the code given by my answer, the computer will put a period in its place. After I understood that I needed to have a low ascii value for key part one and a high ascii value for key part two, I decided to just brute force and get lucky. After at least 20 tries I decided that if I could look at the answers in two parts and try and find the patterns that way, why not look at the given coded message and try to figure it out there first? So I organized the message in two parts. I realized two things: one that there were patterns within each grouping and that the last character was most likely a period. So I used a XOR calculator and the ascii value for a period and the last letter in the message to find the second half of the key. Next I guessed that there were most likely vowels in the other half of the message. So I picked out a few repeating values and brute forced those with vowels. On about the fourth try, I found the answer and was relieved that I was able to crack the code. 


### Final Code
https://github.com/Austinbolinger/ECE382_Lab2/blob/master/AFunctionality.txt

#Results
I showed my results to Dr. York for required and B functionality in class on lesson 11. Later that day before COB, I showed my A functionality to Capt Trimble. My answers are: Congratulations!  You decrypted the ECE382 hidden message and achieved required functionality#; The message key length is 16 bits  It only contains letters, periods, and spaces#; and Fast. Neat.  Average. Friendly. Good. Good.

#Documentation
Capt Trimble helped me understand the xor function. In the process I was able to see that my actual error was using the wrong values.

Dr. York talked to me about how to approach the A functionality. He suggested brute force and looking for patterns. In class he mentioned the odd and even byte patterns which was the most useful. 
