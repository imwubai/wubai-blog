
# Javascript 继承

个人收集整理的一些方法

#### 如下，有2个构造函数

```js
// Animal构造函数
function Animal(){
    this.species = "动物";
}
// Cat构造函数
function Cat(name,color){
    this.name = name;
    this.color = color;
}

```

#### 怎样才能使Cat继承Animal呢？

##### 一、 构造函数绑定

第一种方法也是最简单的方法，使用call或apply方法，将父对象的构造函数绑定在子对象上，即在子对象构造函数中加一行：

```js
function Cat(name,color){
    Animal.apply(this, arguments);
    this.name = name;
    this.color = color;
}

var cat1 = new Cat("大毛","黄色");

console.log(cat1.species); // 动物
```

##### 二、 prototype模式

```js
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;

var cat1 = new Cat("大毛","黄色");
console.log(cat1.species); // 动物
```


##### 三、 直接继承prototype

第三种方法是对第二种方法的改进。由于Animal对象中，不变的属性都可以直接写入Animal.prototype。所以，我们也可以让Cat()跳过 Animal()，直接继承Animal.prototype。

现在，我们先将Animal对象改写：

```js
function Animal(){ }
Animal.prototype.species = "动物";
```

然后，将Cat的prototype对象，然后指向Animal的prototype对象，这样就完成了继承。

```js
Cat.prototype = Animal.prototype;
Cat.prototype.constructor = Cat;
var cat1 = new Cat("大毛","黄色");
console.log(cat1.species); // 动物
```
