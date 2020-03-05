# Raspberry Pi Setup

## Basic Setup

```
sudo raspi-config
```

### Change User Password

### Network Options

#### Hostname

`${greek}pi${model}`, e.g. alphapi4

#### Wi-fi

SSID is just the Wi-fi network name, not the BSSID

### Boot Options

#### Desktop / CLI > B2 Console Autologin

### Localisation Options

#### Change Locale

Use space to select/deselect entries

Select `en_US.UTF-8 UTF-8`

Hit enter to update and select `en_US.UTF-8 UTF-8` again

### Interfacing Options

#### SSH > Yes

### Advanced Options

#### Memory Split

Enter 256

## Update Keyboard

```
sudo nano /etc/default/keyboard
```

Update
```
XKBLAYOUT="us"
```

Save and reboot

## Update Raspbian

```
sudo apt -y update && sudo apt -y full-upgrade
sudo apt -y update && sudo apt -y dist-upgrade
sudo apt clean
sudo reboot
```

## Silent Boot

### Update /boot/cmdline.txt

```
sudo nano /boot/cmdline.txt
```
#### Change console level

Change 
```
console=tty1
```

to
```
console=tty3
```

Add
```
quiet splash loglevel=0 logo.nologo
```
to end of file

Add
```
vt.global_cursor_default=0
```
to end of file for no cursor

#### Remove MOTD

```
sudo rm /etc/motd
```

#### Add .hushlogin

```
touch ~/.hushlogin
```

#### Remove Autologin Message

[Typical instructions](https://raspberrypi.stackexchange.com/questions/59310/remove-boot-messages-all-text-in-jessie) won't work, so you'll need to update

```
sudo nano /etc/systemd/system/getty@tty1.service.d/autologin.conf
```

and change ExecStart to
```
ExecStart=-/sbin/agetty --skip-login --noclear --noissue --login-options "-f pi" %I $TERM
```

## Config Options & Overclocking

### Edit config.txt

```
sudo nano /boot/config.txt
```

#### Basic Config Options

Add
```
disable_splash=1
```

#### Pi 4 Options

Add
```
over_voltage=6
arm_freq=2000
gpu_freq=750
```

### Pi 0 Options