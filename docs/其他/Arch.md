---
title: Arch
createTime: 2025/07/08 17:03:15
permalink: /article/9sukl0lj/
---
# Arch Linux

> [Arch Linux](https://archlinux.org/)

## 准备

### 配置控制台字体

[控制台字体](https://wiki.archlinuxcn.org/wiki/Linux_console#字体)位于 `/usr/share/kbd/consolefonts/` 目录中，设置方式请参考 [setfont(8)](https://man.archlinux.org/man/setfont.8)。例如，要使用适合 [HiDPI 屏幕](https://wiki.archlinuxcn.org/wiki/HiDPI#Linux_console_(tty))的最大字体之一，请运行以下命令：

```bash
setfont ter-132n
```

### 联网

确保系统已经列出并启用了网络接口，用[ip-link(8)](https://man.archlinux.org/man/ip-link.8)检查：

```bash
ip link
```

用ping检查网络连接：

```bash
ping archlinux.org
```

**加镜像源**

```bash
vim /etc/pacman.d/mirrorlist
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
```

**更新必用的软件**

```bash
pacman -Syy
```

## 磁盘分区

**查看分区情况**

```bash
lsblk
```

**分区工具**

- fdisk：命令行
- cfdisk：交互式界面

**推荐分区**

*核心分区方案（必选）*

1. **EFI系统分区（/boot/efi）**
   - **大小**：建议 512MB-1GB（多系统共存需更大）
   - **格式**：FAT32
   - **作用**：存放UEFI引导文件，需单独分区且挂载到 `/boot/efi`（UEFI模式必须）
2. **根分区（/）**
   - **大小**：建议 30-100GB（基础系统约15GB，开发环境建议更大）
   - **格式**：ext4/Btrfs
   - **作用**：存放系统核心文件，若未单独划分 `/home` 或 `/var`，需预留额外空间
3. **交换分区（swap）**
   - **大小**：物理内存的1-2倍（若内存≥8GB且无休眠需求，可省略或使用交换文件）
   - **格式**：专用swap分区或交换文件
   - **作用**：内存扩展和休眠支持

*可选扩展分区*

1. **家目录分区（/home）**

   - **大小**：剩余空间的大部分（用户数据存储）
   - **格式**：ext4/XFS
   - **优势**：系统重装时保留用户配置和文件

2. **/var分区**

   - 大小：8-20GB（存放日志、软件包缓存等频繁写入数据）
   - **格式**：ext4（注重稳定性）
   - **作用**：避免日志膨胀占用根分区空间

3. **专用数据分区**

   - **场景**：多系统共享文件、多媒体库存储等
   - **格式**：NTFS/exFAT（跨系统兼容）

   > 如果想安装 Windows + Linux 双系统的话，则建议现安装 Windows 系统，安装时会自动生成一个 EFI 分区，在安装 Linux 时就不需要再分出 EFI 分区以及格式化
   >
   > 但在实践双系统过程中发现 Windows 自动生成的 EFI 分区较小，可以利用傲梅或其他工具将 EFI 分区扩大到 550M
   >
   > 同时推荐双系统方案分出一个共享分区，方便两个系统之间进行文件交换

```bash
# 使用 fdisk 对硬盘分区
fdisk /dev/sda
# fdisk 简要使用方法
# n-新建分区 t-改变分区类型 w-写入分区信息并退出 q-不保存修改然后退出
```

**分区完成后格式化和挂载**

> 如果是已经存在的 EFI 分区，务必不要对 EFI 分区进行格式化，尤其是安装双系统时更需要注意

```bash
# 根分区（示例）
mkfs.ext4 /dev/sda2  
mount /dev/sda2 /mnt  
# EFI分区（示例）
mkfs.fat -F32 /dev/sda1  
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot/efi  
# 交换分区（示例）
mkswap /dev/sda3  
swapon /dev/sda3
# /home 分区
mkdir /mnt/home
mount /dev/[home_part] /mnt/home
```

## 安装arch

来安装 base 软件包、Linux 内核和固件。这一步会花费较多时间，耐心等待即可，保证网络连接的稳定。

```bash
pacstrap /mnt base linux linux-firmware
```

