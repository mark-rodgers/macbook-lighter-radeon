# mackbook-lighter-radeon

MacBook keyboard and screen backlight adjust on the ambient light.
Internally, macbook-lighter-radeon reads the following files:

* /sys/devices/platform/applesmc.768/light
* /sys/class/backlight/radeon_bl0/brightness
* /sys/class/backlight/radeon_bl0/max_brightness
* /sys/class/leds/smc::kbd_backlight/brightness
* /sys/class/leds/smc::kbd_backlight/max_brightness

So you're expected to install corresponding Radeon/Intel drivers first.

## Setup

All commands including macbook-lighter-kbd, macbook-lighter-screen
will be available with sudo privilege once macbook-lighter-radeon finished install.

To use in non-root environment such as [xbindkeys](https://wiki.archlinux.org/index.php/Xbindkeys),
it's recommended to setup an "udev" rule to allow users in the
"video" group to set the backlights.
Place a file /etc/udev/rules.d/90-backlight.rules containing:

```
SUBSYSTEM=="backlight", ACTION=="add", \
  RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness", \
  RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"
```

And a file /etc/udev/rules.d/91-leds.rules containing:

```
SUBSYSTEM=="leds", ACTION=="add", \
  RUN+="/bin/chgrp video /sys/class/leds/%k/brightness", \
  RUN+="/bin/chmod g+w /sys/class/leds/%k/brightness"
```

## Usage

```bash
# Increase keyboard backlight by 50
macbook-lighter-kbd --inc 50
# Increase screen backlight by 50
macbook-lighter-screen --inc 50
# Set screen backlight to max
macbook-lighter-screen --max
# start auto adjust daemon
systemctl start macbook-lighter-radeon
# start auto adjust interactively, root previlege needed
macbook-lighter-ambient
```

## Tested MacBook Versions

* MacBook Pro Mid 2015 (11,5)
