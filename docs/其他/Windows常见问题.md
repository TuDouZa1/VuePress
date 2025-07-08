---
title: Windows常见问题
createTime: 2025/07/08 17:03:15
permalink: /article/qhkkbk6h/
---
# Windows 常见问题

> 用来记录一些平时使用电脑碰到的不常见问题和解决方法

## 磁盘相关

### 磁盘分区类型变成了 RAM

管理员命令行输入

```cmd
diskpart
list disk                   # 找到对应的硬盘编号，如：磁盘 2
select disk 2
clean                       # 清除所有的分区信息
create partition primary    # 创建分区
format fs=ntfs quick 	    #格式化为ntfs
```

### 清理C盘垃圾

- win + R输入`%temp`和`temp`全部删除即可，不能删的就跳过
- 

## 其他

### 手动设置某个exe开机自启

1. 启动**任务计划程序**
2. 右侧**点创建任务**
3. 名字，描述随意
4. **触发器**设置登录时
5. **操作**为启动某个应用
6. **条件**去掉插电才启动

### 右键管理

**管理右键选项**
[Release 3.3.3.1 · BluePointLilac/ContextMenuManager](https://github.com/BluePointLilac/ContextMenuManager/releases/tag/3.3.3.1)

**锁定右键选项不会被修改**
[HaujetZhao/Protect-Windows-Context-Menu](https://github.com/HaujetZhao/Protect-Windows-Context-Menu?tab=readme-ov-file)

### 打开方式软件管理

win + R，输入`Regedit`
打开`HKEY_CLASSES_ROOT\Applications` 
打开`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts`
