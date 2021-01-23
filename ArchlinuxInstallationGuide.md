# Archlinux Installation Guide

## 1 查看磁盘信息

```
fdisk -l
```

## 2 分盘挂载

```
cfdisk
new -> type -> write
mkfs.ext4 /dev/root_partition			（根分区）
mount /dev/root_partition /mnt
mkswap /dev/swap_partition				（交换空间分区）
swapon /dev/swap_partition
```

## 3联网

```
iwctl
station wlan0 get-networks
station wlan0 connect Morphling
```

## 4安装系统

```
vim /etc/pacman.d/mirrorlist		## 移动China源到前面
pacstrap /mnt base base-devel linux linux-firmware intel-ucode vim networkmanager fish dhcpcd
```

## 5其他系统配置

```
genfstab -U /mnt >> /mnt/etc/fstab
```

```
arch-chroot /mnt
```

```
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
```

```
hwclock --systohc
```

```
vim /etc/locale.gen
locale-gen
```

```
vim /etc/locale.conf
LANG=en_US.UTF-8
```

```
vim /etc/hosts
127.0.0.1	localhost
::1			localhost
127.0.1.1	Archlinux.localdomain	Archlinux
```

```
passwd
useradd  -m -g wheel **
passwd ** yourpasssword
visudo
%whell ALL=(ALL)ALL
```

```
systemstl enable NetworkManager
systemstl enable dhcpcd
```



## 6安装启动管理器

```
pacman -S grub efibootmgr os-prober  
grub-install --target=x86_64-efi --efi-directory=esp --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```

```
vim /boot/grub/grub.cfg
default **					#修改默认启动顺序
timeout **					#修改等待时间
```

## 7安装图形界面

```
pacman -S gdm gnome gnome-extra 
pacman -S xorg nvidia nvidia-utils 
systemstl enable gdm
```



```
exit
umount -R /mnt

reboot
```

# 启动后联网

```
nmcli device wifi list
nmcli device wifi connect SSID password password

```

