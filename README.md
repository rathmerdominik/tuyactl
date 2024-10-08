> [!WARNING]
> I no longer use this project as i just use the Smart Home app.

# tuyactl

A python script to control tuya branded bulb devices from the shell.

## Prerequisites

* You need to know the ID, IP and Key of your Tuya bulb
* Your Android based device has to be **rooted**. Alternatively you can install a Virtual Android Environment for that.
* Root supporting file explorer (I used Total Commander for this specific example)

You are expected to know how to root your device. There are countless guides on the Internet for your specific model.

(Except if you use modern phones from China, then you may be screwed)

Remove already existing Smart Life instances.

To get the device ID and IP you have to use the command `python -m tinytuya scan`.

To get the key you have to install this on your Android based device: [APK](https://www.apkmirror.com/apk/volcano-technology-limited/smart-life-smart-living/smart-life-smart-living-3-7-2-release/smart-life-smart-living-3-7-2-android-apk-download/download/).

Connect your Tuya devices with the app.

Now go to `/data/data/com.tuya.smartlife/shared_prefs` and search for a file with the name `preferences_global_key<randomnumbers>.xml`.
Inside this File you have to search for `localKey`. You will have multiple entries when you inserted multiple devices.
To know which key applies to which id you have to go back a little in the document until you see something that looks like your ID you got from the scan.
These numbers are the ID of your device and apply to the nearest key.

## Configuration

The following paths are used for configuration, in order:

1. `$XDG_CONFIG_HOME/tuyactl/devices.ini`,
2. `~/.config/tuyactl/devices.ini`,
3. `/etc/tuyactl/devices.ini`

Configuration example:

```ini
[LAMP1]

id=xxx
ip=192.168.xxx.xxx
key=xxx
```

Here, `LAMP1` is a user-defined name, used to identify the device on the command line, as follows:
INFO

Some commands may be subject to change

```sh
# values after these subcommands are optional, leave them out to query the information instead
tuyactl LAMP1 color ff0000      # set the color to red
tuyactl LAMP1 brightness 500    # set the brightness to medium (0-1000)
tuyactl LAMP1 temp 0            # set the light temperature to warm (0-1000)
tuyactl LAMP1 switch on         # turn the lamp on (on|off)

# the following values can not be queried:
tuyactl LAMP1 white 1000 1000   # max brightness and coldest temperature (0-1000, 0-1000)
tuyactl LAMP1 whiteper 50       # 0-100
tuyactl LAMP1 colorper 50       # 0-100
# one type of transition is also supported:
tuyactl slow -i 1 00ff00 ff0000 # fade from green to red, with one second of delay
# an abrupt/fast transition is not (yet?) possible
tuyactl breathing -i 1 1 00ff00 ff0000 #fade from green to red, with one second of delay and one second of off time
# these two are experimental, so some features might not be available on your device
tuyactl LAMP1 mode white        # white, colour, scene, music
tuyactl LAMP1 scene 1           # 1=nature, 3=rave, 4=rainbow
```

## Dependencies
* Python >3.4
* [tinytuya](https://pypi.org/project/tinytuya/)
* [pycrypto](https://pypi.org/project/pycrypto/)
* [docopt](https://pypi.org/project/docopt/)
