# JavaScript基础知识

## 一、变量

### 1、变量的声明

ES3：

````javascript
var a = 20;
````



ES6:

```javascript
变量
let a = 100;
常量
const  b = 200;
```



## 二、数据类型

- 基本数据类型
  - string类型
  - number类型
  - boolean类型
  - 特殊值：null&undefined

- 引用数据类型
  - object类型
    - 普通对象Object类型
    - 数组类型
    - Math对象类型
    - Date日期对象类型
    - ……
  - function函数类型

  

### 1、基本数据类型

---

#### string类型

---

string类型就是字符串类型，例如：`‘12342342’`、`‘你好，世界！'`等都是字符串类型的数据；



#### number类型

---

> naumber类型就是数字类型，包括了像123、123.456这些常规的数字，以及特殊值：**NaN**；



**关于NaN**

- **NaN**代表的是`not a number`,译为：`不是一个数字`；
- `NaN`不与任何值(包括NaN)相等,所以不能用`==`来与其他类型值作比较判断其他值是否为数字；

```javascript
console.log("123"==NaN);//false
console.log(123==NaN);//false
console.log("abc"==NaN);//false
console.log(NaN==NaN);//false
```



**判断一个值是否为数字**

- 判断一个值是否为数字可以使用函数`isNaN()`来实现；
- 函数`isNaN()`会首先调用函数`Number()`来将传入的值转换为数字(number)类型，然后再判断转换后的值是否为NaN；

```javascript
isNaN("12a");	//->true
/*
 * 分析：
 * 第一步：调用函数Number()将传入的"12a"转换为number类型的值，即：
 * Number("12a") ->NaN
 * 第二步：判断函数Number()执行后的结果是否为NaN；
 *
 * 总结：可以将函数isNaN()的结果取反来判断一个值是否为数字；
 */
```



**关于函数Number()**

常见类型值调用示例

| Number函数调用示例     | 返回结果 |
| ---------------------- | -------- |
| Number(1)              | 1        |
| Number("1")            | 1        |
| Number("1.1")          | 1.1      |
| Number("abc")          | NaN      |
| Number("1ad")          | NaN      |
| Number(true)           | 1        |
| Number(false)          | 0        |
| Number(null)           | 0        |
| Number(undifined)      | NaN      |
| Number({title:"test"}) | NaN      |
| Number([])             | 0        |
| Number([1])            | 1        |
| Number([1,2])          | NaN      |



总结：

基本数据类型

- 数字

  调用Number函数时传入数字，则返回这个数字本身；

- 字符串
传入"123"这样的值(字符串里是纯数字)会返回为数字123，传入"123das"这样的值(字符串里面带有其他字符<第一个小数点除外>则)返回 NaN，表示这不是一个有效数字；

 * 布尔类型

   true-->1、false-->0；

 * 特殊值null&undefined

   null--->0、undefined-->NaN；



引用数据类型

将引用数据类型的数据转换为数字，首先会调用toString()方法将其转换为字符串，然后再转换为数字；




#### boolean类型

---

boolean类型就是布尔类型，有且仅有两个值：true和false；



#### null&undefined

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



### 2. 引用数据类型

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



### 3. 数据类型的检测

---

- `typeof valName`&`typeof(valName)`：用来检测数据类型的运算符

  注意：`typeof`是一个运算符，而`typeof()`是一个函数；

- instanceof：用来检测当前对象是否隶属于某个类

- constructor：基于构造函数检测数据类型(也是基于类的方式)

- Object.prototype.toString.call()：检测数据类型最好的办法



### 数据类型的转换

---

#### 转换为字符型

1+toString()

#### 转换为数字型

---

- 1+‘123’
- parseInt()函数；
- parseFloat()函数；
- Number()函数;
