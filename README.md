# Raspberry Pi Setup

## Raspi Config
```
sudo raspi-config
```
- [ ] Change User Password
- Network Options
  - [ ] Hostname
`${greek}pi${model}`, e.g. alphapi4
  - [ ] Wi-fi
SSID is just the Wi-fi network name, not the BSSID
- Boot Options
  - [ ] Desktop / CLI > B2 Console Autologin
- Localisation Options
  - [ ] Change Locale
    - Use space to select/deselect entries
    - Select `en_US.UTF-8 UTF-8`
    - Hit enter to update and select `en_US.UTF-8 UTF-8` again
- Interfacing Options
  - [ ] SSH > Yes
- Advanced Options
  - [ ] Memory Split
Enter 256

## Update Keyboard
```
sudo nano /etc/default/keyboard
```
- [ ] Change XKBLAYOUT
```
XKBLAYOUT="us"
```
- [ ] Reboot to see effect

## Update Locale
- [ ] Update LANGUAGE
```
sudo update-locale LANGUAGE=en_US.UTF-8
```
- [ ] Update LC_ALL
```
sudo update-locale LC_ALL="en_US.UTF-8"
```
- [ ] Reboot to see effect in `locale`

## Update Raspbian

- [ ] Update Apt-Get
```
sudo apt-get update
```
- [ ] Update & Full Upgrade
```
sudo apt -y update && sudo apt -y full-upgrade
```
- [ ] Update & Dist Upgrade
```
sudo apt -y update && sudo apt -y dist-upgrade
```
- [ ] Clean Apt
```
sudo apt clean
```
- [ ] Reboot to see effect

## Silent Boot
- Update /boot/cmdline.txt
```
sudo nano /boot/cmdline.txt
```
- [ ] Update Console
```
console=tty1
```
to
```
console=tty3
```
- [ ] Remove logo, splash, update loglevel

Add
```
quiet splash loglevel=0 logo.nologo
```
to end of file
- [ ] Remove cursor (optional, consider doing this later)

Add
```
vt.global_cursor_default=0
```
to end of file
#### Login Messages
- [ ] Remove MOTD
```
sudo rm /etc/motd
```
- [ ] Add .hushlogin
```
touch ~/.hushlogin
```
- [ ] Remove Autologin Message

[Typical instructions](https://raspberrypi.stackexchange.com/questions/59310/remove-boot-messages-all-text-in-jessie) won't work, so we'll need to update getty autologin conf
```
sudo nano /etc/systemd/system/getty@tty1.service.d/autologin.conf
```
Change ExecStart to
```
ExecStart=-/sbin/agetty --skip-login --noclear --noissue --login-options "-f pi" %I $TERM
```
## Config Options & Overclocking
```
sudo nano /boot/config.txt
```
- [ ] Disable Splash
```
disable_splash=1
```
- [ ] Overclock Pi 4
```
over_voltage=6
arm_freq=2000
gpu_freq=750
```
- [ ] Overclock Pi 0
```
TBD
```
