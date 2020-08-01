# kaixin-api

![](https://img.shields.io/badge/version-0.1-blue) ![](https://img.shields.io/badge/OpenAPI-3.0-green)

开心 Open API，使用 [OpenAPI 3.0 规范](https://swagger.io/specification/)定义。通过 [Swagger Codegen](https://swagger.io/tools/swagger-codegen/)，可以根据 API 定义文件生成服务端测试桩、各语言版本的客户端 SDK 和 API 说明文档。当前版本 0.1，在线文档可以在[这里](https://app.swaggerhub.com/apis-docs/ubesthelp/kaixin/0.1)查看。

所有 API 都需要签名才能使用，签名算法文档见[这里](docs/SIGNATURE.md)。绝大部分 API 需要在认证及授权（即登录）之后才能使用，详细文档见[这里](docs/AUTH.md)。

## 目录结构

- [yaml-resolved](yaml-resolved)

  解析后的 OpenAPI 3.0 定义文件。

- [html2](html2)

  由上述文档生成的静态 HTML 说明文档。

- [docs](docs)

  API 相关的其它文档。

## 目前可用 API

- 注册新用户（`SignUp - POST /user`）
- 登录（`SignIn - POST /session`）
- 修改密码（`ChangePassword - PATCH /user`）
- 设置密码（`SetPassword - PATCH /user/{username}`）
- 发送验证邮件（`SendVCodeEmail - POST /email/vcode`）
- 发送重置密码邮件（`SendResetPasswordEmail - POST /email/reset-password`）
