## 1 JavaScript 介绍

### 1.1 JavaScript 是什么

是一门编程语言。

### 1.2 JavaScript 书写位置

#### 1.2.1 内部

```HTML
<body>
  <!-- body的上面部分写html的内容，js要写在body的最下面 -->

  <!-- 内部方式 -->
  <script>
    alert('内部 JavaScript')
  </script>
</body>
```

#### 1.2.2 外部

```HTML
<body>
  <!-- 外部方式 -->
  <script src="./外部js.js">
    // script标签内写内容将会被忽略
  </script>
</body>
```

`外部js.js`

```JavaScript
alert('外部 JavaScript')
```

#### 1.2.3 行内

```HTML
<body>
  <!-- 行内方式 -->
  <!-- 目前作为了解，在后面Vue中会用到这种模式 -->
  <button onclick="alert('内联 JavaScript')">按钮</button>
</body>
```

### 1.3 JavaScript 注释

```JavaScript
// 单行注释

/* 
多行注释
*/
```

### 1.4 JavaScript 结束符

分号，可以加，也可以不加（习惯上），按照团队约定

### 1.5 输入输出语法

```HTML
<body>
  <script>
    // 弹窗输入
    prompt('请输入')
    // 弹窗输出
    alert('弹窗输出')
    // 文档输出内容
    document.write('<h1>我是标题</h1>')
    // 控制台打印输出
    console.log('控制台打印日志')
  </script>
</body>
```

按照 HTML 文档顺序执行，其中，`alert()` 和 `prompt()` 会跳过页面渲染先被执行。

### 1.6 字面量

- 字符串字面量： `'张三'`
- 数字字面量： `18`
- 数组字面量： `[]`
- 对象字面量： `{}`
- …

## 2 变量

### 2.1 变量的基本使用

### 2.2 变量的本质

### 2.3 变量的命名规范

## 3 常量

## 4 数据类型

## 5 类型转换

## 6 实战案例
