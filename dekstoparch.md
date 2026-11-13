## DEKSTOP ARCH

```

sudo pacman -S xorg-server xorg-xinit
```
### Pilihan Dekstop

#### Plasma
```

sudo pacman -S plasma sddm
```
```

sudo systemctl enable sddm
```

#### Gnome
```

sudo pacman -S gnome gdm
```
```

sudo systemctl enable gdm
```

#### Xfce
```

sudo pacman -S xfce4 xfce4-goodies lightdm lightdm-gtk-greeter
```
```

sudo systemctl enable lightdm
```

```

reboot
```



