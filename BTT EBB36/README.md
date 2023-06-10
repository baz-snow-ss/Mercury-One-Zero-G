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

### CanBoor Config
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/1ca575fa-94b8-430f-a05c-4e938c5acfd6)

### Klipper when using CanBoot
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/578a743d-00b4-4261-8b22-6e3cbed7ca45)


### Klipper when NOT using CanBoot
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/7996c85d-0699-446b-a703-3f1cb153ce0b)

```
sudo apt update
sudo apt upgrade
sudo apt install python3 python3-pip python3-can
pip3 install pyserial
```

### Installling CanBoot

```
cd ~
git clone https://github.com/Arksine/CanBoot
```
```
cd ~/CanBoot
make menuconfig
```
Pick the correct settings for CanBoot config
```
make clean
make
```
Attch the USB, put the EBB36 in DFU Mode and check that it is.
```
dfu-util -l
lsusb
```
You can then flash the CanBOOT firmware to your toolhead board by running.
```
dfu-util -R -a 0 -s 0x08000000:force:mass-erase:leave -D ~/CanBoot/out/canboot.bin -d 0483:df11
```
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/a8043d01-fd93-44b5-a05e-a576f8e79b3c)


### CanBooT is now installed.
```
python3 ~/CanBoot/scripts/flash_can.py -i can0 -q
```
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/8dfb9c6c-f76a-4b9f-b06f-384e1da60e72)
```
Detected UUID: 45a3695bb38a, Application: Klipper
Detected UUID: 918c224b9a4c, Application: CanBoot
```

### Installing Klipper

Pick the correct setting for Klipper config
```
cd ~/klipper/
make menuconfig
```
```
make clean
make
```
If you have CanBOOT installed
Run a `python3 ~/CanBoot/scripts/flash_can.py -i can0 -q` and take note of the CanBoot device that it shows:
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/35e531c9-25b1-4ce2-b1cf-c90e0f00e260)
Then run the following command to install klipper firmware via CanBOOT. Use the UUID you just retrieved in the above query.
```
python3 ~/CanBoot/scripts/flash_can.py -i can0 -u 918c224b9a4c -f ~/klipper/out/klipper.bin
```
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/07f23b82-4a3f-42db-8724-e8862690f301)

One the flash has been completed you can run the
`python3 ~/CanBoot/scripts/flash_can.py -i can0 -q` command again. This time you should see the same UUID but with "Application: Klipper" instead of "Application: CanBoot"
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/bcc1ebae-6e28-4b3a-b39c-6e969828b5c2)

If you don't have CanBOOT installed
To flash, connect your toolhead board to the Pi via USB and put it into DFU/BOOT mode (your toolhead board user manual should have instructions on doing this).

```
cd ~/klipper
make flash FLASH_DEVICE=0483:df11
```
where the FLASH_DEVICE ID is the address of the USB device you noted down above.
### Klipper is now installed.

You can now run the Klipper canbus query to retrieve the canbus_uuid of your toolhead board:
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/dcd08846-b539-480d-820d-b4d82566a773)

