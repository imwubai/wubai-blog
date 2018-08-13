
# ES6 Class 的继承

```js
class Point {

    constructor () {
        this.name = 'My name is Point.'
    }

    toString () {
        return this.name;
    }

}
class ColorPoint extends Point {
    constructor (x, y, color) {
        super(x, y);
        this.color = color;
    }
    toString () {
        return this.color + '\n' + super.toString();
    }
}

let cp = new ColorPoint(1, 2, 'Red');
console.log(cp.toString());
```

###### ES5 的继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）。
###### ES6 的继承机制完全不同，实质是先将父类实例对象的属性和方法，加到this上面（所以必须先调用super方法），然后再用子类的构造函数修改this。

不管有没有显式定义，任何一个子类都有constructor方法。

在子类的构造函数中，只有调用super之后，才可以使用this关键字，否则会报错。这是因为子类实例的构建，基于父类实例，只有super方法才能调用父类实例。