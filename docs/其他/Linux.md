---
title: Linux
createTime: 2025/07/08 17:03:15
permalink: /article/zqxr3n6w/
---
# Linux

## 安装软件

### 安装 V2ray

```bash
mkdir -p /etc/apt/keyrings
wget -qO - https://apt.v2raya.org/key/public-key.asc | sudo tee /etc/apt/keyrings/v2raya.asc
echo "deb [signed-by=/etc/apt/keyrings/v2raya.asc] https://apt.v2raya.org/ v2raya main" | sudo tee /etc/apt/sources.list.d/v2raya.list
sudo apt update
sudo apt install v2raya v2ray
sudo v2raya --reset-password #重置密码
sudo systemctl start v2raya.service
sudo systemctl enable v2raya.service
```

### 安装open-vm-tools

## 其他

### 设置GRUB默认引导

1. **确定Windows的启动项编号**

   - 重启电脑，观察GRUB菜单中Windows启动项的位置。GRUB菜单项的编号从0开始计数（例如：第1项为0，第2项为1，以此类推）

   - 若无法手动查看，可在终端执行以下命令查看当前配置：

     ```bash
  grep GRUB_DEFAULT /etc/default/grub
     ```
    
     如果当前默认项是“系统恢复”（如GRUB_DEFAULT=2），Windows可能位于下一顺位（即设置为3）

2. **编辑GRUB配置文件**

   ```bash
sudo nano /etc/default/grub  # 使用Nano编辑器，或替换为vim/gedit
   ```
   
   - 找到`GRUB_DEFAULT`参数，修改为Windows的启动项编号或名称（例如：若Windows是第3项，则设置为

     ```
GRUB_DEFAULT=2
     ```

   - 可选：设置

     ```
     GRUB_TIMEOUT=0
     ```

     以跳过菜单直接启动

3. **更新GRUB配置**

   ```bash
   sudo update-grub
   ```

   完成后重启生效
