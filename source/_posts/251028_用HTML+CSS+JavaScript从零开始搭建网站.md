---
title: 用 HTML + CSS +JavaScript 从零开始搭建网站
categories:
  - Software
tags:
  - HTML
  - CSS
  - JavaScript
---
## 简单上手
### 前端三剑客
HTML、CSS、JavaScript 被称为前端三剑客，即网页的前端开发中构建网页的三种核心技术，纯前端开发足以满足以内容展示为主的网页搭建。
- HTML：超文本标记语言，将排版信息代码化，负责页面的结构和内容
- CSS：层叠样式表，定义各种样式名称和效果，在HTML文件中直接引用这些样式，负责页面的样式和布局
- JavaScript：脚本语言，实现网页的动态功能，如滚动、点击、输入等操作，负责页面的交互逻辑和动态行为

### 文件层级结构
一个完整的网页前端`.html`文件，按顺序为 CSS 样式表、HTML 信息、JavaScript 代码。这里写一个简单的页面，可以直接复制下来，新建一个 txt 文档，将内容粘贴进去保存后，将文档后缀改为html，用浏览器打开：
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HOME</title>
    <style>
        /* CSS 样式表 */
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background-color: #000000;
        }
        
        h1 {
            font-size: 4rem;
            color: #ffffff;
            cursor: pointer;
            padding: 10px;
            border-radius: 5px;
        }
        
        h1:hover {
            background-color: #2f2f2f;
        }
    </style>
</head>
<body>
    <!-- HTML 信息 -->
    <h1 id="home-title">HOME</h1>

    <script>
        // JavaScript 代码

        // 获取标题元素
        const homeTitle = document.getElementById('home-title');
        // 添加点击事件监听器
        homeTitle.addEventListener('click', function() {
            // 刷新页面
            location.reload();
        });
    </script>
</body>
</html>
```
这个网站的效果是，正中一个大大的HOME，黑底白字，鼠标悬停显示灰色背景，点击刷新页面。可以看到，三者的注释方式也不同。这是将CSS、JavaScript一起写在HTML中的样子，由于这里还是HTML的地盘，CSS用`<style></style>`包裹起来，JavaScript用`<script></script>`包裹起来。

我们命名这个文件为`home.html`。当然我们可以将CSS部分分离出来创建`home.css`文件，将JavaScript部分分离出来创建`home.js`文件：
```css
body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    margin: 0;
    background-color: #000000;
}

h1 {
    font-size: 4rem;
    color: #ffffff;
    cursor: pointer;
    padding: 10px;
    border-radius: 5px;
}

h1:hover {
    background-color: #2f2f2f;
}
```

```javascript
// 获取标题元素
const homeTitle = document.getElementById('home-title');

// 添加点击事件监听器
homeTitle.addEventListener('click', function() {
    // 刷新页面
    location.reload();
});
```

然后在HTML中原CSS和JavaScript处引用这些文件：
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HOME</title>
    <link rel="stylesheet" href="home.css">
</head>
<body>
    <!-- HTML 信息 -->
    <h1 id="home-title">HOME</h1>

    <script src="home.js"></script>>
</body>
</HTML>
```

这样将三个文件放在一起一个目录下时，便能实现一样的效果。分开管理css和js文件能够提高网站的可维护性，谁也不想在动辄几百上千行的html里找一个样式名称。

随着页面增多，我们可以按需创建`global.css`和`global.js`放一些通用的样式，不同页面的特定样式或交互逻辑，则放在如`home.css`、`home.js`、`page2.css`、`page2.js`等专有文件中。建立一个css文件夹放`.css`文件，建立一个js文件夹放`.js`文件，对应的之前引用文件的地址则改为：

```html
    <link rel="stylesheet" href="css/home.css">
    <script src="js/home.js"></script>>
```

一个健康的文件层级应该是：
- `css/` - 存放CSS样式文件
- `js/` - 存放JavaScript脚本文件
- `images/` - 存放图片资源
- `fonts/` - 存放自定义字体文件
- `pages/` - 存放除首页外的其他HTML页面
- `assets/` - 存放其他静态资源，如文档、下载文件等
- `index.html` - 主入口HTML页面
- `README.md` - 项目说明文档

