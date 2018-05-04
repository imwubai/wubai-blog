
# new Date不同时区转换

代码如下：

```js
function calcTime(city, offset) { 
  var d = new Date(); 
  var utc = d.getTime() + (d.getTimezoneOffset() * 60000); 
  var nd = new Date(utc + (3600000 * offset)); 
  return "The local time in " + city + " is " + nd.toLocaleString(); 
}

alert(calcTime('Singapore', '+8'));//强制转换成中国时间
alert(calcTime('Singapore', -(new Date()).getTimezoneOffset()/60));//各地当地时间
```