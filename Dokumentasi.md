# INSTALASI ARCH LINUX
## 1. Download ISO Arch Linux
### download iso arch menggungakan web arch cari indonesia, citrahost dan link archlinux-2026.05.01-x86_64.iso

## 2. Buat Bootable 
### colokkan flashdisk 

### rufus file iso yang sudah di download ke dalam flashdisk

## 3. Booting ke flashdisk installer
### colokkan falshdisk

### restart laptop

### tekan esc berkali-kali

## 4. Sambungkan ke internet
```
iwctl
```

```

device list
```
```
station wlan0 get-networks
```
```

station wlan0 connect nama wifi
```
```

ping 8.8.8.8
```

## 5. Format partisi
```

vfat format
```

## 6. Setup luks 
```

cryptsetup luksFormat /dev/nvme0n1p (partisi untuk root)
```

## 7. Mounting 
```

mount /dev/mapper/main /mnt
```
```

mkfs.ext4 /dev/mapper/main
```
```

mkdir -p /mnt/boot
```

## 8.Download aplikasi
```

pacstrap /mnt intel-ucode linux linux-headers linux-firmware iwd neovim sbctl git base-devel lvm2
```

## 9. Menyimpan mountingan
```

genfstab -U /mnt > /mnt/etc/fstab
```

## 10. Menyimpan network 
```

cp /etc/systemd/network/*  /mnt/etc/systemd/network
```

## 11. Masuk kedalam mode chroot
```

arch-chroot /mnt
```
## 12. Membuat Hostname
```

nvim /etc/hostname
```
### i (masuk dalam mode edit)

### masukkan hostname

### esc 
```

 :wq 
```
## 13. memberi hak akses kepada user
```

nvim etc/sudoers.d/hisyam
```

i (masuk dalam mode edit)

### tambahkan ini dalam sudoers
```

icem ALL=ALL(ALL:ALL) ALL
```
esc
```

:wq
```

## 14. Masuk Proses Locale
```

nvim /etc/locale.gen
```

<img width="1600" height="1200" alt="WhatsApp Image 2026-10-31 at 2 25 57 AM" src="https://github.com/user-attachments/assets/d9302cad-df64-4459-bad5-d284480cc542" />

hapus hastag pada /en_US

esc
```

:wq
```
```

locale-gen
```
```

locale > /etc/locale.conf
```
```

nvim /etc/locale.conf
```

<img width="1600" height="1200" alt="10" src="https://github.com/user-attachments/assets/bc2eb202-9406-4a90-90d1-31cd680f89d6" />


## 15. Masuk Kernel Parameter 
```

mkdir -p /etc/cmdline.d
```
```

touch /etc/cmdline.d/01-boot.conf
```
```

echo "rd.luks.name=$(blkid -s UUID -o /dev/nvme0n1p16)=main root=/dev/ mapper/main" > /etc/cmdline.d/01-boot.conf (nvme0n1p16 itu partisi boot)
```
```

mkdir -p kernel efi
```
```

mv intel-ucode.img kernel
```
```

mv vmlinuz-linux kernel/
```
```

rm initramfs-linux.img
```
```

cd efi mkdir linux
```
```

cd ..
```
```

ls
```
```

ls efi
```
```

ls kernel
```
## 16. Memindahkan File mkinitcpio
```

mv etc/mkinitcpio.conf /etc/mkinitcpio.d/default.conf
```
```

nvim /etc.mkinitcpio.d/default.conf
```

search HOOKS dan tambahkan lvm2 sd-encrypt setelah sd-vconsole

save
```

nvim /etc/mkinitcpio.d/linux.preset
```

<img width="1600" height="1200" alt="WhatsApp Image 2026-10-31 at 2 25 58 AM" src="https://github.com/user-attachments/assets/754a55bf-768b-418c-a568-dca75a65f6e5" />

```

bootctl --path=boot install
```
```

mkinitcpio -P
```
```

touch /etc/vconsole.conf
```
```

exit
```
```

bootctl --path=/mnt/boot install
```
```

umount -R /mnt
```
```

systemctl enable --now systemd-networkd
```
```

systemctl enable --now systemd-resolved
```
```

reboot
```

## 17. Masuk Kedalam Arch Linux
```

sudo su
```

## 18. Setup BIOS Mode
### posisi BIOS mati
```

reboot
```
### masuk ke dalam arch

```

sbctl create-keys
```
```

sbctl status
```
```

sbctl sign -s /boot/efi/systemd/systemd-bootx64.efi
```
```

sbctl sign -s /boot/efi/BOOT/BOOTX64.EFI
```
```

sbctl sign -s /boot/kernel/vmlinuz-linux
```
```

 reboot
```
### lalu ke BIOS 

### F7

### nyalakan secure boot

### reset key setup

### save
```

 reboot
```
## 19. Masuk Kedalam Arch
### Tampilan archlinux

<img width="1600" height="1200" alt="WhatsApp Image 2026-10-31 at 5 53 06 PM" src="https://github.com/user-attachments/assets/a30f79cc-6b2d-47e6-8934-1c77588247ff" />

### secure boot enable

<img width="1600" height="1200" alt="WhatsApp Image 2026-10-31 at 5 54 26 PM" src="https://github.com/user-attachments/assets/5cbcd14c-b62c-4f2a-88ab-fbd9b3c2b703" />