一个html模板：
```html
<!DOCTYPE html> <!-- 文档类型声明，告诉浏览器使用HTML5标准解析此文档 -->
<html lang="zh-CN"> <!-- html根元素，lang属性定义文档的主要语言 -->
<head>  <!-- 文档头部区域，包含元数据和链接信息 -->
    <meta charset="UTF-8">  <!-- 字符编码声明，确保中文字符正确显示 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  <!-- 视口设置，使网页在移动设备上正确缩放 -->
    <title>网页标题</title> <!-- 网页标题，显示在浏览器标签页上 -->
    <link rel="stylesheet" href="styles.css">   <!-- 引入CSS样式表 -->
</head>
<body>  <!-- 文档主体区域，包含所有可见内容 -->

    <header>    <!-- 页面头部区域，通常包含logo、导航等 -->
        <h1>网站标题/Logo</h1> <!-- 主要标题 -->
        <nav>   <!-- 导航区域 -->
            <ul>
                <li><a href="#">首页</a></li> <!-- 导航链接 -->
                <li><a href="#">关于我们</a></li>
                <li><a href="#">联系我们</a></li>
            </ul>
        </nav>
    </header>

    <main>  <!-- 页面主要内容区域 -->
        <section>   <!-- 内容区块1 -->
            <h2>区块标题</h2>   <!-- 二级标题 -->
            <p>这里是内容段落...</p>    <!-- 段落文本 -->
        </section>
        <article>   <!-- 独立的文章内容 -->
            <h2>文章标题</h2>
            <p>文章内容...</p>
        </article>
    </main>

    <aside> <!-- 侧边栏内容 -->
        <h3>侧边栏标题</h3>
        <p>侧边栏内容...</p>
    </aside>

    <footer>    <!-- 页面底部区域 -->
        <p>&copy; 2023 公司名称 版权所有</p>    <!-- 版权信息 -->
    </footer>

    <script src="script.js"></script>   <!-- 引入JavaScript文件 -->
</body>
</html>
```

这个文档模板中出现的如`nav`、`section`等，都是容器的名称，即我在这个地方放置一个名为`nav`的容器，将导航链接这些元素放在这个容器里。这个容器的样式，以及容器内元素的样式则都在css文件中定义。

---

## HTML：构建网页的骨架

HTML使用一系列**标签**来定义内容和结构。以下是一些常用标签：

### 常用HTML标签

- **标题**: `<h1>` 到 `<h6>`，重要性依次递减
- **段落**: `<p>`
- **链接**: `<a href="url">链接文本</a>`
- **图片**: `<img src="image.jpg" alt="图片描述">`
- **列表**:
  - 无序列表: `<ul>` 和 `<li>`
  - 有序列表: `<ol>` 和 `<li>`
- **分区**: `<div>` (块级) 和 `<span>` (行内)
- **表单**:
  ```html
  <form>
    <input type="text" placeholder="请输入文本">
    <input type="email" placeholder="请输入邮箱">
    <input type="password" placeholder="请输入密码">
    <button type="submit">提交</button>
  </form>
  ```

### HTML5 语义化标签

HTML5引入了语义化标签，让结构更清晰，也利于SEO：
- `<header>`: 页眉
- `<nav>`: 导航栏
- `<main>`: 主要内容
- `<article>`: 独立文章
- `<section>`: 文档中的节
- `<aside>`: 侧边栏
- `<footer>`: 页脚

尽量使用语义化标签，而不是全部用`<div>`。

---

## CSS：为网页添加样式

CSS控制网页的表现形式，包括布局、颜色、字体等。

### CSS的三种引入方式

1. **内联样式**：直接在HTML标签的`style`属性中编写
   ```html
   <h1 style="color: blue; font-size: 24px;">标题</h1>
   ```
2. **内部样式表**：在HTML的`<style>`标签中编写
3. **外部样式表**：在单独的`.css`文件中编写，通过`<link>`引入（**推荐**）

### CSS选择器

选择器用于指定要样式化的HTML元素：

- **元素选择器**: `p { color: red; }`
- **类选择器**: `.className { font-size: 16px; }` (在HTML中使用`class="className"`)
- **ID选择器**: `#idName { background: yellow; }` (在HTML中使用`id="idName"`)
- **后代选择器**: `div p { margin: 10px; }` (选择`<div>`内的所有`<p>`)

