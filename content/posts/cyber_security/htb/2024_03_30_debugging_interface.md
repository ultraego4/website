+++
title = 'HTB - Debugging Interface - Intro to Hardware Hacking'
date = 2024-03-30T18:32:11+01:00
draft = false
tags=["htb","hardware","reversing"]
categories=["ctf"]
summary= "“We accessed the embedded device’s asynchronous serial debugging interface while it was operational and captured some messages that were being transmitted over it. Can you decode them?”"
+++

YELLO!!!

Long time no see...BUT NEW SERIES!!!!! CTF writeup.

I started the Intro to Hardware Hacking on HackTheBox, this is gonna be the first writeup about the debugging interface challenge.

## Challenge description

"We accessed the embedded device's **asynchronous serial debugging interface** while it was operational and captured some messages that were being transmitted over it. Can you decode them?"


## Initial findings

When you first download the given files, its in a zip. After i extracted it, it gave me a .sal file. I've never seen this kind of file extension so i did some searching on the net. Searched for like 10 mins i didn't find shit, most of the sites pointed to its being a mysql extension but no luck with trying to run it with mysql. I almost scrolled to the bottom of the search results and found a website with a title like and description like this:

![search_result](/images/2024_03_30_debugging_interface/serach_result.png)

Seems its some kind of external debugging tool and it also has a software called Logic.

## Decoding the digital signal

After installing the software i was prompted to import a file so i was able to import the .sal file. On one channel I was able to see a digital signal in a time frame. This wasn't the first time ive seen a program or an output like this. Like a month ago i was watching embedded reversing videos and in one of them there was something related to this and i remembered he was switching the bitrate of the signal. So i went down that route, i found something on the websites doc about how i can find out, calculate the bitrate. Theres an extension in the program which calculates the average frequency of the signal. It was around 31.23kHZ, i converted the kHZ to bits/s and it was around 31230/s.

![digital_signal](/images/2024_03_30_debugging_interface/digital_signal.png)

 I changed the baud rate to this and the bits to represent ascii characters and i was able to see the flag. 
 
 ![changing_baudrate](/images/2024_03_30_debugging_interface/changing_baudrate.png)

 BOOOOOOOM--------------

 ![flag](/images/2024_03_30_debugging_interface/flag.png)



