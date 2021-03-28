# tuyactl

A python script to control tuya branded bulb devices from the shell.

## Prerequisites

* You need to know the ID, IP and Key of your Tuya Bulb
* Your Android based device has to be **rooted**. Alternatively you can install a Virtual Android Environment for that
* Root supporting file explorer (I used Total Commander for this specific example)

Your expected to know how to root your device. There are countless guides on the Internet for your specific model.

(Except if you use modern Phones from China, then you may be screwed)

Remove already existing Smart Life instances.

To get the device ID and IP you have to use the command `python -m tinytuya scan`.

To get the key you have to install this on your android based device: [APK](https://www.apkmirror.com/apk/volcano-technology-limited/smart-life-smart-living/smart-life-smart-living-3-7-2-release/smart-life-smart-living-3-7-2-android-apk-download/download/).

Connect your Tuya Devices with the app.

Now go to `/data/data/com.tuya.smartlife/shared_prefs` and search for a file with the name `preferences_global_key<randomnumbers>.xml`.
Inside this File you have to search for "localKey". You will have multiple entries when you inserted multiple devices. 
To know which key applies to which id you have to go back a little in the document until you see something that looks like your ID you got from the scan.
These numbers are the ID of your device and apply to the nearest key.

## Configuration

The following paths are used for configuration, in order:

1. `~/.config/tuyactl/devices.ini`,
2. `/etc/tuyactl/devices.ini`

Configuration example:

```ini
[LAMP1]

id=xxx
ip=192.168.xxx.xxx
key=xxx
```

Here, `LAMP1` is a user-defined name, used to identify the device on the command line, as follows:

```sh
tuyactl LAMP1 color         # to get the rgb color values
tuyactl LAMP1 color 255 0 0 # set the color to red
tuyactl LAMP1 brightness 0  # 0-1000
tuyactl LAMP1 temp 0        # 0-1000, soft-hard
tuyactl LAMP1 switch        # check whether the device is on or off
tuyactl LAMP1 switch on     # or off

# these two are experimental, so some features might not be available on your device
tuyactl LAMP1 mode white    # white, colour, scene, music
tuyactl LAMP1 scene 1       # 1=nature, 3=rave, 4=rainbow
```

## Dependencies
* Python >3.4
* [tinytuya](https://pypi.org/project/tinytuya/)
* [pycrypto](https://pypi.org/project/pycrypto/)