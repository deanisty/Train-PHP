#### 自建CA

##### 创建顶级CA

```SHELL
# 生成CA秘钥 ca-key.pem
sudo openssl genrsa -des3 -out ca-key.pem
# 使用秘钥生成CA自签名证书 密码必填 后面颁发证书时使用
sudo openssl req -new -x509 -days 365 -key ca-key.pem -out ca.pem
```

##### 使用CA颁发服务器证书

```SHELL
# 生成服务器秘钥
sudo openssl genrsa -des3 -out server-key.pem
# 创建认证请求 需要填写服务器相关信息 common name 必须要写域名或者 *（允许所有）
sudo openssl req -new -key server-key.pem -out server.csr
# 向CA的序列号文件中写入值 也可以通过 -CAcreateserial 参数自动生成文件
echo 01 > ca.srl
# 使用服务器认证请求文件向CA申请颁发证书
sudo openssl x509 -req -days 365 -in server.csr  -CA ca.pem -CAkey ca-key.pem -out server-cert.pem -CAcreateserial
# 移除服务器秘钥文件的密码
sudo openssl rsa -in server-key.pem -out server-key.pem
```

##### 使用CA颁发客户的证书

```SHELL
# 生成客户端秘钥
sudo openssl genrsa -des3 -out client-key.pem
# 生成客户端认证请求文件 并使用私钥签名  需要填写客户的相关信息 common name 必须要写域名或者 *（允许所有）
sudo openssl req -new -key client-key.pem -out client.csr
# 设置CA属性 允许客户的认证
echo extenderKeyUsage = clientAuth > extfile.cnf
# 向CA申请颁发客户的证书
sudo openssl x509 -req -days 365 -in client.csr -CA ca.pem -CAkey ca-key.pem -out client-cert.pem -extfile extfile.cnf
# 移除客户端秘钥密码
sudo openssl rsa -in client-key.pem -out client-key.pem
```

##### 使用证书

将客户的的证书文件 client-cert.pem 秘钥 client-key.pem 和 CA证书复制到客户的机器 并相应配置
服务端使用 server-cert.pem server-key.pem 以及 CA证书 ca.pem进行配置
此后客户端和服务器即可使用 HTTPS 协议通讯
