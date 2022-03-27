# JavaScript基础知识.md

# 创建变量的六种方式

- **ES3**

  1、var a = 100;

  2、创建函数

  function test(){

  ​	……

  }

- **ES6**

  3、let a = 100;

  4、const a = 100;

  5）模块导入

  import a from 'lib/a.js'

  6）创建一个类

  class animal{

  }

# 数据类型

- 基本数据类型
  - string类型
  - number类型
  - boolean类型
  - 特殊值：null&undefined

- 引用数据类型
  - object类型
    - 普通对象Object类型：`{}`
    - 数组类型：`[]`
    - Math对象类型
    - Date日期对象类型
    - ……
  - 函数类型`function`

  

### 基本数据类型

---

#### 1、string类型

---

> 所有用单引号、双引号、反引号（ES6模板字符串）抱包起来的都是字符串类型；



##### 把其他类型的值转换为字符串

- 函数toString()
- 字符串拼接



##### **函数toString**

数字类型（number）

```js
1314.toString() --->语法错误
(1314).toString --->'1314'
-----------------------------------------------------------------
let num = 1314;
num.toString() --->'1314'
```

布尔类型（boolean）

```js
(true).toString() --->'true'
(false).toString() --->'false'
```

null&undefined

```js
(null).toString() --->语法错误
(undefined).toString() --->语法错误
null和undefined是禁止直接调用toString方法的；
```

引用数据类型

```js
普通对象{}：
({name: '张三'}).toString(); --->[object Object]
数组[]：
[12,23] --->'12,23'
```



##### **字符串拼接**

加号遇见了字符串时，会产生字符串拼接，而不是加法运算；

```js
console.log(123+'123') --->'123123'
```





#### 2、number类型

---

> naumber类型就是数字类型，包括了像123、123.456这些常规的数字，以及特殊值：**NaN**；

**关于NaN**

1、**NaN**代表的是`not a number`,译为：`不是一个数字`；

2、`NaN`不与任何值相等(包括NaN自己)：

```javascript
console.log("123"==NaN);//false
console.log(123==NaN);//false
console.log("abc"==NaN);//false
console.log(NaN==NaN);//false
```





**判断一个值是否为有效数字：isNaN()**

> 判断一个值是否为数字可以使用函数`isNaN()`，将函数执行结果取反即可判断是否为数字；
>
> 函数`isNaN()`中传入非**数值型（number）**数据的时候，`isNaN()`会首先调用函数`Number()`来将传入的值转换为数字(number)类型，然后再判断转换后的值是不是一个**NaN**；
>
> 注意：这里只是判断转换后的值是不是一个**NaN**，而不是将转换后的值与**NaN**作比较，NaN与任何值都不相等（包括NaN自己）；
> 

**示例分析**

```javascript
isNaN("12a");	//->true
/*
 * 分析：
 * 第一步：调用函数Number()将传入的"12a"转换为number类型的值，即：
 * Number("12a") ->NaN
 * 第二步：判断函数Number()执行后的结果是否为一个NaN；
 * isNaN(NaN)-->true
 *
 * 总结：可以将函数isNaN()的结果取反来判断一个值是否为有效数字；
 */
```





**函数`Number()`总结分析**

> 函数**Number()**用于将其他类型的值转换为数字（number）类型的值，number类型的值包括**NaN**；
>
> number()函数是浏览器v8引擎底层的将其他类型值转换为数字的转换机制；

- 数字型（number）

```js
Number(1) --->1
```

- 字符型（string）

```js
1、内容是`纯有效数字`的字符串：
	Number("1") --->1
	Number("1.23") --->1.23
2、内容带`英文字母、空格、两个小数点`的字符串：
	Number("123abc") --->NaN
	Number("1 2") --->NaN
	Number("1.23.1") --->NaN
3、空字符串：``
	Number('') --->0
```

- 布尔型（boolean）

```js
Number(true) --->1
Number(false) --->0
```

- null&undefined

```js
Number(null) --->0
Number(undefined) --->NaN
```

- 什么都不填写

```js
Number() --->0
值得注意的是函数`isNaN()`什么都不填写返回true
```

- 引用数据类型

```js
Number({name: `张三`}) --->NaN
Number([]) --->0	
Number([123])、Number([`123`]) --->123
Number([123,124]) --->NaN
这是由于函数`Number()`中传入的是引用数据类型时，Number函数会调用引用类型数据的toString方法将引用类型数据转换为字符串，然后再转换为数字;

分析：Number({name: `张三`}) --->NaN
步骤一：
let person ={name: `张三`}
person.toString() --->'[object Object]'
步骤二：
Number('[object Object]') --->NaN
```



**将string类型转换为number类型的函数：`parseInt()`、`parseFloat()`**

>这两个函数也能将其他类型的值转换为number类型的值，但是与**Number()**的转换规则不一样。它们主要是用于将**字符串**转换为整型、浮点型数据；

- 字符型（string）