### 盒模型

CSS盒模型是布局的基础，每个元素都被视为一个矩形盒子，包括：
- **内容**: `width`, `height`
- **内边距**: `padding`
- **边框**: `border`
- **外边距**: `margin`

```css
.box {
  width: 300px;
  padding: 20px;
  border: 5px solid black;
  margin: 10px;
}
```

### 常用CSS属性

- **文本**: `color`, `font-size`, `font-family`, `text-align`, `line-height`
- **背景**: `background-color`, `background-image`
- **布局**: `display` (block, inline, inline-block, flex, grid), `position` (static, relative, absolute, fixed)

### Flexbox 布局

Flexbox是一种一维布局模型，非常适合居中和对齐元素：

```css
.container {
  display: flex;
  justify-content: center; /* 水平居中 */
  align-items: center; /* 垂直居中 */
  flex-direction: row; /* 排列方向：行 */
}
```

---

## JavaScript：实现网页交互

JavaScript是一种动态编程语言，可以为网页添加复杂的交互行为。

### 基本语法

- **变量声明**:
  ```javascript
  let name = "张三"; // 可重新赋值
  const age = 25; // 常量，不可重新赋值
  ```
- **数据类型**: String, Number, Boolean, Array, Object
- **函数**:
  ```javascript
  function greet(name) {
    return "Hello, " + name;
  }
  // 或使用箭头函数
  const greet = (name) => "Hello, " + name;
  ```
- **条件语句**:
  ```javascript
  if (age >= 18) {
    console.log("成年人");
  } else {
    console.log("未成年人");
  }
  ```
- **循环**:
  ```javascript
  for (let i = 0; i < 5; i++) {
    console.log(i);
  }
  ```

### DOM 操作

DOM（文档对象模型）是HTML文档的编程接口，JavaScript可以通过DOM动态修改页面：

- **选择元素**:
  ```javascript
  const title = document.getElementById('home-title');
  const paragraphs = document.getElementsByTagName('p');
  const boxes = document.getElementsByClassName('box');
  // 现代方法：
  const element = document.querySelector('#id'); // 选择第一个匹配元素
  const elements = document.querySelectorAll('.class'); // 选择所有匹配元素
  ```
- **修改内容**:
  ```javascript
  title.textContent = "新的标题";
  title.innerHTML = "<em>强调的标题</em>";
  ```
- **修改样式**:
  ```javascript
  title.style.color = "red";
  title.style.fontSize = "2rem";
  ```
- **添加/删除元素**:
  ```javascript
  const newParagraph = document.createElement('p');
  newParagraph.textContent = "我是新段落！";
  document.body.appendChild(newParagraph);
  
  // 删除元素
  const oldElement = document.getElementById('old');
  oldElement.remove();
  ```

### 事件处理

JavaScript可以响应用户的各种操作：

```javascript
const button = document.getElementById('myButton');

// 添加点击事件
button.addEventListener('click', function() {
  alert('按钮被点击了！');
});

// 表单提交事件
const form = document.getElementById('myForm');
form.addEventListener('submit', function(event) {
  event.preventDefault(); // 阻止表单默认提交行为
  // 处理表单数据
  const inputValue = document.getElementById('myInput').value;
  console.log('用户输入:', inputValue);
});
```

---

## 实战：创建一个交互式待办事项列表

咱们创建一个简单的待办事项应用：

**HTML (todo.html)**:
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>待办事项</title>
    <link rel="stylesheet" href="css/todo.css">
</head>
<body>
    <div class="container">
        <h1>我的待办事项</h1>
        <form id="todo-form">
            <input type="text" id="todo-input" placeholder="添加新任务..." required>
            <button type="submit">添加</button>
        </form>
        <ul id="todo-list"></ul>
    </div>
    <script src="js/todo.js"></script>
</body>
</html>
```

**CSS (css/todo.css)**:
```css
body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 500px;
    margin: 0 auto;
    background: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

h1 {
    text-align: center;
    color: #333;
}

#todo-form {
    display: flex;
    margin-bottom: 20px;
}

#todo-input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 3px;
}

button {
    padding: 10px 15px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    margin-left: 10px;
}

