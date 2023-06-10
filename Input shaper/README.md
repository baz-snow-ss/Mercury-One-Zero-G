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
```
accelerometer values (x, y, z): -370.102971, -9326.594869, 0.000000
```
```
MEASURE_AXES_NOISE
```
```
Axes noise for xy-axis accelerometer: 206.121633 (x), 48.911146 (y), 51.236390 (z)
```
```
TEST_RESONANCES AXIS=X
```
```
Resonances data written to /tmp/resonances_x_20230610_090838.csv file
```
```
~/klipper/scripts/calibrate_shaper.py /tmp/resonances_x_20230610_090838.csv -o /tmp/shaper_calibrate_x.png
```
 
