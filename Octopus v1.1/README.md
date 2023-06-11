## Flashing Octopus F446

### CanBoot Cofig
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/a3b5ea41-a841-420e-b2f1-35a7c7dc24c2)


### Klipper USB-CAN-Bridge when using CanBoot or stocl bootloader
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/726a1208-e9cc-4515-aa16-ac9b64eb780f)

### Klipper USB-CAN-Bridge when NOT using Canboot or stock bootloader
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/f8443b90-5b5d-4475-ae52-45137c28cbd7)

```
ls /dev/serial/by-id
```
usb-CanBoot_stm32f446xx_280017001750344D30353320-if00

Need to make sure that this is installed.
```
pip3 install pyserial
```

### Flashing Klipper
`python3 ~/CanBoot/scripts/flash_can.py -f ~/klipper/out/klipper.bin -d /dev/serial/by-id/` Add your ID `usb-CanBoot_stm32f446xx_280017001750344D30353320-if00`
```
python3 ~/CanBoot/scripts/flash_can.py -f ~/klipper/out/klipper.bin -d /dev/serial/by-id/usb-CanBoot_stm32f446xx_280017001750344D30353320-if00
```
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/ab7dd49f-e168-4565-b927-42f7f8bc151a)


Check that is shows as a Can Adapter.
`lsusb`
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/0ca18a32-c340-45a8-86aa-528e38f2f0d6)


Check that the Can network is running.
`ifconfig`
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/7925f87e-d64b-436f-9778-30c2210b32ee)


Query the Can0 network
```
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/bdd0e941-f57a-49e1-b3b7-47f0d665216a)

This is the Mainboards UUID: `45a3695bb38a`


