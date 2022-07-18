---
title: JavaScript
date: 2021-04-18 21:07:18
tags:Javascript
---

### JavaScript基础

#### JavaScript范例

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title></title>
  </head>
  <body>
    <script>
      console.log('hello world');
    </script>
  </body>
</html>
```

#### 变量

##### 声明变量

```html
var name = '实验楼'；
```

##### 变量类型

- Number：你可以在变量中存储数字，不论这些数字是 10（整数），或者是 3.1415926（浮点数）。

    ```html
    var x1 = 10;
    var x2 = 3.1415926;
    ```

- String：存储字符（比如 "shiyanlou"）的变量，字符串可以是引号中的任意文本，你可以使用单引号或双引号，也可以在字符串中使用引号，只要不匹配包围字符串的引号即可：

    ```html
    var carname = 'shiyanlou';
    var carname = 'shiyanlou';
    var answer = "I Love 'shiyanlou'";
    var answer = 'I Love "shiyanlou"';
    ```

