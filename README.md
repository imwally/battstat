# battstat

This is a tiny shell script that displays the status of your battery along with an icon indicating whether it's charging or discharging as well as the time remaining. Currently macOS is 100% supported while Linux is not too far behind.

### macOS

Battery details are collected via `pmset(1)`.

### Linux

Power information is collected via sysfs.

### Charging
![battery charging](https://github.com/imwally/battstat/raw/master/img/charging.png)

### Discharging
![battery discharging](https://github.com/imwally/battstat/raw/master/img/discharging.png)
