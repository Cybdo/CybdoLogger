# Journal!

Total so far: 4 hrs 35 mins across 5 journals

## 30/07/2026 - research and planning
**(30 mins)**

I spent some time looking into usb keyloggers since i always wanted one. 

I have since found out that wireless keysniffers are basically impossible since all modern keyboards have some form of encryption and use varying protocols (or bluetooth, but I'm not gonna break into bluetooth lol)

Instead, here's what i've found:
- https://github.com/therealdreg/pico-usb-sniffer-lite - full firmware for a keylogger with rp2040 (looks incredibly painful)
- https://forums.raspberrypi.com/viewtopic.php?t=11558 - forum thread about using GPIO as a secondary USB interface on rp2040
- https://github.com/sekigon-gonnoc/Pico-PIO-USB - PIO implemetation of USB on pi pico (rp2040)

so i guess now the plan is to have a board with 1 usb-a female and 1 usb-a male that essentially acts as a MITM device between a usb keyboard and a host device (eg computer).

```
Keyboard -> USB Female (PIO) -> MCU (RP2040) -> USB Male (primary USB) -> Computer
```

and the RP2040 analyses the data from the keyboard while passing it along unmodified to the host device and stores it in an SD card.

I also want to have a button where I can hold upon boot to have the device show up as USB mass storage to show the stored data, but that can be a later me problem. For now, just taking the SD card out and using it should be good enough.

Tomorrow i start work on the pcb!!

## 01/08/2026 - schematic work
**(1 hour 15 mins)**

and so i started with the schematics

it shouldnt be too difficult, 2 USB ports, voltage reg, rp2040 minimum system and sd card

used lcsc manager to import usb female + male and sd card components so i dont have the issue of mismatched footprints (cough cough cybdokey)

<img width="540" height="305" alt="image" src="https://github.com/user-attachments/assets/959c7bd5-4798-4c38-896d-83cb6d113c0c" />

usb upstream and downstream both with respective usb protection

i am so confused how does this work i thought sd cards were spi 😭😭

<img width="558" height="607" alt="image" src="https://github.com/user-attachments/assets/73078d49-237d-4f11-840f-e24dcd96dadd" />

nvm 
i reckon i got it

<img width="358" height="329" alt="image" src="https://github.com/user-attachments/assets/00640757-8be6-4360-b276-9840981ea7d5" />

<img width="1015" height="705" alt="image" src="https://github.com/user-attachments/assets/c722aab4-6796-48af-9b24-ce59397443fd" />
that should be the minimum system done now! i also spent some time organising the schema. I deliberately left all the GPIO unconnected- ive found that its easier for me to lay out the pcb then figure out what gpios are easiest to route

## 01/08/2026 - pcb routing
**(45 mins)**

second journal of the day!!

im gonna get going with layout + routing what i can. the idea is to keep it as small as possible as to be as hidden as possible.


i forgor to assign footprints 😭


hopefully this works aaaaaaaaaaa

hopefully i can keep everything on one side

pcb is currently 50mm long

<img width="169" height="453" alt="image" src="https://github.com/user-attachments/assets/4fd69a51-2ada-499c-b8a4-83cd088d7f8f" />

hadf to swap this around bcs of how the footprint is laid out

<img width="902" height="446" alt="image" src="https://github.com/user-attachments/assets/05ecbf0d-7ce1-4813-9a0f-126c27147f5b" />

had to change all the net names for kicad to recognise the diff pairs

<img width="725" height="657" alt="image" src="https://github.com/user-attachments/assets/a81bb3e3-5e26-4626-a18b-e314e06fe1c0" />

this is possible right :pf:

<img width="268" height="708" alt="image" src="https://github.com/user-attachments/assets/1cb2a224-7092-412a-83fb-c4aa46f94192" />

new idea- im mvoing the sd card slot up and putting everything else under


cooked

<img width="592" height="666" alt="image" src="https://github.com/user-attachments/assets/a2a7f87f-c04e-444c-96ff-9eafe6b583a9" />



<img width="210" height="668" alt="image" src="https://github.com/user-attachments/assets/8bd01a81-2549-494f-8c39-d8ca599fbd52" />

what if i put the sd slot under hmm.. its annoying to handsolder but will make my life considerably easier


i spent the next like 15 minutes experimenting with different layouts to no avail :pf: i reckon current one is optimal since rp2040 gets the most room and tehres enoguh space for the xtal and SD card GPIO. button and bootsel will have to go under tho, no complaints about that


## 02/08/2026 - more rounting
**(1.5hrs)**

added passives to sd card
<img width="657" height="662" alt="image" src="https://github.com/user-attachments/assets/ebcb0ead-cb1b-490c-a97c-272c5453be44" />



differential pairs and usb, respectfully, fuck you

<img width="695" height="715" alt="image" src="https://github.com/user-attachments/assets/da179e88-e97e-4685-93ff-c1cb05a16ede" />

WHY IS IT FLIPPED WHY BRO

its fine im just going to put the usb male on the other side so d+ and d- swap

why are rp2040's usb pins flipped man

<img width="1128" height="518" alt="image" src="https://github.com/user-attachments/assets/2d6022c0-b19e-47ef-9cc1-87b409563181" />


ok my life is a bit easier ig

<img width="1173" height="567" alt="image" src="https://github.com/user-attachments/assets/76e52ac3-0fb0-444d-b808-5ffcb20a2524" />


oh yea claude told me to add decoupling caps to the sd card + pullups on miso and mosi so im gonna do that asw

i have been neglecting the silkscreen

<img width="506" height="607" alt="image" src="https://github.com/user-attachments/assets/ea423e10-0883-4ea6-9dcd-54010e96d519" />

i have still neglected the silkscreen but more stuff has happened

<img width="1027" height="855" alt="image" src="https://github.com/user-attachments/assets/6369cc6e-d009-48cc-b0fa-62f7dd363f39" />

what even is a groud plane 🥀 like my back layer is p clean rn icl but i cant figure out how to route my sd data lines cleanly 😭

nevermind

<img width="429" height="572" alt="image" src="https://github.com/user-attachments/assets/01533b4a-e5c3-48ae-8e8f-bbb7d67df3fa" />

cooked

<img width="519" height="664" alt="image" src="https://github.com/user-attachments/assets/1706f4df-fff6-4a0e-ae96-535d26a8b172" />


what did i even do today

i
- figured out a layout im happy with (sd card on back side)
- moved stuff around
- routed
- added bootsel + read_sd buttons and jumpers
- added passives for the sd card 

geez taht doesnt sound like 1.5 hrs of work but i swear it is 😭

# 02/08/2026 - hopefully done with routing maybe
**(35 mins)**

ok so according to Pico-PIO-USB, d+ and d- can be on any two sequential gpio, and d+ must be the lower numbered one of the two

this should be fine then

<img width="771" height="649" alt="image" src="https://github.com/user-attachments/assets/4de6f03c-0a4d-4d1f-993a-fc0c0bc37aef" />


silkscreens cleaner now

<img width="881" height="444" alt="image" src="https://github.com/user-attachments/assets/6ef52ac1-816b-47cc-b339-2392005ded89" />


wired up the SPI for SD card asw, i had to move stuff around to line up with the rp2040's SPI0 interface on gpios 0-3 (the other two are just digital inputs for detection)

<img width="399" height="329" alt="image" src="https://github.com/user-attachments/assets/fa18c18b-f8c8-41e6-8620-7f13fcfb7cfc" />

i also moved some stuff around and did some power stuff at some point just to make room for the spi lines whilst trying my best to maintain a ground plane

almost ALMOST done with hw but it also needs a load of polish icl

<img width="547" height="787" alt="image" src="https://github.com/user-attachments/assets/4eceb220-531f-493a-b4eb-6b44ad00ba14" />

