---
layout: post
title: How to add a bluetooth keyboard to the PocketCHIP
---

## Pontifications

* From [How does the PocketCHIP compare to the Raspberry Pi](https://opensource.com/article/17/2/pocketchip-or-pi?sc_cid=701600000011jJVAAY)

**QUOTE**

```bash
#!/bin/bash
 
ARG="${1}"
help() {
    echo "Connect a Bluetooth device to PocketCHIP"
echo "Usage: $ [MOD=1] ./blue.sh BLUETOOTH_ID"
    echo "Optional: put your device ID into ~/.bluechip"
    exit 0
    }
 
xkbfunc() {
    setxkbmap dvorak
    xmodmap $HOME/Xmodmap.logitech
    exit 0
}
 
if [ -e ~/.bluechip ]; then
    ARG=`cat $HOME/.bluechip`
elif [ X"$ARG" = "X" ]; then
    help
fi
 
echo "Using ID $ARG"
 
sudo systemctl start bluetooth || echo \
"Bluetooth already started or cannot be started."
 
sudo \
echo -e "power on\n connect $ARG \nquit" | bluetoothctl
xkbfunc 
```

**END QUOTE**

* Anybody know how to have a normal i.e. non-dvorak keyboard layout? (hopefully I can figure this out on my own)