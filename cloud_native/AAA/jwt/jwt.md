## jwt是什么？

>JSON Web Token (JWT) is a compact URL-safe means of representing claims to be transferred between two parties. The claims in a JWT are encoded as a JSON object that is digitally signed using JSON Web Signature (JWS).
-RFC7519 https://tools.ietf.org/html/rfc7519

jwt是一种安全标准仅仅是一个token的格式。他是经过数据签名的，他仅仅用来判定token在传输过程中是否被篡改。因为jwt中token包含三部分。

1. Header
    - 声明类型及签名使用的算法
        ```python
        {
            "alg" : "AES256",
            "typ" : "JWT"
        }
        ```
2. Claims声明 
    - claim是整个token的核心，表示要发送的用户信息。token有时候会被保存在客户端（例如浏览器）中使用
        ```python
        {
            "sub": "1234567890",
            "name": "John Doe",
            "admin": true
        }
        ```

3. signature签名
    - 签名是为了保证上面的两部分信息不被篡改。尝试使用base64对解码后的token进行修改，则signature就会失效。一般使用private key进行混淆。所以只有原始的token才能和签名匹配

所以我们可以看到， **jwt不是为了保证用户名不被窃取**。这个是由https来保证的。**jwt只是来保证这个token确实是由这个用户签发的**（因为修改claims会导致签名无效）
