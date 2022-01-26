#  cm9.Configure-Buletooth

## 1st Enuste your Bluetooth-Device has been disconnect from other device

* Chech again from other device whether your BT-device is disconnect
* Restart(Flop/Flip cap) your BT Device

## Install package and reboot

``` bash
sudo pacman -Syu blueman pulseaudio-bluetooth
```

## Enable Bluetooth

``` bash
sudo systemctl enable bluetooth
sudo systemctl start bluetooth
```

##  Reboot

``` bash
reboot
```

## Using buletooth manager gui

open `buletooth manager gui`

1. turn on bluetooth
2. search your device
3. connect your device
4. open YT to test

**If u are not using bluetooth device mow, please "disable" buletooth-manager**
