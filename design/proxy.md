# Javascript设计模式 - 代理模式

##### 代理模式是为一个对象提供一个代用品或占位符，以便控制对它的访问



现在我们改变故事的背景设定，假设当 A 在心情好的时候收到花，小明表白成功的几率有 60%，而当 A 在心情差的时候收到花，小明表白的成功率无限趋近于 0。

小明跟 A 刚刚认识两天，还无法辨别 A 什么时候心情好。如果不合时宜地把花送给 A，花 被直接扔掉的可能性很大，这束花可是小明吃了 7 天泡面换来的。

但是 A 的朋友 B 却很了解 A，所以小明只管把花交给 B，B 会监听 A 的心情变化，然后选 择 A 心情好的时候把花转交给 A，代码如下:

```js
var Flower = function () { };
var xiaoming = {
    sendFlower: function (target) {
        var flower = new Flower();
        target.receiveFlower(flower);
    }
};
var B = {
    receiveFlower: function (flower) {
        A.listenGoodMood(function () {
            A.receiveFlower(flower);
        });
    }
};
var A = {
    receiveFlower: function (flower) {
        // 监听 A 的好心情
        console.log('收到花 ' + flower);
    },
    listenGoodMood: function (fn) {
        setTimeout(function () { // 假设 10 秒之后 A 的心情变好
            fn();
        }, 10000);
    }
};
xiaoming.sendFlower(B);
```


##### 虚拟代理实现图片预加载

现在开始引入代理对象 proxyImage，通过这个代理对象，在图片被真正加载好之前，页面中将出现一张占位的菊花图 loading.gif, 来提示用户图片正在加载。代码如下：

```js
var myImage = (function () {
    var imgNode = document.createElement('img'); document.body.appendChild(imgNode);
    return {
        setSrc: function (src) {
            imgNode.src = src;
        }
    }
})();
var proxyImage = (function () {
    var img = new Image; img.onload = function () {
        myImage.setSrc(this.src);
    }
    return {
        setSrc: function (src) {
            myImage.setSrc('../Desktop/loading.gif');
            img.src = src;
        }
    }
})();
proxyImage.setSrc('https://img.alicdn.com/tfs/TB1MaoKpIUrBKNjSZPxXXX00pXa-204-80.png');
```