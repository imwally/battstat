# battstat

`battstat` is a tiny shell script that displays formatted information about the status of your battery. It's best when used as apart of your __tmux__ status line. Really though, any place where a shell script can be executed should work just as well.

Information is displayed in the order the format tokens are written. For example, the command given in the screenshots below is `battstat --percent-when-charged {i} {t} {p}`. This will display an icon, the time remaining when charging and discharging, and finally the percentage but only when the battery is fully charged. Format tokens can be written in any order and as many times as you like, although I'm not sure why you would use more than one of each at a time.

![battery charging](https://github.com/imwally/battstat/raw/master/img/charging.png)
![battery discharging](https://github.com/imwally/battstat/raw/master/img/discharging.png)
![battery full charged](https://github.com/imwally/battstat/raw/master/img/charged.png)

The following Operating Systems are supported (almost).

### macOS 100%

Details are collected via `pmset(1)`.

### Linux 99%

Details are collected via [sysfs](https://en.wikipedia.org/wiki/Sysfs).

_Note: Finding the time remaining is the only outstanding problem. The rest of the code is in place and ready to go._

### Install

First grab the script. Here are a few options:

      * Download and extract the [zip](https://github.com/imwally/battstat/archive/master.zip).
      * `$ git clone https://github.com/imwally/battstat.git`
      * `$ curl -O https://raw.githubusercontent.com/imwally/battstat/master/battstat`

Then move it to your favorite binary path and make it executable.

```
$ mv battstat /usr/local/bin
$ chmod u+x /usr/local/bin/battstat
```

### Usage

```
usage: battstat [options] format

options:
    -h, --help                display help information
    --percent-when-charged    only display percent when charged

format:
    {i}    display icon
    {t}    display time remaining
    {p}    display percent

    Note: There must be a space between each format token.
```