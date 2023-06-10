## EBB36 Flashing

Add a jumper as shown in the image below so the board can be powered via a USB connection
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/cd0944a8-8e53-47a7-bebe-bb95da758dd5)

Connect your device to your Pi via USB

Press and hold the `RESET` and `BOOT` buttons down (button locations shown in step 1)

Release `RESET` button
Release `BOOT` button
The device should now be in DFU mode. Verify this via the `lsusb` command, which should look something like this:
```
Bus 001 Device 005: ID 0483:df11 STMicroelectronics STM Device in DFU Mode
```
