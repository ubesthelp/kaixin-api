# API 列表

## 待设计

- [x] 会话（session）
  - [x] 登录（`POST /session`）
  - [x] 注销（`DELETE /session`）
  - [x] 更新令牌（`PATCH /session`）
- [x] 用户（user）
  - [x] 注册新用户（`POST /user`）
    - [x] 获取用户名/email 是否已被注册（`GET /user/availability`）
    - [x] 发送验证邮件（`POST /email/vcode`）
  - [x] 修改密码（`PATCH /user`）
  - [x] 设置密码（`PATCH /user/{username}`，内部 API，不对外开放）
  - [x] 发送重置密码链接邮件（`POST /email/reset-password`）
- [x] 电子商务（ecomm）
  - [x] 使用序列号激活（`POST /ecomm/activation`，内部 API，不对外开放）
  - [x] 获取支付二维码链接（`POST /ecomm/payment-url`，内部 API，不对外开放）
  - [x] 注册反向通知（`POST /ecomm/notification`，WebSocket 协议）
  - [x] 注销反向通知（`DELETE /ecomm/notification`，WebSocket 协议）
- [x] 其它
  - [x] 获取设备 ID（`POST /device-id`）
  - [x] 获取软件授权（`GET /auth`）
  - [x] 获取素材链接（`GET /materials`）
  - [x] 获取软件最低可用版本（`GET /lowest-version`）
  - [x] Web 页面直达（`GET /web-url`，注册、修改密码、重置密码、购买、激活）

