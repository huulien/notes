# MAC 生成RSA公钥私钥

## 准备
* 安装openssl
`brew install openssl`

## 生成私钥
`openssl genrsa -out rsa_private_key.pem 1024`

## 私钥转换成PKCS8格式
`openssl pkcs8 -topk8 -inform PEM -in rsa_private_key.pem -outform PEM –nocrypt`
回车后会要求输入密码以及确认密码

## 根据私钥成成公钥
`openssl rsa -in rsa_private_key.pem -out rsa_public_key.pem -pubout` 