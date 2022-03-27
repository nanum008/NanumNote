# Vue总结

# 一、Vue环境搭建

## 1、`script`标签直接引入

---

Vue是一个JavaScript框架，直接用script标签引入即可使用Vue；

- 制作原型或学习版本：可读性好，包含完整的警告和调试模式；

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
```

- 生产环境版本：删除了警告、压缩混淆等，性能更佳，但是可读性差，不利于程序员开发；

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14"></script>
```



## 2、安装Vue Devtools

---

在使用 Vue 时，Vue推荐在浏览器上安装 [Vue Devtools](https://github.com/vuejs/vue-devtools#vue-devtools)。它为我们提供了一个更友好的界面来审查和调试 Vue 应用。

当我们没有安装`Vue Devtools`的时候，使用Vue会在控制台看到如下的提示；

```
Download the Vue Devtools extension for a better development experience:
https://github.com/vuejs/vue-devtools
```

安装好`Vue Devtools`扩展后控制台的提示就会消失；



**Chrome安装：**

在Google的[Chroome网上应用商店](https://chrome.google.com/webstore/category/extensions?hl=zh-CN)搜索`Vue Devtools`添加扩展即可；





## 3、入门案例：Hello Vue

```html
<body>
    
    Vue实例会通过div的id属性找到该元素并将其绑定作为vue的视图层，div里的内容称之为模板，vue会对模板进行解析，解析之后在插入到这里；
    <div id="root">
        这里使用了插值表达式将Model层(data)中的数据插入到了这里，vue解析模板的时候会执行；
        hello {{name}}
    </div>
    
    通过script标签引入Vue框架；
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    
    <script type="text/javascript">
  	  new Vue({
          //将id为root的元素绑定到Vue，这就是Vue的视图层；
          //el的值可以是像下面这样的【css选择器】，也可以是【document.getElementByd()】这样的dom元素；
    	    el:'#root',
          //这是Vue的Model层；
     	   data:{
       	     name:"Vue",
         	 in:"nice"
        }
   	 });
    </script>
</body>
```

- 当我们运行时在控制台会看见如下两条提示信息：

```
Download the Vue Devtools extension for a better development experience:
https://github.com/vuejs/vue-devtools

vue.js:9108 You are running Vue in development mode.
Make sure to turn on production mode when deploying for production.
See more tips at https://vuejs.org/guide/deployment.html
```

第一条提示信息详情参见：`安装Vue Devtools`；

第二条提示信息是提示我们当前使用的是Vue的开发版本，想要关闭该提示信息的输出需要进行如下操作：

```html
这是对Vue的配置：关闭产品提示的输出；
建议放在script标签的第一行；
<script type="text/javascript">Vue.config.productionTip = false;</script>
```

# 二、Vue指令




## 1、插值表达式

> 插值表达式的作用就是将Vue对象里data属性(对象)的内容(属性)插入到HTML标签当中；
>
> 插值表达式只能将model层的内容插入到HTML标签的标签体当中，即开始标签到结束标签之间的内容才可以使用插值表达式，而HTML元素的属性值不能使用插值表达式；

/-/ 语法格式

```html
<a>只有在这里才可以使用插值表达式：{{ }}</a>
```

## 2、属性绑定（v-bind）

> `v-bind`的作用就是将Vue中model层的数据单向绑定到HTML标签的属性；

/-/ 语法格式

```js
v-bind:标签的属性名 = "要绑定的引用"；
---------------------------------------------------
简写形式：
:标签的属性名 = "要绑定的引用"；
注意：冒号不能省略；
```



/-/ 示例

```html
<div id="root">
        <a v-bind:href ="link">百度</a>
 </div>    
```

```js
new Vue({
        el:'#root',
        data:{
            name:"Vue",
            link:"https://www.baidu.com"
        }
 });
```



## 3、数据双向绑定（v-model）

> 如果说v-bind是将model层的数据插入到html标签的属性值，那么v-model就是将html标签的属性与model层的数据进行双向绑定，视图层的数据变了，model层的数据也会跟着改变，二者互相影响，紧密连接；

/-/ 语法格式

```js
v-model:标签的属性名 = "要绑定的引用"；
```



/-/ 示例

```html
<div id="root">
     <input type="text" v-model:value="content">{{content}}
 </div>    
```

```js
 new Vue({
        el:'#root',
        data:{
            content:"hello",
        }
    });
```

通过v-model，视图层的数据与model层(data)的数据进行了紧密相连；以上例子中，我们如果在input标签输入任意内容后，那么model层content属性值也会随之发生改变，那么也会导致插值表达式的内容发生变化；



## 4、el&data的两种写法

### 1、**el的两种写法：**

---

方式一：`el："css选择器"`

方式二：

```js
var v = new Vue( data:……);
v.$mount("css选择器")
```

二者的区别就在于方式一是在new Vue实例的时候就对vue的视图层进行绑定，而方式二则可以按需求来绑定视图，比如说创建好vue实例后等个几秒再绑定视图；



### 2、data的两种写法

---

方式一，对象式：`data：{……}`

方式二，函数式：

```js
//形式一：
data:function(){
    ……
    //此处return返回的对象就是方式一中想要的对象；
    return {……}
}

//形式二：
//既然data属性可以写成一个函数，那么这种形式更加方便；
data(){
     ……
    //此处return返回的对象就是方式一中想要的对象；
    return {……}
}
```



## 5、数据代理

### 5.1、Objet.defineProperty()

> 该方法可以为一个对象定义(追加)属性；
>
> 形参列表如下：
>
> defineProperty(Object 要定义属性的对象,String 属性名,Object 属性的配置对象)

```js
let number = 18;
let person = {name: "张三",sex:'男',};
Object.defineProperty(person , ' age',{
    // value: 18,
    //enumerable:true，//控制属性是否可以枚举，默认值是false
    // writable:true，//控制属性是否可以被修改，默认值是false
    //configurable:true //控制属性是否可以被删除，默认值是false
    
	//当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是该对象新定义的属性的值
    get(){
		console.log( '有人读取age属性了")；
        return number)；
    },
//当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的
    set(value){
	console.log("有人修改了age属性，且值是',value)
    number = value;
     }

```

### 5.2、数据代理

> 数据代理：通过一个对象代理对另一个对象属性的操作(读/写)；

```js
let obj = {x:100}
let obj2 = {y: 200}
object.defineProperty(obj2,'x',{
    get(){return obj.x},
	set(value){obj.x = value}
})
```

### 5.3、Vue中的数据代理

> Vue实例中`data的属性`都会通过Object.defineProperty()方法定义到Vue实例对象的属性当中，从而实现数据代理；

```js
 let vm = new Vue({
            el:"#root",
            data:{
                name:"Alex"
            }
        });
```

![image-20211120183624962](C:\Users\nanum008\AppData\Roaming\Typora\typora-user-images\image-20211120183624962.png)

我们创建了一个Vue实例,data对象有一个name属性;当我们在控制台输出这个实例的时候可以看见`vm`对象也有name属性，这个属性就是通过Object.defineProperty()方法为`vm`定义(追加)的属性；

`vm`还有一个属性`_data`就是我们创建Vue实例时定义的`data`;



## 6、事件处理

### 1、v-on:click

> 当用户点击时触发对应的事件(函数)；

 **语法格式**

v-on:click = "事件函数名"

简写形式：`@click = "事件函数名"`



**示例**

```html
    <div id="root">
        <button v-on:click="hello">点我</button>
    </div>
```

```js
   new Vue({
        el:'#root',
        methods:{
            hello(){
                console.log("hello");
            }
        }
    });
```

当用户点击的时候就会触发hello函数里的代码输出hello，响应用户的点击事件，与用户产生交互;



在我们定义的函数当中，我们还可以定义形参去接收用户点击时产生的`Event对象`，函数里使用关键字`this`代表的是当前的Vue实例；

```js
   new Vue({
        el:'#root',
        methods:{
            hello(event){
                console.log("hello");
                //输出点击的heml元素的文本信息；
                console.log(event.target.innerText);
                //输出vue实例
                console.log(this);
            }
        }
    });
```

| 测试结果                                                     |
| ------------------------------------------------------------ |
| ![image-20211120190449229](C:\Users\nanum008\AppData\Roaming\Typora\typora-user-images\image-20211120190449229.png) |

**ps**：`(event)=>{}`以这种形式定义的函数，在里面使用关键字`this`代表的是`window`，所以在vue里定义的函数不建议使用这种形式；

# 三、模板语法















# 四、Vue组件

## 1、组件的创建与使用

###  组件的创建

---/ 



---/ 单文件组件

单文件组件就是将一个单独的`.vue`文件作为一个Vue组件；

----/ 示例

`nav.vue`

```js
```





### 注册组件

--- 全局注册

```js
Vue.component(	'组件名'	，Vue组件实例	)
```



--- 局部注册

```js
//	这是一个vue组件实例
const vue1 = {
    template:	`<h1>{{msg}}</h1>`,
    data(){
        return{
            msg:'这是一个组件'
        }
    }
}

new Vue({
    //注册vue组件
    components:{
        vue1
    }
    ……
})
```









## 2、组件之间的通信



### 2.1、父子组件之间的通信



### 2.2、平行组件之间的通信







# 五、插槽



### 匿名插槽



### 具名插槽

# 四、前端工程化

### 1、npm简单使用

---

/-/ npm安装模块

---

/-//-/ 本地安装

在项目的根路径下执行以下命令即可；

```shell
npm install 模块名
npm i 模块名
```



/-//-/ 全局安装

```shell
npm install --global 模块名 
npm install -g 模块名
```



/-//-/ 安装并记录到属性`dependencies`中

```shell
npm install 模块名 --save
npm install 模块名 -S
```

在后面添加的参数`-S`表示安装模块完成后记录到npm的配置文件：`packge.json`的属性`dependencies`当中；

-S可以省略不写，默认会加上；



/-//-/ 安装并记录到属性`devDependencies`当中

```shell
npm install 模块名 --save-dev
npm install 模块名 -D
```

在后面添加的参数`-D`表示安装模块完成后记录到npm的配置文件：`packge.json`的属性`devDependencies`当中；

-D和-S之间的区别在于，-D表示只在开发阶段才会用到，而-S表示在开发和部署上线的时候都会用到；



/-//-/ 查找npm模块

npm的模块信息可以在npm提供的[官方网站](https://www.npmjs.com/)上查找；



### 2、webpack的简单使用

---

/-/ 简单使用webpack打包项目

---

① 在文件`package.json`中配置；

```json
{
    ……
    "scripts" : {
    	"build" : "webpack"
	}
}
```

② 在项目的根路径下创建文件：`webpack.config.js`，这是webpack的配置文件，进行如下的配置；

```js
module.exports={
    // mode用来指定构建模式，可选值：①production、②development
    // ①production：代表项目部署上线阶段
    //		--/ 优点：
    //		，对生成的文件会进行压缩处理（去除换行和空格），这样生成的js文件的体积会缩小很多
    //		这样网络传输速度快，网页渲染时间短，客户的体验好；
    //		--/ 缺点
    // 		压缩处理代码会比development模式花费更多的时间，项目构建慢；
    // development：代表开发阶段；
    //		不会对代码进行压缩处理，构建速度快，
    mode : "develpoment"
}
```

③ 在终端输入以下命令即可打包构建项目；

```shell
npm run build
```

项目打包构建好之后默认会输出到项目根目录下的dist目录下的文件：`main.js`当中，我们只需要在`html`文件中引入即可；



/-/ 配置打包文件和输出文件

---

/-//-/ webpack打包文件的默认配置

在webpack4.x和5.x版本中，有以下默认的约定：

① 默认的打包文件为：src/index.js；

② 默认的输出文件为：dist/main.js；



/-//-/ 配置打包文件

在文件`webpack.config.js`中进行如下配置：

```js
module.exports = {
    mode : 'development',
    entry : '打包文件的路径'
}
```



/-//-/ 配置输出文件

在文件`webpack.config.js`中进行如下配置：

```js
module.exports = {
    mode : 'development',
    output : {
        filename : '输出的文件名',
        path : '输出路径'
    }
}
```



/-//-/ 示例

webpack.config.js

```js
const path = require('path')

module.exports = {
    mode : 'development',
    entry : path.join(__dirname , "./src/index.js"),
    output:{
        filename:'bundle.js',
        path:path.join(__dirname,'dist')
    }
}
```



/-/ webpack-dev-server插件

---

/-//-/ 情景

由于我们引入的是webpack打包生成的文件，在我们每一次改动代码后都得执行命令`npm run ……`才能保证新改动的代码生效；这样做非常麻烦，于是我们可以安装插件`webpack-dev-server`来帮助我们：每次改动源代码后，自动运行命令：`npm run ……`为我们打包构建；



/-//-/ 安装命令

```shell
npm install webpack-dev-server -D
```



/-//-/ 使用`webpack-dev-server`插件

①  `packge.json`配置

```json
{
    ……
     "scripts": {
    "build": "webpack serve"
  }
}
```

② 执行`npm run build`；

③说明：

执行以上步骤以后当我们修改源代码按下`Ctrl + S`保存，这个插件就会监听到源码的改动，自动的为我们打包构建项目；

该插件会启动一个实时的http服务器，生成的项目的访问路径在：http://127.0.0.1:8080/src/index.html；

这个时候生成的文件并没有放在我们的本地磁盘上，而是在内存当中。这样做是由于我们频繁的改动代码，放在磁盘的话速率会降低，而且频繁的读写磁盘也会影响磁盘的寿命，于是将其放在了内存当中；

我们可以在项目的根目录下访问到该文件，即：http://127.0.0.1:8080/bundle.js

于是我们在html文件中引用该文件的路径也应该变：

```html
<script src="/bundle.js"></script>
```



/-//-/ 更多配置

在webpack.config.js当中，我们可以对该插件进行更多的配置

```js
{
    ……
        devServer:{
        static:path.join(__dirname),
        // 配置第一次运行时自动打开浏览器；
        open:true,
        // 配置运行的主机地址；
        host:'127.0.0.1',
        // 配置主机端口号；
        port:'80'
    }
}
```





/-//-/ 可能会遇到的问题

--/ 访问http://127.0.0.1:8080出现：Can not get /

解决办法：在webpack.config.js中进行如下配置

```js
const path = require('path')
module.exports = {
        devServer:{
       	 static:path.join(__dirname)
    }
}
```



/-/ html-webpack-plugin插件

---

/-//-/ 作用

将src目录下的html文件复制一份到其他目录下；

将内存当中的



/-//-/ 安装命令

```shell
npm install html-webpack-plugin -D
```



/-//-/ 配置html-webpack-plugin

`webpack.config.js`

```js
const path = require('path')
// 导入html-webpack-plugin插件，得到该插件的构造函数；
const HtmlPlugin = require('html-webpack-plugin')

//根据构造函数创建该插件的实例；
const htmlPlugin = new HtmlPlugin({
    template:'./src/index.html',
    filename:'./index.html'
})

module.exports = {
    mode : 'development',
    entry : path.join(__dirname , "./src/index.js"),
    output:{
        filename:'bundle.js',
        path:path.join(__dirname,'dist')
    },
    devServer:{
        static:path.join(__dirname)
    },
    //在webpack中声明该插件实例，使其生效；
    plugins:[htmlPlugin]
}
```

这样，我们在浏览器输入http://localhost:8080即可访问项目的index.html；



/-/ loader加载器

---

webpack默认只能打包处理js文件，要想处理其他的文件，就得安装并配置对应的loader；



/-//-/ 示例：

若是项目中使用到了css文件，而不安装css文件的loader的话会报错；

这个时候就得安装模块：

```shell
npm install style-loader css-loader -D
```

安装完成之后在文件`webpack.config,js`中进行配置：

```js
module.exports = {
    ……
     module:{
        rules:[
            {
    		//文件类型
            test:/\.css$/,
    		//使用何种loader
            use:['style-loader','css-loader']
             }
        ]
    }
}
```





# 五、VUe-router

