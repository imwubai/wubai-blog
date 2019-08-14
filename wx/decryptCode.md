# 微信前端js解密数据

**注：一般是由后端解密的，微信不推荐把sessionKey返回前端**

```js
import CryptoJS from 'crypto-js'
import { Base64 } from 'js-base64'

interface parameter {
	encryptedData: string, // 微信授权返回的加密数据
	iv: string, // 微信授权返回的
	sessionKey: string, // 微信jscode2session接口返回的
}

let decryptCode = ({ sessionKey, iv, encryptedData }: parameter ) => {
	let Base64Key = CryptoJS.enc.Base64.parse(sessionKey)
	let Base64Iv = CryptoJS.enc.Base64.parse(iv)
	let decrypt = CryptoJS.AES.decrypt(encryptedData, Base64Key, {
		iv: Base64Iv,
		mode: CryptoJS.mode.CBC,
		padding: CryptoJS.pad.Pkcs7
	})
	return JSON.parse(Base64.decode(CryptoJS.enc.Base64.stringify(decrypt)))
}

export default decryptCode;
```