+++
date = '2026-05-05T12:41:58+02:00'
draft = false
title = 'Xbox360 Chipless RGH3 glich writeup (Corona v4 4GB Waitsburg)'
summary = "TODO"
tags=["xbox360"]
categories=["Console hacking"]
slug = "xbox360_rgh3_chipless"
+++


## Motivation

I got my first console around the end of elementary school, a PS2 Phat ([SCPH-50004](https://consolemods.org/wiki/PS2:Model_Differences#:~:text=SCPH%2D500XX%20%282003%2D2004)), and it already had a MODBO modchip installed. I played it every day and was fascinated that I could play any game I had a copy of.

Around middle school, I got a PSP ([PSP-1000](https://consolemods.org/wiki/PSP:Model_Differences#:~:text=PSP%2D1000%20%22Phat%2FFat%22%20%282004%2D2007)) and later on a PS Vita ([PCH-2004](https://consolemods.org/wiki/Vita:Model_Differences#PCH-20xx_%22Slim%22_(2013-2019):~:text=PCH%2D20xx%20%22Slim%22%20%282013%2D2019)). The PS Vita was the first console I ever modded.

Since then, I also soft-modded my Japanese Nintendo 3DS and modified my hard-modded PS2 to boot games from an HDD.

This Xbox 360 was the first hard mod I’ve done, and also the first time I started actual SMD soldering.

This project was started around February 2025 and was put down for almost a year (you’ll see why below) before continuing in December 2025. During that time, I did multiple soldering jobs and my skills improved as lot.



## Identification

To perform the hard mod I went by the [Xbox 360 Hub guide](https://xbox360hub.com/guides/rgh-3-guide/) and [MrMario's video](https://www.youtube.com/watch?v=hpOlGeCHwro), cross referencing both of them.

The first step was to identify which specific models and components I have and there are multiple resources to do that.

### Motherboard

Starting off the modding I only had a name: Xbox 360 S Console, written on the barcode sticker of the console.

Motherboard version is based on the current drawn ([octal450 wizard](https://octal450.github.io/identify/)):

![alt text](/img/xbox360/octal_identification.png)

This is what I had:

![alt text](/img/xbox360/current_draw.jpg)

Meaning it was either a CORONA or WAITSBURG. It is important because later steps will have to be done based on specific models.

### POST_OUT

To understand more about POST_OUT read the [official writeup](https://swarm.ptsecurity.com/xbox-360-security-in-details-the-long-way-to-rgh3/). But for now just note the state of it.

![post_out_types](/img/xbox360/post_out_types.png)

In my case its missing:

![post_out_identification](/img/xbox360/post_out_identification.jpg)

A POST_OUT adapter will have to be used and also it means the mobo is either a CORONA v3,4,5 or 6.

### NAND

Identification was performed based on this image:

![nand_types](/img/xbox360/nand_types.png)

The NAND I had:

![nand_identification](/img/xbox360/nand_identification.jpg)

Looks like a 4GB but if we also search for the part number ```H26M31001FPR``` we can check the [datasheet](https://www.datasheets360.com/part/detail/h26m31001fpr/3879213463055891901/) where it states the size of the memory:

![alt text](/img/xbox360/nand_datasheet.png)


### Resistor bridging


![resisitor_bridging_types](/img/xbox360/resisitor_bridging_types.png)

R2C6 & R2C7 are missing:

![resistors_missing](/img/xbox360/resistors_missing.jpg)

**HOWEVER THIS CAN BE IGNORED IF ONLY THE 2 ARE MISSING, SAID IN MRMARIO SLIM CORONA MOD VIDEO. (IT WORKED WITHOUT IT ;))**


### Corona, Waitsburg, Stringra ?

From [ConsoleMods - RGH3](https://consolemods.org/wiki/Xbox_360:RGH/RGH3):


" **Waitsburg** is the successor to Corona and is the final motherboard used in the Xbox 360 S. It is considered a revision of Corona despite having its own name."

"**Commonly referred** to by the community (but not by Microsoft) as "Corona V3" (16MB) and "**Corona V4" (4GB)**. "

"You can also identify if you have a Waitsburg motherboard from a Corona by looking for the part number of ```X862605``` on the bottom left of the PCB."

My part number: 

![mobo_version](/img/xbox360/mobo_version.jpg)


More evidences on Waitsburg here: [XenonLibrary](https://xenonlibrary.com/wiki/Waitsburg). 

### Conclusion of the identification

Multiple evidences suggest that my XBOX 360 S is a **Corona v4** with the following configuration:

- Motherboard type: Waitsburg
- 4GB NAND
- No POST_POUT

## Preparation and soldering

All of the necessary points in the guide were cleaned, tinned and soldered to:

### PLL:

**VERY IMPORTANT! BETWEEN THE TWO PLL POINTS I HAD TO INSTALL A 1K RESISTOR BASED ON THE GUIDE! SRY I DON'T HAVE PICTURES :(** (Put a heat shrinking tube on it and kapton taped it down.)

Note that the via had to be scraped off just a very little to expose the soldier point.

![alt text](/img/xbox360/PLL.jpg)

### SMC_POST1 and SMC_PLL:

![alt text](/img/xbox360/smc_post_and_pll.jpg)

### POST fix adapter

POST1 is connected to the post fix adapter. I ordered the adapter from good old [AliExpress](https://www.aliexpress.com/item/1005006147786174.html). The adapter has to go around the cpu making contact with the springy pin.

![postfix_adapter](/img/xbox360/postfix_adapter.jpg)

During installing the adapter I searched around the internet how to validate the connection of the pin, multiple forums said there has to be resistance across the two points to validate it is properly installed, there were some reddit posts questioning the value of the resistance. I was measuring way off numbers but decided to go with it. 

I used the POST1 pad because that was the only one where I could measure resistance.

At the end it did not matter, just have continuity:

![measuring_the_postfix](/img/xbox360/measuring_the_postfix.jpg)

### Pico Wiring


Pico wiring diagram for the [PicoFlasher](https://github.com/15432/PicoFlasher) which is the original that was used for the exploit, not the other forks.

![pico_wiring_diagram.png](/img/xbox360/pico_wiring_diagram.png)


![soldering_pico1](/img/xbox360/soldering_pico1.jpg)

![soldering_pico2](/img/xbox360/soldering_pico2.jpg)

### Finishing touches

- New cooling paste applied on the CPU.
- Everything kapton taped down neatly, the POST fix adapter is very important.


## The first Execution

When the very first time in February I did the wirings I proceeded to the execution. Soldering job looked okay-ish, as I said in the beginning it was my first time SMD soldering. I checked everything for continuity, all looked great.

The next step was to load up [J-runner](https://github.com/Octal450/J-Runner-with-Extras). Unfortunately this tool only runs on Windows, therefore I spun up a Windows VM and passed through the Pico. Sounds sketchy I know. The first couples of times I did try Wine but something was off, and decided to use a VM.

**J-runner discovered the Pico, I was able to read the NAND and Write [XeLL](https://consolemods.org/wiki/Xbox_360:XeLL)**. At this point I needed to plug in a TV and try to boot into XeLL. Well I couldn't. **Nothing happened, blank screen**.

So the long debugging session started and went on for a lot of days, questing not even the smallest details but my existence as well...

I did hardware level debugging, checked the joints, soldering, the video cabel (I was using RCA->EUROSCART at that point). I de-soldered everything and redid the wiring, now **I couldn't even read the NAND anymore**. Gladly I had the original dump.

I was seraching around the internet, checking github issues, forums and lot of people was mentioning the unreliability of the Pico, so I thought maybe thats my problem. Tried a different wiring and version of the PicoFlasher but nothing was working.

I gave up for the time, was thinking ordering an XFlasher (which costs a lot), but at the end decided to just put the Xbox on the shelf and it sat there until December...

## The second Execution

For the 3rd time I completely re-did my soldering job, those are the picture that you can see above. This time I was using my CRT which I found just a couple weeks earlier lying around on the street. **I still could not read the NAND nor write it.**

I was looking around on the internet to gather more information around XeLL, why does it not boot. For somehow my mind was only focusing on the circular on and off button of the Xbox and I think it was ConsoleMods where I saw or in a random Reddit thread, that your supposed to use the eject button.

**It booted into XeLL. CPU key acquired.**

![xell_booted](/img/xbox360/xell_booted.jpg)

(I was using Ethernet at this point, I could not read the numbers on the CRT.)

I did not re-flash, I only re-did the soldering and it booted into XeLL. **It was probably working all along** and I managed to flash it successfully **I was just not using the correct buttons to start it...**

But I still had an other problem, I **could not communicate with the Xbox through the PicoFlasher**, and thats when I tried the **original exploiters PicoFlasher layout** referenced in his report, couple commits away from the X360Tools/PicoFlasher and using different wiring, and **it was WORKING**!!!

![first_boot](/img/xbox360/first_boot.jpg)

## Post install

For the post install process I followed [MrMarios guide](https://www.youtube.com/watch?v=FNYVGkFJV2s&t=684s) on it.

From that point on my flow is, I use iso2god with Wine then transfer the games via FTP and use Aurora.

(The ftp default credentials are xboxftp:xboxftp)

## Closing thoughts

This was a very fun and challenging experience. I played with the console a couple times and since then its just sitting in the cupboard. Thats how all my consoles end up.You hack it for the fun, and never actually use it.

## References

- Official writeup - [Xbox 360 security in details: the long way to RGH3](https://swarm.ptsecurity.com/xbox-360-security-in-details-the-long-way-to-rgh3/)
- [Xbox 360 Hub guide](https://xbox360hub.com/guides/rgh-3-guide/)
- [How to RGH3 a Xbox 360 Slim (Corona) - Chipless RGH 3.0 Tutorial! - MrMario2011](https://www.youtube.com/watch?v=hpOlGeCHwro)
- [Octal's Xbox 360 Identification Wizard ](https://octal450.github.io/identify/)
- [HYNIX 26nm 32Gb based e-NAND product Family](https://www.datasheets360.com/part/detail/h26m31001fpr/3879213463055891901/)
- [XenonLibrary - Waitsburg](https://xenonlibrary.com/wiki/Waitsburg)
- [ConsoleMods - RGH3](https://consolemods.org/wiki/Xbox_360:RGH/RGH3)
- [J-Runner-with-Extras github](https://github.com/Octal450/J-Runner-with-Extras) 
- [ConsoleMods - Xell](https://consolemods.org/wiki/Xbox_360:XeLL)
- [Setting Up Aurora Dashboard on a JTAG/RGH Xbox 360 - Beginner Setup with XeXMenu & DashLaunch!](https://www.youtube.com/watch?v=FNYVGkFJV2s&t=684s)
