# battstat

`battstat` is a shell script that displays formatted information about the status of your battery. 

![battery discharging](/img/discharging.png)

## Examples

There are a few ways to customize the output of `battstat`. Charging and discharging icons can be replaced with single character or multi-character strings. The `-c` flag sets the charging string and the `-d` flag sets the discharging string.

```
~ % battstat -d "💀"
11:25 74% 💀

~ % battstat -d "😎" -f "{i} ({t})"
😎 (11:15)

~ % battstat -c "AC:" -d "BAT:" -f "{i} {p} {t}"
BAT: 74% 11:35

~ % battstat -d "Battery:" -f "{i} {p}"
Battery: 74%
```

## Formatting

`battstat` uses printf style formatting when using the `-f` flag. This means you can print replacement tokens however you want.

```
~ % battstat -f "{i}\t{t}\t({p})"               
🔋      11:55   (74%)

~ % battstat -f "{i}\nType whatever you want.\n{t}\n({p})" 
🔋
Type whatever you want.
12:05
(73%)
```

## macOS menu bar

![bitbar screenshot](/img/bitbar.png)

Using [bitbar](https://github.com/matryer/bitbar) you can add the output of `battstat` to the menu bar on macOS. There are many ways to customize the output so I suggest reading over the [writing plugins](https://github.com/matryer/bitbar#writing-plugins) section to understand what's possible.

The screenshot above is using the following shell script. Make sure the script is executable and placed in the bitbar plugins path.

```
#!/bin/sh

time=$(/usr/local/bin/battstat -f {t})

echo "($time) | size=13"
```

## Supported Operating Systems

* __macOS__: Details are collected via `pmset(1)`.
* __Linux__: Details are collected via `upower(1)`.
* __OpenBSD__: Details are collected via `apm(8)`.

## Notes

The script does not account for laptops with multiple batteries. Newer ThinkPad models include both a swappable and non-swappable battery which may cause problems when searching for the battery with `upower`. I currently don't have the means necessary to test against these models but pull requests are of course welcomed.

## Install

1. Grab the script. Here are a few options:

    * Download and extract the [zip](https://github.com/imwally/battstat/archive/master.zip).
    * `$ git clone https://github.com/imwally/battstat`
    * `$ curl -O https://raw.githubusercontent.com/imwally/battstat/master/battstat`

2. Move it to your favorite binary path and make it executable.

```
$ mv battstat /usr/local/bin
$ chmod u+x /usr/local/bin/battstat
```

## Usage

```
usage: battstat [options] format

options:
    -h, --help                display help information
    -c, --charging-icon       string to display in icon's place when battery is charging
    -d, --discharging-icon    string to display in icon's place when battery is discharging
    -f, --format              formatted output of battstat
    --percent-when-charged    only display percent when charged

format replacement tokens:
    {i}    display icon
    {t}    display time remaining
    {p}    display percent

example:
    battstat -f "Cool Battery: {t} ({p})"
```