```js
纯数字的字符串直接转换为数字；
parseInt('123') --->123
parseInt('12.12') --->12

从左到右依次查找有效数字，遇见非有效数字立刻停止：
parseInt('123a') --->123
parseInt('a123') --->NaN 

空字符串转换为NaN：
parseInt('') --->NaN
```

- 其他类型：除了数组特殊，其他类型均为NaN；

```js
1、布尔型：先将true转换为字符串：'true'，然后再从左到右查看是否有有效数字；
	parseInt(true) 、 parseInt(false)--->NaN

2、null&undefined：转换方式与布尔值一样；
	parseInt(null)、parseInt(undefined) --->NaN

3、引用数据类型：先调用引用类型的toString方法转换为字符串，然后将字符串再从左到右查找有效数字；
	分析：parseFloat({age: 12})--->NaN
	var person = {age: 12};		person.toString() --->'[object Object]'
	parseFloat('[object Object]') --->NaN
	----------------------------------------------------------------------------------------------------------
	分析：perseFloat([12]) --->12
	首先：[12].toString --->'12'，然后：parseFloat('12') --->12
```





#### 3、boolean类型

---

> boolean类型就是布尔类型，有且仅有两个值：true和false；

##### 把其他类型的值转换为字符串

- Boolean()
- !、!!
- 条件判断



##### 函数Boolean()







#### 4、null&undefined

---

null和undefined都代表是**没有**；

- null：意料之中

  一般情况下都是我们开始时不知道变量的值，手动设置为初始空值null，后期再赋值为其它，null在堆栈内存当中没有空间；

  ```javascript
  let num = null;
  ……
  num = 10000;
  ```

```javascript
	let num;//num->undefined
```



### 引用数据类型

#### 普通对象类型

---

**普通对象的创建**

```javascript
let person = {
	name:'zhangsan',
	age:20,
	sex:'man',
	1:2000,
	……
}
```

- 上述代码创建了一个`person`对象，`person`对象有`name`等属性，属性与属性之间用`逗号`隔开；

- 对象的属性都是以键值对的方式指定的,`name`是属性名，`zhangsan`是属性值；

- 对象的属性名有字符串和数字两种；



**对象的属性值的获取**

```javascript
let person = {
	name:'zhangsan',
	age:20,
	sex:'man',
	1:2000,
}
//第一种方式获取属性值
console.log(person.name);//zhangsan
//第二种方式获取属性值
console.log(person['name']);//zhangsan
```

**注意**：对于数字属性名指定的属性只能以第二种方式获取

```javascript
//consol.log(person.1)	-->错误
console.log(person[1]);//2000	-->正确
```



**对象属性值的增加与修改**

```javascript
let person = {
	name:'zhangsan',
	age:20,
	sex:'man',
	1:2000,
}
person.intrest = 'basketbool';
```

对象的属性值的增加与修改采取`对象名.属性名/对象名[属性名] = ……`的方式设置

- 如果该对象没有这个属性，那就会新增这个属性并**赋值**等号右边的内容；
- 如果该对象已经存在这个属性，那么就会将该属性的属性值**修改**为等号右边的内容；



**对象属性值的删除**

```javascript
let person = {
	name:'zhangsan',
	age:20,
	sex:'man',
	1:2000,
}
//第一种删除方式
//delet person.name;
//第二种删除方式
person.name = null;
```

- 采用第一种方式会将对象的属性彻底删除；

- 采用第二种方式会将对象的属性值修改为`null`，并不是真的删除了这个属性；



#### 数组对象类型

---

**数组对象的创建**

```javascript
let array = [1,2,'dsadfgcuj',true];
```



**数组对象的属性的访问**

```javascript
let array = [1,2,'daisdwhqawd',false];
console.log(array[0]);//1
console.log(array[1]);//2
console.log(array[3]);//false
```

数组对象的属性的访问时采用下标的方式获取的，下标从`0`开始，依次递增，每增加一个属性，下标就自动加一。访问时只需采用`对象名+[属性对应的]`即可访问该属性的属性值；

数组存在一个默认的属性`length`，length属性的值就是这个数组的长度,该属性可以用`对象名.length`访问；

**注意：**由于数组的属性名是数字(下标)，所以`对象名.属性名`这种方式不适用于访问数组对象的属性(length属性除外)；



#### function类型

---

function的创建方式有两种

```javascrip
//第一种
function sum(a,b){
	……
}
//第二种
let sum = (a,b){
	……
}
```



### 数据类型的检测

---

- `typeof valName`&`typeof(valName)`：用来检测数据类型的运算符

  注意：`typeof`是一个运算符，而`typeof()`是一个函数；

- instanceof：用来检测当前对象是否隶属于某个类

- constructor：基于构造函数检测数据类型(也是基于类的方式)

- Object.prototype.toString.call()：检测数据类型最好的办法



#### 数据类型的转换

---

#### 转换为字符型

1+toString()

#### 转换为数字型

---

- 1+‘123’
- parseInt()函数；
- parseFloat()函数；
- Number()函数;





# 小知识

1、将网页变成可编辑状态

```js
document.body.contentEditable = true
恢复原状：
document.body.contentEditable = 'inherit'
```

