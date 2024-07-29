# 机械革命翼龙15PRO内置键盘修复备份

## 使用方法

### 添加 initrd 文件
```bash
find kernel | cpio -H newc --create > acpi_override
sudo cp acpi_override /boot
```
### 注册

#### grub2

```bash
echo "GRUB_EARLY_INITRD_LINUX_CUSTOM=\"acpi_override\"" >> /etc/default/grub
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

#### systemd-boot

修改 `/boot/loader/entries/` 目录下的文件

```bash
# Created by: archinstall
# Created on: 2024-07-28_08-06-24
title   Arch Linux (linux-zen)
linux   /vmlinuz-linux-zen
initrd  /acpi_override # 这一行
initrd  /initramfs-linux-zen.img
options root=PARTUUID=d1204e8c-13ab-4c8d-a6fd-45d731684912 zswap.enabled=0 rootflags=subvol=@ rw rootfstype=btrfs
```
