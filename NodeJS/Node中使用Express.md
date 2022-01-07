# Node中使用Express

#### 安装：

```shell
npm install express --save
```

#### hello world:

```javascript
//导入express包
const express = require('express') 
//调用express顶级函数，相当于实例化，同时也创建了服务，类似于 http.createServer()
const app = express() 
app.get('/',(req,res)=>{
    res.send('Hello world') //express 对http服务进行了封装，不需要再调用 res.end()方法
})
app.listen(3000,()=>console.log('Example app listening on port 3000'))

```

#### 基本路由：

get:

```javascript
//当以 GET 方法请求 / 的时候，执行对应的处理函数
app.get('/',function(req,res){
    res.send('Hello World')
})
```

post:

```javascript
//当以 POST 方法请求 / 的时候，执行对应的处理函数
app.post('/',function(req,res){
    res.send('Got a POST request')
})
```

#### 静态服务：

```javascript
//直接访问public中的资源，url中不需要加/public 即：http://127.0.0.1:3000/index.html
app.use(express.static('public'))

//给public起了个别名，url中需要添加/static来访问public下面的资源 即http://127.0.0.1:3000/static/index.html
app.use('/static',express.static('public'))
app.use('/static',express.static(path.join(__dirname,'public')))

//通过 http://127.0.0.1:3000/public/index.html访问public下面的资源
app.use('/public',express.static('public'))
```

*总结：* `app.use(参数1,参数2)` 第二个参数是想要开放资源的目录，比如public，第一个参数是给这个目录起别名，可以为空，如果为空则url中直接从根目录访问相关资源，一般情况下 别名和目录名称应保持一致

#### 在Express中配置使用 `art-template` 模板引擎

+ [art-template-GitHub仓库](https://github.com/aui/art-template)
+ [art-template 官方文档](https://aui.github.io/art-template/)
+ [art-template 中文文档](https://aui.github.io/art-template/zh-cn/index.html)

安装：

```shell
npm install --save art-template
npm install --save express-art-template
```

配置：

```javascript
//第一个参数官方指定的是art，可以改成别的，比如 html,在使用的时候必须和这个类型一致
app.engine('art',require('express-art-template'))
```

使用：

```javascript
app.get('/',function(req,res){
    //express 默认会去项目中的views目录中寻找index.art，art和配置的第一个参数一致
    res.render('index.art',{
        title:'hello world'
    })
})
```

如果希望修改默认的 views 试图渲染存储目录，可以:

```javascript
//注意第一个参数 views 千万不要写错
app.set('views',目录路径)
```

#### 在express中获取 get 方法请求数据

如果请求方法是get，可以通过以下方法获取相应数据

```javascript
app.get('/pinglun',(req,res)=>{
     //req.query 就是get方法中的参数，以json的方法返回：{ name: '张三', message: '这是内容信息' }
      var comment = req.query      
      comment.dateTime='2021-04-16'
      comments.unshift(comment)
      res.redirect('/')
  })
```

#### 在express中获取表单 post 请求体数据

在 express 中没有内置获取表单 POST 请求体的API，这里我们需要使用一个第三方包： `body-parser` 

1. 安装：

   ```shell
   npm install body-parser --save
   ```

   

2. 配置

   ```javascript
   var express = require('express')
   //引包
   var bodyParser = require('body-parser')
   
   var app = express()
   
   //配置 body-parser 
   //只要加入这个配置，则在 req 请求对象上会多出来一个属性：body
   //也就是说你就可以直接通过 req.body 来获取表单 post 请求体数据了
   // parse application/x-www-form-urlencoded
   app.use(bodyParser.urlencoded({ extended: false }))
   
   // parse application/json
   app.use(bodyParser.json())
   
   app.use(function (req, res) {
     res.setHeader('Content-Type', 'text/plain')
     res.write('you posted:\n')
     //可以通过 req.body 来获取表单 post 请求体数据
     res.end(JSON.stringify(req.body, null, 2))
   })
   ```

   

