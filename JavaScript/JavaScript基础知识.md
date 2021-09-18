# JavaScript基础知识

## 二、数据类型

- 基本数据类型
  - string类型
  - number类型
  - boolean类型
  - null&undefined

- 引用数据类型
  - object类型
    - 普通对象类型
    - 数组类型
    - Math对象类型
    - Date日期对象类型
    - ……
  - function类型

  

### 1. 基本数据类型

---



#### string类型

---

string类型就是字符串类型，例如：`‘12342342’`、`‘你好，世界！'`等都是字符串类型的数据；



#### number类型

---

- naumber类型就是数字类型，包括了像123、123.456这些常规的数字，以及**NaN**;
- **NaN**代表的是意思是：NOT A NUMBER,翻译为中文就是`不是一个数字`的意思；
- 注意区分大小写：N a N
- 每个NAN的值是不一样的，以下程序的结果是false:

```javascript
let a=NaN;
let b=NaN;
alert(a==b);//false
```



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

  

- undefined：意料之外

  创建一个变量不赋值，默认值就是undefined

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
