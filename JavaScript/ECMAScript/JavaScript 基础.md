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

```JavaScript
// 声明变量
let age
// 变量赋值
age = 18
// 声明多个变量（不推荐）
let name = '张三', sex = 1
```

### 2.2 变量的命名规范

1. 规则
	1. 不能用关键字，如：let、var、if、for 等
	2. 只能用下划线、字母、数字、$ 组成，且数字不能开头
	3. 字母严格区分大小写，如 Age 和 age 是两个不同的变量
2. 规范
	1. 起名要有意义
	2. 小驼峰命名法：userName

### 2.3 变量拓展 - 数组

```JavaScript
let names = ['张三', '李四']
console.log(names[0])
console.log(names.length)
```

## 3 常量

```JavaScript
const PI = 3.14 // 声明时必须赋值
PI = 3.15 // 报错，不可再次赋值
```

## 4 数据类型

1. 基本数据类型
	1. number 数字型
		1. NaN 代表一个计算错误，是一个不正确的或一个未定义的数学操作所得结果 `console.log('张三' - 2)`
		2. NaN 是粘性的，任何对 NaN 的操作都会返回 NaN `console.log(NaN + 2)`
	2. string 字符串型
		1. 通过单引号（''）、双引号（""）、反引号（\`\`）包裹
		2. 单引号双引号没有本质区别，推荐使用单引号
		3. 模板字符串：外面用反引号，里面用 `${变量名}`：console.log(\` 我今年 ${age}岁了\`)`
	3. boolean 布尔型
		1. ''、0、undefined、null、NaN 转换为布尔值后都是 false，其余则是 true，比如 Boolean(NaN) 为 false
	4. undefined 未定义型
		1. 声明一个变量但未赋值
	5. null 空类型
		1. 赋值了但是内容为空
		2. 将来有个变量里存放的是一个对象，但是对象还没创建好，可以先给个 null
2. 引用数据类型
	1. object 对象

## 5 类型转换

```JavaScript
// 查看变量类型
typeof 变量名
```

### 5.1 隐式转换

- `+` 两边只要有一个是字符串，都会把另一个转换为字符串
- `+` 作为正号，转换成数字型：+'12' 为数字 12
- 除了 `+` 以外的算数运算符都会把数据转换成数字类型

### 5.2 显式转换

```JavaScript
let str = '123'
console.log(Number(str))

parseInt('12.89px') // 只保留整数，不四舍五入，12
parseFloat('12.89px') // 可以保留小数，12.89
parseInt('abc12.89px') // NaN
```

## 6 运算符

### 6.1 赋值运算符

=、+=、-=、\*=、/=、%=

### 6.2 一元运算符

++、--

> ++i 和 i++ 与 Java 相同。

### 6.3 比较运算符

```
> 、<、>=、<=
== 左右两边值是否相等：2 == '2' //true
=== 左右两边值和类型都相等（推荐）：2 === '2' //false
!==
```

### 6.4 逻辑运算符

&&、||、!

### 6.5 运算符优先级

| 优先级 | 运算符   | 顺序             |     |     |
| --- | ----- | -------------- | --- | --- |
| 1   | 小括号   | ()             |     |     |
| 2   | 一元运算符 | ++ -- !        |     |     |
| 3   | 算数运算符 | 先 * / % 后 + -  |     |     |
| 4   | 关系运算符 | > >= < <=      |     |     |
| 5   | 相等运算符 | == != \=== !== |     |     |
| 6   | 逻辑运算符 | 先&& 后 \|\|     |     |     |
| 7   | 赋值运算符 | =              |     |     |
| 8   | 逗号运算符 | ,              |     |     |

## 7 语句

### 7.1 分支语句

#### 7.1.1 if 分支语句

```JavaScript
if () {

} else if () {

} else {

}
```

#### 7.1.2 三元运算符

```
条件 ? 满足条件执行的代码 : 不满足条件执行的代码
```

#### 7.1.3 switch 语句

```JavaScript
switch (1) {
  case 1:
    console.log('1')
    break
  case 2:
    console.log('2')
    break
  default:
    console.log('其他')
}
```

### 7.2 循环语句

```JavaScript
break 退出循环
continue 结束本次循环，继续下次循环
```

#### 7.2.1 while 循环

```JavaScript
while (循环条件) {

}
```

#### 7.2.2 for 循环

```JavaScript
for (let i = 0; i < n; i++) {
  console.log(i)
}
```

