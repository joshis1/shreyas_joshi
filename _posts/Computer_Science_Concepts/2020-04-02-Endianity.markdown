---
layout: post
title:  "Endianity"
date:   2020-04-02 14:13:31 +1300
categories: Computer_Science_Concepts
---

This article is all about endianity. Endianity is all about how a word is stored in the computer memory.
There are two types of endianity - Big Endian and Little Endian.

**What is Big Endian?**

The way human beings write can be considered Big Endian. We first write MSB and then write LSB.
Basically, the lower address has MSB and the higher address has LSB.

**What is Little Endian?**

The little endian is liked by the machines and it is opposite to how human beings do write.
Basically, Least significant byte is written first and then Most significant byte is written.
In computer science terminology, least significant byte is written in the lower address and
the most significant byte is written in the higher address. 

**Why do machines like little Endian?**
This is because addition, subtraction operations are easier in little endian.
Why because we start adding from the LSB and then we carry forward it to the next MSB.
So, in general while machine is adding the LSB, it can fetch the MSB. Thus, it can do things in 
parallel and this will make things faster. In general, human beings like big endian and machines like
little endian.

**Does byte is big endian or little endian?**

There is no big endian or little endian within the byte. The byte is the fixed minimal data.
In short, a 32 bit address i.e. 4 bytes are arranged either in the big endian or little endian.
In big endian, the the most significant byte is stored in the lower address and the least significant byte
is stored in the higher address.

**Why Endianity matters?**
Assume two machines or two different processor architecture wants to communicate with each other.
Let's assume machine A processor architecture is big endian and machine B processor architecture is little endian.
Now, if machine A sends data 0x10FF to machine B. The machine B will interpret data as 0XFF10. So, this will be a
big problem. So, it is very important to know endianity. How do we tackle this issue? The answer is serialisation.
By serialising, the information is stored in a particular format for e.g. big endian and when the machine receives it uses de-serialising to re-interpret the information correctly. For e.g. in network, the network byte address is 
stored in big endian. However, we use htonl() which reverses the byte order in little endian machine. There is no 
operations in big endian. Basically, htonl() is used to convert host unsigned long byte address to network unsigned
long byte address. This is often used with IPv4 address. The htons() is used to convert host unsigned short byte address to network unsigned short byte address. This is often used with tcp port or udp port numbers.

**Why do they call htonl?**
Basically htonl() means host to network. This means whatever the data you have in your host machine convert into 
a format that network will understand. The network understands big endian. So, basically, it converts your machine 
data i.e host machine data to big endian. If your machine/host is already big endian then it won't have any affects.
The htonl is basically host to network unsigned long byte used for IPv4 address. 
The htons is basically host to network unsigned short byte used for TCP/UDP port number.

This brings an end to this article. 

