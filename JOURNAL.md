# Journal!

Total so far: 2.5hrs across 3 journals

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
