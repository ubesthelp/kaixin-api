# 认证与授权

## 需要认证与授权的 API

绝大多数 API 都需要在认证与授权之后才能调用，除了以下 API：

* 登录
* 更新令牌
* 注册新用户
* 发送重置密码邮件
* 重置密码

## 认证与授权流程

### 登录

登录成功后，系统将返回如下响应：

```json
{
    "code": 0,
    "msg": "",
    "data": {
        "access_token": "访问令牌",
        "expires_in": 3600,
        "refresh_token": "更新令牌",
        "refresh_token_expires_in": 2592000,
        "id_token": "JWT"
    }
}
```

其中，`access_token`和`id_token`将在调用 API 时使用。`id_token`为 [JWT](https://jwt.io/) 格式，使用 JWK RS256 算法签名，公钥为：

* JSON 格式

    ```json
    {
        "kty": "RSA",
        "e": "AQAB",
        "kid": "2020-07-23T01:45:50Z",
        "alg": "RS256",
        "n": "hCv3iNGsEa7pJ6yprVENcMwgRJNjHmlNM5v_gzat5zqkt3Vt29_9Afy89cyQd3emKskKQoNoEHfl48NWjFsO45Bgwx5ysqNONGcn2-eBTQ2UbuEyu6lPX1cWSkFNMcHkWIYCHXXWcqJ24mAuwDLMWY4uSu_THYdB3zlCIvADdW8c8BPJP9O9qz92CThoOnd00e56KMnho6kY3IT-V7UqGXEaNi58LhCbuxqezi64A50afEv8Qyw5HZNADZt_Z-wOv9cth-OdsT8cwA_BlWbMfjUjCDD70qsaPbT_uZrzcLDKdywzb_a-D75DDlLAmEby_CsUHch2PDZScylJavj0xQ"
    }
    ```

* X.509 PEM 格式

  ```
  -----BEGIN PUBLIC KEY-----
  MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAhCv3iNGsEa7pJ6yprVEN
  cMwgRJNjHmlNM5v/gzat5zqkt3Vt29/9Afy89cyQd3emKskKQoNoEHfl48NWjFsO
  45Bgwx5ysqNONGcn2+eBTQ2UbuEyu6lPX1cWSkFNMcHkWIYCHXXWcqJ24mAuwDLM
  WY4uSu/THYdB3zlCIvADdW8c8BPJP9O9qz92CThoOnd00e56KMnho6kY3IT+V7Uq
  GXEaNi58LhCbuxqezi64A50afEv8Qyw5HZNADZt/Z+wOv9cth+OdsT8cwA/BlWbM
  fjUjCDD70qsaPbT/uZrzcLDKdywzb/a+D75DDlLAmEby/CsUHch2PDZScylJavj0
  xQIDAQAB
  -----END PUBLIC KEY-----
  ```

API 调用方可以验证 JWT 的签名是否有效，并从中提取用户相关信息。JWT 中至少包含以下 claims：

* iss
* sub：用户标识，目前就是用户名
* aud：软件编号
* iat
* exp
* email
* status：用户状态，0 - 无效用户，1 - 下次登录强制修改密码，2 - 密码已确认
* secret：base64 编码字符串，用户密钥，可用于本地数据库对称加密
* agent_code：代理编号

### 调用 API

调用 API 时，需要在 URL 查询字符串中添加 a 参数，值为登录时获取的`access_token`；同时在 HTTP Headers 中添加 Authorization 头，值为 Bearer + 半角空格 +`id_token`。

