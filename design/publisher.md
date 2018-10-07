# Javascript设计模式 - 观察者模式

##### 观察者模式又叫发布—订阅模式，它定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都将得到通知。



```js
class Publisher {
    constructor() {
        this.clientList = {};
    }
    listen(key, fn) {
        this.clientList[key] = fn;
    }
    trigger(key, price) {
        let fns = this.clientList[key];
        if ( !fns ) {
            return false;
        }
        fns( price );
    }
    remove(key, fn) {
        delete this.clientList[key];
    }
}

var a = new Publisher();
a.listen('squareMeter88', function (price) {
    console.log(price)
})
a.listen('squareMeter100', function (price) {
    console.log(price)
})
a.trigger('squareMeter88', 20000);
a.trigger('squareMeter100', 30000);
a.remove('squareMeter88');
a.trigger('squareMeter88', 20000);
a.trigger('squareMeter100', 30000);

// --------------------------------------------------------
console.log('----------------------')

var b = new Publisher();
b.listen('squareMeter88', function (price) {
    console.log(price)
})
b.listen('squareMeter100', function (price) {
    console.log(price)
})
b.trigger('squareMeter88', 21000);
b.trigger('squareMeter100', 31000);
```