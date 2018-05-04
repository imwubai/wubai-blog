
# node + express + multer上传图片

## 一、服务端配置

在express生成器生成的项目里找到根目录下的app.js，并进行以下修改


1.引入安装依赖

```js
var fs = require('fs')
var multer = require('multer')
var upload = multer({ dest: 'uploads/' })
```

2.添加上传图片的路由

```js
// 多个文件上传
app.post('/upload-multiple', upload.array('myfile', 2), function (req, res, next) {

	// 上传的多个文件的信息，数组类型
	let files = req.files;

	files.map((obj, i) => {
		let suffix = obj.originalname.split('.')[1];
		fs.renameSync(obj.path, obj.path + '.' + suffix);
	})

	res.send("done");
})

// 单个文件上传
app.post('/upload', upload.single('logo'), function (req, res, next) {

	// 上传的文件信息
	let file = req.file;

	// 图片后缀
	let suffix = file.originalname.split('.')[1];

	fs.renameSync(file.path, file.path + '.' + suffix);

	res.send('done');

});
```

## 二、客户端配置

创建一个html并且写入：

```html
<form enctype="multipart/form-data" action="/upload" method="post">
    <input type="file" name="logo"></input>
    <input type="submit" value="提交"></input>
</form>


<br/><br/><br/>

<form enctype="multipart/form-data" action="/upload-multiple" method="post">
    <input type="file" name="myfile"></input>
    <input type="file" name="myfile"></input>
    <input type="submit" value="提交"></input>
</form>
```