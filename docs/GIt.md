---
title: GIt
createTime: 2025/07/08 17:03:15
permalink: /article/nek3qjr0/
---
# Git

## 登录



## 提交文件

1. **检查修改状态** 在 VSCode 的终端中执行以下命令，查看当前修改的状态：

   ```bash
   git status
   ```

2. **暂存修改的文件** 将修改的文件添加到暂存区：

   ```bash
   git add .
   ```

   ```bash
   git add <file1> <file2>
   ```

3. **提交修改** 提交暂存的更改：

   ```bash
   git commit -m "信息"
   ```

4. **再次推送** 推送提交后的更改到远程仓库：

   ```bash
   git push origin master
   ```