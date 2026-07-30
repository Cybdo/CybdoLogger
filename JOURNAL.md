# Journal!

Total so far: 0.5hrs across 1 journal

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
