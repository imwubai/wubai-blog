# 常用正则总结

```js

// 匹配允许0的正整数，但是不允许01， 001格式
/^([1-9]\d*|[0]{1,1})$/

// 邮箱
/^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/
/^[A-Za-z\d]+([-_.][A-Za-z\d]+)*@([A-Za-z\d]+[-.])+[A-Za-z\d]{2,4}$/

// 座机号码
/^(([0\+]\d{2,3}-)?(0\d{2,3})-)(\d{7,8})(-(\d{3,}))?$/

// 手机号码
/^13[0-9]{9}$|14[0-9]{9}|15[0-9]{9}$|17[0-9]{9}$|18[0-9]{9}$/

// 图片格式
/\.(gif|jpg|jpeg|png|GIF|JPG|PNG)$/

// 身份证号码验证
/^(\d{15}$|^\d{18}$|^\d{17}(\d|X|x))$/

// 验证金钱格式，x or x.x or x.xx ,x为数字，不允许0开头
/^(?=[\d.]{1,15})([1-9]\d{1,14}|\d)([.][0-9]{0,2})?$/

// 1-15位的纯数字
/^\d{1,15}$/,

// 替换空格
'aa&nbsp;aa'.replace(/&nbsp;/g, ' ');

// 替换某某开始某某结尾
'<span width="100">1231231</span>'.replace(/\<span.*?\>/g, '');

```


#### 替换话题

```js
function stringToTopic (contentString) {
    // 转换下空格
    contentString = contentString.replace(/&nbsp;/g, ' ');
    let resultArr = [];

	let topicHtml = '<a href="javascript:;" class="J-topic" to="/topic?text=$1">#$1 </a>';


    // 判断是不是以前的老数据(textarea填写提交的)
    if ( contentString.includes('</p>') ) {
        let contentArr = contentString.split('</p>');
        contentArr.map((pString) => {

            // 把span标签剔除
            pString = pString.replace(/\<span.*?\>/g, '');
            pString = pString.replace(/\<\/span.*?\>/g, '');

            if ( pString.endsWith('#') ) {
                pString += '</p>';
                pString = pString.replace(/(?:#([^#\s]+)\s)/g, topicHtml);
            } else {
                pString += ' </p>';
                pString = pString.replace(/(?:#([^#\s]+)\s)/g, topicHtml);
            }

            resultArr.push(pString);

        })
    } else {
        resultArr.push(contentString.replace(/(?:#([^#\s]+)\s)/g, topicHtml));
    }

    return resultArr.join('');
}

```