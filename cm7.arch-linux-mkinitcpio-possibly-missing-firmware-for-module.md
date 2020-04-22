# CM7.  Arch Linux mkinitcpio: Possibly missing firmware for module

## Problem

In Arch Linux `mkinitcpio -p linux`

shows

```text
Possibly missing firmware for module: aic94xx
Possibly missing firmware for module: wd719x
```

## Solve

```text
git clone https://aur.archlinux.org/aic94xx-firmware.git
cd aic94xx-firmware
makepkg -sri
```

```text
git clone https://aur.archlinux.org/wd719x-firmware.git
cd wd719x-firmware
makepkg -sri
```

and then

```text
sudo mkinitcpio -p linux
```

 again.

## Reference

[https://wiki.archlinux.org/index.php/Mkinitcpio](https://wiki.archlinux.org/index.php/Mkinitcpio)
