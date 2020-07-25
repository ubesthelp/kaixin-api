# API 列表

## 待设计

- [x] 会话（session）
  - [x] 登录（`POST /session`）
  - [x] 注销（`DELETE /session`）
  - [x] 更新令牌（`PATCH /session`）
- [ ] 用户（user）
  - [x] 注册新用户（`POST /user`）
    - [x] 获取用户名/email 是否已被注册（`GET /user/availability`）
    - [x] 发送验证邮件（`POST /email/vcode`）
  - [x] 修改密码（`PATCH /user`）
  - [x] 设置密码（`PATCH /user/{username}`，内部 API，不对外开放）
  - [x] 发送重置密码链接邮件（`POST /email/reset-password`）
- [ ] 电子商务（ecomm）
  - [x] 使用序列号激活（`POST /ecomm/activation`）
  - [ ] 获取支付二维码链接（`POST /ecomm/payment-url`）
  - [ ] 注册反向通知
  - [ ] 注销反向通知
  - [ ] 支付成功通知
- [ ] 其它
  - [ ] 获取设备 ID
  - [ ] 获取软件授权
  - [ ] 获取素材链接
  - [ ] 获取软件最低可用版本
  - [ ] 获取 Shopee 域名列表
  - [ ] Web 页面直达（注册、修改密码、重置密码、购买/激活）

