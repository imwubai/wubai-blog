# 创建github page

### 1.选择自己的一个github项目

项目中包含已经打包好的build或者dist文件目录（纯静态html网站，github暂不支持类似React,vue的单页面）

### 2.安装gh-pages包

```js
npm install gh-pages --save
```

### 3.在package.json 文件中添加

```js
"predeploy": "npm run build", // 打包命令
"deploy": "gh-pages -d dist" // 创建一个分支名字叫gh-pages，内容是根目录下的dist文件夹内容
```

### 4.执行

```js
npm run deploy
```

执行 deploy 的时候会先执行 predeploy 命令

### 5.访问页面

在github项目中找到Settings选项卡，拉到下面会看到GitHub Pages，域名已经帮你自动生成好了，可以直接访问。