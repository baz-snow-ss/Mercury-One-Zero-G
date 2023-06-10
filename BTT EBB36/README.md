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

