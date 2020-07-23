# kaixin-api
开心 Open API。

当前版本 0.1，在线文档可以在[这里](https://app.swaggerhub.com/apis-docs/ubesthelp/kaixin/0.1)查看。

## 目录结构

- [yaml-resolved](yaml-resolved)

  解析后的 OpenAPI 3.0 YAML 格式文档。

- [html2](html2)

  由上述文档生成的静态 HTML 说明文档。

## 目前可用 API

- 注册新用户（`SignUp - POST /user`）
- 登录（`SignIn - POST /session`）

## 相关文档

- [API 签名算法](docs/SIGNATURE.md)
- [认证与授权](docs/AUTH.md)
