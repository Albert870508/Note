# Node中的模块系统

#### Node应用程序

使用 Node 编写应用程序主要是在使用：

 + EcmaScript 语言
    + 和浏览器不一样，在 Node 中没有 BOM、DOM
 + 核心模块（**核心模块是Node内置模块，不需要安装，直接通过 `require('Name')` 使用即可**）
    + fs 文件操作模块
    + http 服务模块
    + url 路径操作模块
    + path 路径处理模块
    + os 操作系统信息模块
 + 第三方模块 (**需要通过 `npm install Name --save` 下载安装，然后通过 `require('Name')` 调用     **)
     + art -template 模块
     + express 模块
 + 自己写的模块
     + 自己创建的文件

#### 什么是模块化

 + 文件作用域
 + 通信规则
    + 加载
    + 导出

#### CommonJS 模块规范

在 Node 中的 JavaScript 还有一个很重要的概念：模块系统

+ 模块作用域
+ 使用 require 方法来加载模块
+ 使用 exports 接口对象导出模块中的成员

#### 加载 `require`

语法：

```javascript
var 自定义变量名称 = require('模块')
```

两个作用：

+ 执行被加载模块中的代码
+ 得到被加载模块中的 `exports` 导出接口对象

#### 导出  `exports`

+ Node 中是模块作用域，默认文件中所有的成员只在当前模块有效
+ 对于希望可以被其它模块访问的成员，我们就需要把这些公开的成员都挂载到 `exports` 接口对象中就可以了

**导出多个成员（必须在对象中）：**

```javascript
exports.a=123
exports.b='hello'
exports.c=function(){
    console.log('ccc')
}
exports.d={
    foo:'bar'
}
```

**导出单个成员（拿到的就是：函数、字符串）**

```javascript
module.exports='hello'
```

以下情况会覆盖：

```javascript
module.exports='hello'
//以这个为准，后者会覆盖前者
module.exports=function(x,y){
    return x+y
}
```

也可以这样来导出多个成员：

```javascript
module.exports={
    add:function(x,y){
        return x+y
    },
    str:'hello'
}
```

