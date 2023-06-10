## Input shaper

Software installation
```
sudo apt update
sudo apt install python3-numpy python3-matplotlib libatlas-base-dev
```

Next, in order to install NumPy in the Klipper environment, run the command:
```
~/klippy-env/bin/pip install -v numpy
```
Add the following to the printer.cfg file:
```
[resonance_tester]
accel_chip: adxl345
probe_points:
    100, 100, 20  # an example
```
```
ACCELEROMETER_QUERY
```
accelerometer values (x, y, z): -370.102971, -9326.594869, 0.000000
```
MEASURE_AXES_NOISE
```
Axes noise for xy-axis accelerometer: 206.121633 (x), 48.911146 (y), 51.236390 (z)
```
TEST_RESONANCES AXIS=X
```
Resonances data written to /tmp/resonances_x_20230610_090838.csv file
```
~/klipper/scripts/calibrate_shaper.py /tmp/resonances_x_20230610_090838.csv -o /tmp/shaper_calibrate_x.png
```
 ![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/1c2407f9-f545-4918-aaff-1c98b93f41de)

![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/6bf2e58f-3674-44ad-a9aa-dac3d0b604b2)


```
TEST_RESONANCES AXIS=Y
```
Resonances data written to /tmp/resonances_y_20230610_091245.csv file
```
~/klipper/scripts/calibrate_shaper.py /tmp/resonances_y_20230610_091245.csv -o /tmp/shaper_calibrate_y.png
```
![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/5e6f75a3-7658-4f16-b95a-52c8f034d9e3)

![image](https://github.com/baz-snow-ss/Mercury-One-Zero-G/assets/99566898/5ea5038e-77a2-4756-ad6c-aa37432f2110)


Add to the Printer.cfg file
```
[input_shaper]
shaper_freq_x: 70
shaper_type_x: mzv
shaper_freq_y: 34.6
shaper_type_y: mzv
```
