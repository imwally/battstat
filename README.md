# battstat

`battstat` is a tiny shell script that displays formatted information about the status of your battery. It's best when used as apart of your __tmux__ status line. Really though, any place where a shell script can be executed should work just as well.

Information is displayed in the order the format tokens are written. For example, the command given in the screenshots below is `battstat --percent-when-charged {i} {t} {p}`. This will display an icon, the time remaining when charging and discharging, and finally the percentage but only when the battery is fully charged. Format tokens can be written in any order and as many times as you like, although I'm not sure why you would use more than one of each at a time.

![battery charging](https://github.com/imwally/battstat/raw/master/img/charging.png)
![battery discharging](https://github.com/imwally/battstat/raw/master/img/discharging.png)
![battery full charged](https://github.com/imwally/battstat/raw/master/img/charged.png)

## Examples

There are a few ways to customize the output of `battstat`. Charging and discharging icons can be replaced with single character or multi-character strings.

```
$ battstat -d "🍕" {t} {i}
 10:30  🍕

$ battstat {t} {i}
 11:47  🔋

$ battstat -c "AC:" -d "BAT:" {i} {p} {t}
 BAT:  82%  12:11

$ battstat {i} {p}    
 🔋  81%

$ battstat -d "Battery:" {i} {p}
 Battery:  81%
```

## Supported Operating Systems

* __macOS__: Details are collected via `pmset(1)`.
* __Linux__: Details are collected via `upower(1)`.

## Install

First grab the script. Here are a few options:

* Download and extract the [zip](https://github.com/imwally/battstat/archive/master.zip).
* `$ git clone https://github.com/imwally/battstat`
* `$ curl -O https://raw.githubusercontent.com/imwally/battstat/master/battstat`

Then move it to your favorite binary path and make it executable.

```
$ mv battstat /usr/local/bin
$ chmod u+x /usr/local/bin/battstat
```

## Usage

```
usage: battstat [options] format

options:
    -h, --help                display help information
    -c, --charging-icon       string to display when battery is charging
    -d, --discharging-icon    string to display when battery is discharging
    --percent-when-charged    only display percent when charged

format:
    {i}    display icon
    {t}    display time remaining
    {p}    display percent

    Note: There must be a space between each format token.
```