button:hover {
    background: #0056b3;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    padding: 10px;
    border-bottom: 1px solid #ddd;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

li:last-child {
    border-bottom: none;
}

.completed {
    text-decoration: line-through;
    color: #888;
}

.delete-btn {
    background: #dc3545;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 3px;
    cursor: pointer;
}
```

**JavaScript (js/todo.js)**:
```javascript
// 获取DOM元素
const todoForm = document.getElementById('todo-form');
const todoInput = document.getElementById('todo-input');
const todoList = document.getElementById('todo-list');

// 加载保存的待办事项
document.addEventListener('DOMContentLoaded', loadTodos);

// 添加待办事项
todoForm.addEventListener('submit', function(event) {
    event.preventDefault();
    
    const todoText = todoInput.value.trim();
    
    if (todoText !== '') {
        addTodoItem(todoText);
        saveTodoToLocalStorage(todoText);
        todoInput.value = '';
    }
});

// 添加待办事项到列表
function addTodoItem(text, completed = false) {
    const li = document.createElement('li');
    
    const span = document.createElement('span');
    span.textContent = text;
    if (completed) {
        span.classList.add('completed');
    }
    
    // 点击待办事项标记完成/未完成
    span.addEventListener('click', function() {
        this.classList.toggle('completed');
        updateLocalStorage();
    });
    
    // 删除按钮
    const deleteBtn = document.createElement('button');
    deleteBtn.textContent = '删除';
    deleteBtn.classList.add('delete-btn');
    deleteBtn.addEventListener('click', function() {
        li.remove();
        updateLocalStorage();
    });
    
    li.appendChild(span);
    li.appendChild(deleteBtn);
    todoList.appendChild(li);
}

// 保存到本地存储
function saveTodoToLocalStorage(text) {
    let todos = getTodosFromLocalStorage();
    todos.push({ text, completed: false });
    localStorage.setItem('todos', JSON.stringify(todos));
}

// 从本地存储获取待办事项
function getTodosFromLocalStorage() {
    let todos = localStorage.getItem('todos');
    return todos ? JSON.parse(todos) : [];
}

// 加载待办事项
function loadTodos() {
    let todos = getTodosFromLocalStorage();
    todos.forEach(todo => {
        addTodoItem(todo.text, todo.completed);
    });
}

// 更新本地存储
function updateLocalStorage() {
    let todos = [];
    document.querySelectorAll('#todo-list li').forEach(li => {
        const text = li.querySelector('span').textContent;
        const completed = li.querySelector('span').classList.contains('completed');
        todos.push({ text, completed });
    });
    localStorage.setItem('todos', JSON.stringify(todos));
}
```

---

## 响应式设计

响应式设计确保网站在不同设备上都能良好显示。实现响应式的关键技术：

### 1. 视口设置
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### 2. 媒体查询
```css
/* 默认样式（移动设备优先） */
.container {
  width: 100%;
  padding: 10px;
}

/* 平板电脑 */
@media (min-width: 768px) {
  .container {
    width: 750px;
    margin: 0 auto;
  }
}

/* 桌面电脑 */
@media (min-width: 1024px) {
  .container {
    width: 980px;
  }
}
```

### 3. 弹性布局
使用Flexbox或Grid布局，它们天生具有响应式特性。

---

## 调试技巧

1. **浏览器开发者工具**：按F12打开，可以检查元素、查看CSS、调试JavaScript
2. **Console**：使用`console.log()`输出变量值，帮助调试
3. **断点调试**：在开发者工具的Sources面板中设置断点，逐步执行代码

---

## 部署网站

完成网站开发后，你可以通过以下方式让其他人访问：

1. **GitHub Pages**（免费）：
   - 在GitHub上创建仓库
   - 上传你的网站文件
   - 在仓库设置中启用GitHub Pages

2. **Netlify/Vercel**（免费）：
   - 拖拽你的网站文件夹到上传区域
   - 或连接GitHub仓库自动部署

3. **传统虚拟主机**：
   - 购买域名和主机空间
   - 通过FTP上传文件

---

## 进一步学习

掌握了HTML、CSS和JavaScript的基础后，可以继续学习：

- **CSS预处理器**：Sass/Less
- **CSS框架**：Bootstrap、Tailwind CSS
- **JavaScript框架**：Vue.js、React、Angular
- **版本控制**：Git
- **构建工具**：Webpack、Vite
