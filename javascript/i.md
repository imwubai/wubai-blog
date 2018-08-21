
# 详解 i++ 和 ++i


```js
// i++ 先赋值 再自加
function(i){
  var r;
  r = i;
  i = i + 1;
  return r;
}

// ++j 先自加 再赋值
function(j){
  var r;
  j = j + 1;
  r = j;
  return r;
}


```