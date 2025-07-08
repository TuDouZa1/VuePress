---
title: html
createTime: 2025/07/08 17:03:15
permalink: /article/qzlmanif/
---
# HTML

## 表格标签

table: 定义表格

tr: 定义表格行

th: 定义表头单元格

td: 定义数据单元格

### 示例

```html
<table border="1" cellspacing="0" cellpadding="0">
    <tr>
        <th>姓名</th>
        <th>年龄</th>
        <th>城市</th>
    </tr>
    <tr>
        <td>张三</td>
        <td>25</td>
        <td>北京</td>
    </tr>
</table>
```

cellspacing和cellpadding属性用于设置单元格边框和内容之间的距离。

效果：

| 姓名 | 年龄 | 城市 |
| ---- | ---- | ---- |
| 张三 | 25   | 北京 |

## 表单标签

form: 定义表单

input: 定义输入控件

select: 定义下拉列表

option: 定义下拉列表选项

textarea: 定义多行文本输入控件

button: 定义按钮

label: 定义标签

fieldset: 定义字段集

legend: 定义字段集标题

output: 定义输出控件

progress: 定义进度条

meter: 定义度量尺

### 示例

```html
<form action="submit.php" method="post">
    <label for="name">姓名:</label>
    <input type="text" id="name" name="name">
    <br>
    <label for="age">年龄:</label>
    <input type="number" id="age" name="age">
    <br>
    <label for="city">城市:</label>
    <select id="city" name="city">
        <option value="beijing">北京</option>
        <option value="shanghai">上海</option>
        <option value="guangzhou">广州</option>
    </select>
    <br>
    <label for="message">留言:</label>
    <textarea id="message" name="message"></textarea>
    <br>
    <button type="submit">提交</button>
</form>
```

效果：

姓名: 
年龄: 
城市:                    北京                   上海                   广州                 
留言: 
提交

## 列表标签

ul: 定义无序列表

ol: 定义有序列表

li: 定义列表项

dl: 定义描述列表

dt: 定义描述列表项目

dd: 定义描述列表描述

### 示例

```html
<ul>
    <li>苹果</li>
    <li>香蕉</li>
    <li>橘子</li>
</ul>
<ol>
    <li>第一项</li>
    <li>第二项</li>
    <li>第三项</li>
</ol>
<dl>
    <dt>HTML</dt>
    <dd>超文本标记语言</dd>
    <dt>CSS</dt>
    <dd>层叠样式表</dd>
</dl>
                    
```

效果：

- 苹果
- 香蕉
- 橘子

1. 第一项
2. 第二项
3. 第三项

- HTML

  超文本标记语言

- CSS

  层叠样式表

## 其他标签

div: 定义文档中的分区或区域

span: 定义文档中的行内文本

header: 定义文档的页眉

nav: 定义导航链接

## 移动端适配

