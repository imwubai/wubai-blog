# Javascript设计模式 - 单例模式

##### 单例模式的定义是：保证一个类仅有一个实例，并提供一个访问它的全局访问点。

```js
var getSingle = function (fn) {
    var result;
    return function () {
        return result || (result = fn.apply(this, arguments));
        // return result || (result = fn());
    }
};

var createLoginLayer = function () {
    var div = document.createElement('div');
    div.innerHTML = '我是登录浮窗';
    div.style.display = 'none';
    document.body.appendChild(div);
    return div;
};

var createSingleLoginLayer = getSingle(createLoginLayer);

document.getElementById('loginBtn').onclick = function () {
    var loginLayer = createSingleLoginLayer();
    loginLayer.style.display = 'block';
};
```