> 后面有 [[#10.2 遍历对象|增强for循环]]

## 8 数组

### 8.1 数组基本使用

#### 8.1.1 声明数组

```JavaScript
let arr1 = [1, 2, 3] // 推荐
let arr2 = new Array(1, 2, 3)
```

#### 8.1.2 操作数组

##### 8.1.2.1 查

```JavaScript
arr[1]
```

##### 8.1.2.2 改

```JavaScript
arr[1] = 2
```

##### 8.1.2.3 增

```JavaScript
arr.push(4) // 往末尾添加一个或多个数据，返回数组长度
arr.push(4, 5, 6, 7)
arr.unshift(4) // 往开头添加一个或多个数据，返回数组长度
```

##### 8.1.2.4 删

```JavaScript
arr.pop() // 删除最后一个元素，并返回该元素的值
arr.shift() // 删除第一个元素，并返回该元素的值
arr.splice(1, 2) // arr.splice(起始下标, 删除个数)
arr.splice(1) // arr.splice(起始下标)表示从起始下标后面的全删
```

## 9 函数

### 9.1 函数使用

#### 9.1.1 函数命名规范

- 和变量名基本一致
- 尽量小驼峰式命名法
- 前缀应该为动词，命名建议：常用的动词
	- can 判断是否可以执行某个动作
	- has 判断是否含有某个值
	- is 判断是否为某个值
	- get 获取某个值
	- set 设置某个值
	- load 加载某些数据

#### 9.1.2 函数的声明

```JavaScript
function move() {
  console.log('move')
}
```

#### 9.1.3 函数的调用

```JavaScript
函数名()
```

### 9.2 函数传参

```JavaScript
function getSum(num1, num2) {
  document.write(num1 + num2)
}

getSum(10, 20)


function getSum2(arr) {
  document.write(arr[0] + arr[1])
}

getSum2([10, 20])
```

默认参数：

```JavaScript

function getSum(x = 2, y) {
  console.log('x = ' + x + ', y = ' + y)
}

getSum(3, 4) // x = 3, y = 4
getSum(3) // x = 3, y = undefined
getSum() // x = 2, y = undefined
```

### 9.3 函数返回值

```JavaScript
function getSum(x, y) {
  return x + y
}

let z = getSum(10, 20)
```

### 9.4 作用域

- 全局变量
	- 函数外部 let 的变量
- 局部变量
	- 函数内部 let 的变量

> 注意，如果函数内部，变量没有声明直接赋值 `sum = 2`，也当做全局变量看，但强烈不推荐

### 9.5 匿名函数

#### 9.5.1 函数表达式

具名函数（就是之前讲的函数）的调用可以写到任意位置，包括可以写到函数声明的前面。

匿名函数必须先声明后使用。

```JavaScript
let fn = function (x, y) {
  console.log(x + y)
}
fn(1, 2)
```

#### 9.5.2 立即执行函数

- 避免全局变量之间的污染。
- 最后必须加分号结尾。
- 函数会立即执行

```JavaScript
// 这样会报错：
// let num = 10
// let num = 20
// 可以这样：
(function () {
  let num = 10
})();
(function () {
  let num = 20
})();

// 比如：
(function (x, y) {
  console.log(x + y)
})(1, 2);

// 第二种写法：
(function (x, y) {
  console.log(x + y)
}(1, 2));
```

### 9.6 逻辑中断

就是 Java 里面的短路。

```JavaScript
function fn(x = 0, y = 0) {
  console.log(x + y)
}

// 以上函数也可以用下面的方式写
// 如果左边有值，那么就没必要再判断右边
// 相当于给了默认值0
function fn(x, y) {
  x = x || 0
  y = y || 0
  console.log(x + y)
}
fn(1, 2)
fn()
```

## 10 对象

对象（object）可以理解为是一种无序的数据集合。

### 10.1 对象使用

#### 10.1.1 声明对象

对象由属性和方法组成。

```JavaScript
let 对象名 = {
  属性名: 属性值,
  方法名: 函数
}
let 对象名 = new Object()

let obj = {
  name: '小米15',
  num: '100020384578',
  price: '4999元'
}
```

#### 10.1.2 操作对象

```JavaScript
let obj = {
  uname: '张三',
  age: 18,
  gender: '男'
}
```

##### 10.1.2.1 查

对象. 属性

对象\[' 属性 ']

```JavaScript
obj.uname
// 如果属性名是字符串，比如 'user-name' = '张三'， 则：
obj['user-name'] // 可以防止-符号导致obj.user-name解析错误
// 当然 uname = '张三' 这样的也可以 obj['uname'] 来使用
```

##### 10.1.2.2 改

对象. 属性 = 值

```JavaScript
obj.uname = '李四'
```

##### 10.1.2.3 增

对象. 新属性 = 值

```JavaScript
obj.phoneNum = '15552257382'
```

##### 10.1.2.4 删

delete 对象. 属性

```JavaScript
delete obj.phoneNum
```

#### 10.1.3 对象中的方法

```JavaScript
let person = {
  name: '张三',
  sayHi: function(x, y) {
    document.write('hi')
  }
}
person.sayHi(1, 2)
```

### 10.2 遍历对象

增强 for 循环。

> 之前的 [[#7.2.2 for 循环|普通for循环]]

```JavaScript
let obj = {
  uname: '张三',
  age: 18,
  sex: '男'
}

for (let k in obj) {
  console.log(k) // 属性名，是字符串型
  console.log(obj[k]) // 属性值
}
```

### 10.3 内置对象

JavaScript 内部提供的对象，包含各种属性和方法给开发者调用。

#### 10.3.1 内置对象 Math

```JavaScript
Math.PI
Math.ceil(1.4) // 向上取整,2
Math.floor(1.4) // 向下取整，1
Math.round(1.4) // 四舍五入，1
Math.max(1, 2) // 最大值，2
Math.min(1, 2, 3) // 最小值，1
Math.pow(2, 3) // 幂运算，2^3，8
Math.abs(-1) // 绝对值，1
Math.random() // 生成[0, 1)之间的随机数
Math(Math.random() * (N - M + 1)) + M // 生成[M, N]的随机整数
```

