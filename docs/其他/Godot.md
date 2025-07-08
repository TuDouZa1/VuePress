---
title: Godot
createTime: 2025/07/08 17:03:15
permalink: /article/3ezou8s4/
---
# Godot

## 项目初始化

### 文件结构

- asset

  游戏资源

- source

  游戏场景，代码

### 项目设置

#### 窗口

- 拉伸模式
  - viewport：100%的纯像素显示推荐
  - canvas_items：非100%像素显示

#### 渲染

- 纹理
  - Nerarest：像素化显示
  - 

## 节点

- Node

  所有场景对象的基类

  - Viewport

    视口的抽象基类。对绘图以及与游戏世界的交互进行了封装。

  - CanvasItem

    2D 空间中所有对象的抽象基类。

    - Control
    - Node2D

  - Node3D

    最基本的 3D 游戏对象，所有 3D 相关节点的父类。

  - CanvasLayer

    用于 2D 场景中的对象的独立渲染的节点。

  -  ResourcePreloader

    用于预加载场景子资源的节点。

  - StatusIndicator

    应用程序状态指示器（即通知区域图标）。

    注意：状态指示器在 macOS 和 Windows 上实现。

## 类

一些继承关系

- Object

  所有类的基类。

  - Node

    所有场景对象的基类。

    - CanvasItem

      所有场景对象的基类。

      - Node2D

        ......

### 2D

- TileMapLayer

  - void set_cell()：创建指定的图块

- AStarGrid2D：A* 的一种实现，用于寻找疏松 2D 网格中两点之间的最短路径。

  > 示例初始化
  >
  > ```javascript
  > var _astar := AStarGrid2D.new()
  > 
  > // 设定寻路方式
  > _astar.diagonal_mode = AStarGrid2D.DIAGONAL_MODE_NEVER
  > _astar.default_compute_heuristic = AStarGrid2D.HEURISTIC_MANHATTAN
  > _astar.default_estimate_heuristic = AStarGrid2D.HEURISTIC_MANHATTAN
  > ```