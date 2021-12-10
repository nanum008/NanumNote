# 一、Vue环境搭建

## 1、`script`标签直接引入

> Vue是一个JavaScript框架，直接用script标签引入即可使用Vue；

制作原型或学习版本：包含完整的警告和调试模式

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
```

生产环境版本：删除了警告

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14"></script>
```

ps：`vue.min.js`能带来更加的性能体验；



## 2、安装Vue Devtools


> - 在使用 Vue 时，Vue推荐在浏览器上安装 [Vue Devtools](https://github.com/vuejs/vue-devtools#vue-devtools)。它为我们提供了一个更友好的界面来审查和调试 Vue 应用。
>
> - 当我们没有安装`Vue Devtools`的时候，使用Vue会在控制台看到如下的提示；

```
Download the Vue Devtools extension for a better development experience:
https://github.com/vuejs/vue-devtools
```

安装好`Vue Devtools`扩展后控制台的提示就会消失；



**Chrome安装：**

在Google的[Chroome网上应用商店](https://chrome.google.com/webstore/category/extensions?hl=zh-CN)搜索`Vue Devtools`添加扩展即可；



# 二、Vue的简单使用

## 1、入门案例：Hello Vue

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



## 2、插值表达式

> 插值表达式的作用就是将Vue对象里data属性(对象)的内容(属性)插入到HTML标签当中；
>
> 插值表达式只能将model层的内容插入到HTML标签的标签体当中，即开始标签到结束标签之间的内容才可以使用插值表达式，而HTML元素的属性值不能使用插值表达式；

```html
<a>只有在这里才可以使用插值表达式：{{}}</a>
```

## 3、v-bind

> `v-bind`的作用就是将Vue中model层的数据单向绑定到HTML标签的属性；

**格式**：v-bind:标签的属性名 = "要绑定的引用"；

**简写形式：**`v-bind`可以省略不写，即：`:标签的属性名 = "要绑定的引用"`；



**示例**

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

## 4、v-model

> 如果说v-bind是将model层的数据插入到html标签的属性值，那么v-model就是将html标签的属性与model层的数据进行双向绑定，视图层的数据变了，model层的数据也会跟着改变，二者互相影响，紧密连接；

**格式**：v-model:标签的属性名 = "要绑定的引用"；

**示例：**

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

通过v-model，视图层的数据与model层(data)的数据进行了紧密相连；以上例子中，我们如果在input标签输入任意内容后，那么model层的content属性值也会随之发生改变，那么也会导致插值表达式的内容发生变化；



## 5、el$data的两种写法

### 1）**el的两种写法：**

方式一：`el："css选择器"`

方式二：`var v = new Vue( data:……);	v.$mount("css选择器")`

二者的区别就在于方式一是在new Vue实例的时候就对vue的视图层进行绑定，而方式二则可以按需求来绑定视图，比如说创建好vue实例后等个几秒再绑定视图；



### 2）data的两种写法

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



## 6、数据代理

### 1)Objet.defineProperty()

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

### 2)数据代理

> 数据代理：通过一个对象代理对另一个对象属性的操作(读/写)；

```js
let obj = {x:100}
let obj2 = {y: 200}
object.defineProperty(obj2,'x',{
    get(){return obj.x},
	set(value){obj.x = value}
})
```

### 3)Vue中的数据代理

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



## 7、事件处理

### 1）v-on:click

> 当用户点击时触发对应的事件(函数)；

格式`v-on:click = "事件函数名"`

简写形式：`@click = "事件函数名"`



实例：

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

