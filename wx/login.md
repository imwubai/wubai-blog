# 微信授权登录流程

```js
// login接口携带的三个参数（用户点击授权时候微信返回）
encryptedData: encryptedData,
js_code: res.code,
iv: iv,

// 写死保存在后端的三个字段
appid: AppId,
secret: AppSecret,
grant_type: 'authorization_code',
```

>1. 前端发起login请求，携带encryptedData、js_code、iv（用户点击授权时候微信返回的3个字段）
>2. 后端login接口拿到前端传入的其中1个参数（js_code），再组合3个写死的参数（appid、secret、grant_type）去请求微信的jsCode2Session接口，返回openid + session_key
>3. 根据openid的唯一性，去注册用户，如果注册过了则不用注册
>4. 后端生成token，并且跟openid、session_key建立唯一绑定关系（后面所有请求携带token，后端根据token反查openid定位到用户，判断权限等）
>5. 后端用session_key解密前端传入的encryptedData（这时候会用到前端传入的encryptedData、iv）
>6. 后端返回前端解密后的数据对象、token
>7. 前端wx.setStorage储存token、用户信息(如有必要)


**注意：用户openid唯一、session_key主要用来解密数据**