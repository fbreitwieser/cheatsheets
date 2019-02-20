
[My Manjaro i3 setup - Tech Knowledge Base - jaytaala.com Confluence](https://confluence.jaytaala.com/display/TKB/My+Manjaro+i3+setup)

## Firewall
```
sudo pacman -S ufw
sudo systemctl enable ufw
sudo ufw enable
sudo ufw status
sudo gufw

sudo ufw default deny incoming
sudo ufw default allow outgoing

# Allow some apps -- see them w/ sudo ufw app list
sudo ufw allow 22/tcp # same: sudo ufw allow ssh
sudo ufw allow transmission

## for web server access
# sudo ufw allow www
```

- [How To Setup a Firewall with UFW on an Ubuntu and Debian Cloud Server | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server)
- [UFW - Community Help Wiki](https://help.ubuntu.com/community/UFW)

## Trackpad gestures

```
pacman -S libinput x86-input-libinput xorg-xinput xdotool


# Check devices
xinput

# Check available properties for trackpad
xinput list-props

xinput set-prop 'Synaptics TM3289-002' 'libinput Tapping Enabled' 1
xinput set-prop 'Synaptics TM3289-002' 'libinput Tapping Enabled Default' 1

xinput set-prop 'Synaptics TM3289-002' 'libinput Natural Scrolling Enabled' 1
xinput set-prop 'Synaptics TM3289-002' 'libinput Accel Speed' 1
```

### libinput-gestures
```
# .config/libinput-gestures.conf
gesture: pinch in 2 xdotool key --clearmodifiers 'ctrl+minus'
gesture: pinch out 2 xdotool key --clearmodifiers 'ctrl+plus'
gesture: swipe up 3 i3-msg "workspace next"
gesture: swipe down 3 i3-msg "workspace prev"
gesture: swipe left 3 xdotool key --clearmodifiers 'ctrl+Page_Up'
gesture: swipe right 3 xdotool key --clearmodifiers 'ctrl+Page_Down'
gesture: swipe up 4 rofi -theme Arc -font 'DejaVu Sans 14' -show window -modi 'window,drun,ssh' -show-icons
gesture: swipe left 4 i3-msg "workspace prev"
gesture: swipe right 4 i3-msg "workspace next"
```

### References
- [Libinput ArchWiki](https://wiki.archlinux.org/index.php/Libinput)
- [libinput-gestures](https://github.com/bulletmark/libinput-gestures)
- [Dell XPS 15 9550 Arch Linux Trackpad Multitouch Clicks and Gestures with libinput (and i3-wm)](https://blog.spirotot.com/2016/07/27/dell-xps-15-9550-arch-linux-trackpad-gestures/)
- [More libinput info, good details about Disable While Typing](https://wayland.freedesktop.org/libinput/doc/latest/palm_detection.html)
