# Minegrub
A Grub Theme in the style of Minecraft!


![Minegrub Preview "Screenshot"](resources/preview_minegrub.png)

## Installation
> ### Note: grub vs grub2
> - Check if you have a `/boot/grub2` folder instead of a `/boot/grub` folder in which case you would just have to adjust the file paths mentioned here and in the `resources/minegrub-update.service` file
> - Also if you're not sure, run `grub-mkconfig -V` to check if you have grub version 2 (you should have)

- Clone this repository
```
git clone https://github.com/Lxtharia/minegrub-theme.git
```
- Copy the folder to your boot partition: (for info: `-ruv` = recursive, update, verbose)
```
sudo cp -ruv ./minegrub-theme/* /boot/grub/themes/minegrub-theme/
```
- Change/add this line in your `/etc/default/grub`:
```
GRUB_THEME=/boot/grub/themes/minegrub-theme/theme.txt
```
- Update your live grub config by running
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
- You're good to go!

## Random splash texts!
The `generate.py` script chooses a random line from `resources/splashes.txt` and generates and replaces the `logo.png` which holds the splash text
- Make sure Python 3 (or an equivalent) and the Pillow python package are installed
  - Install Pillow either with the python-pillow package from the AUR or with
```
sudo -H pip3 install pillow
```
  - It's important to use `sudo -H`, because it needs to be available for root
- To add new splash texts simply edit `./resources/splashes.txt` and add them to the end of the file (if you add it at the beginning or in the middle, some splashes may never get used because the image cashing uses the line of the file the splash is on)
- If you want to remove splashes you should reset the cache by deleting `/boot/grub/themes/minegrub-theme/cache`
### Update splash...
#### ...without systemd
- Just run `python /boot/grub/themes/minegrub-theme/generate.py` (from anywhere) after boot using whatever method works for you
#### ...with systemd
- Edit `./resources/minegrub-update.service` to use `/boot/grub2/` on line 5 if applicable
- Copy `./resources/minegrub-update.service` to `/etc/systemd/system`
- Enable the service: `systemctl enable minegrub-update.service`
- If it's not updating after rebooting (it won't update on the first reboot because it updates after you boot into your system), check systemctl status minegrub-update.service for any errors (for example if pillow isn't installed in the correct scope)

### Adjusting for a different amount of boot options:
- When you have more/less than 4 boot options, you might want to adjust the height of the bottom bar (that says "Options" and "Console")
- The formula is in the theme.txt, so you should be able to easily adjust it.

### Notes:
- the `GRUB_TIMEOUT_STYLE` in the defaults/grub file should be set to `menu`, so it immediately shows the menu (else you would need to press ESC and you dont want that)
- I'm no Linux expert, that's why I explain it so thoroughly, for other newbies :>
- i use arch btw
- i hope u like it, cause i sure do lmao

#### Thanks to
- https://github.com/toboot for giving me this wonderful idea!
- the internet for giving me wisdom lmao (Mainly http://wiki.rosalab.ru/en/index.php/Grub2_theme_tutorial)
- The contributors for contributing and giving me some motivation to improve some little things here and there


Font downloaded from https://www.fontspace.com/minecraft-font-f28180 and used for non commercial use.
