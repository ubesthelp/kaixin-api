# 简单设备指纹生成方法

设备授权的应用在获取用户授权前需要向服务端发送设备指纹以获取设备 ID，本文说明简单设备指纹的生成方法。

## 简单设备指纹

简单设备指纹是一串形如“xxx”的 base64url 编码的字符串，例如：

```
eyJiaSI6IjNkYWQwMmUxNTM4NTc1YTgzYjM4NDRkMjlkM2NlMWNlIiwiYmIiOiI2YjZmN2RkZjg2ODNjM2Y0MmI2MDFlOTMwNGFhNmJhNyIsInNtIjoiZTdjMzI2YjM1YWI1N2U3ZmZiNGY2NDRkYjEyYmUxNGUiLCJtYSI6ImI2NzEzNGNmNzQ0NmFlODkyYjViMzVlMTNhZThiNDYwIiwibW8iOiJhODAyNjg2YmVjMjZlODNmNjIwNzAzYzg1MDViYmZmOSIsIm5pIjpbIjY0MjRlMmRjZTI1MWQ3NmIzMTEzZGZhNWE0YjdkMmQyIiwiM2M3ZjA4ZDk4ZDI4YTExMDA4MTkxMGNlNTViNWU5ODQiXSwidXUiOiJiODdhNzEzZDAyYzBhOTVjMDZjNmNmMGRkNjA1ZDIzNCJ9
```

解码后得到如下 JSON 字符串：

```json
{
    "bi": "3dad02e1538575a83b3844d29d3ce1ce",
    "bb": "6b6f7ddf8683c3f42b601e9304aa6ba7",
    "sm": "e7c326b35ab57e7ffb4f644db12be14e",
    "ma": "b67134cf7446ae892b5b35e13ae8b460",
    "mo": "a802686bec26e83f620703c8505bbff9",
    "ni": [
        "6424e2dce251d76b3113dfa5a4b7d2d2",
        "3c7f08d98d28a110081910ce55b5e984"
    ],
    "uu": "b87a713d02c0a95c06c6cf0dd605d234"
}
```

JSON 字符串中字母全为小写，每一个字段均为某一硬件特征字符串的 MD5 值。在计算该 MD5 值之前，需要将特征字符串转换为小写。

## 特征字符串

在此以 Windows 系统为例，说明各字段特征字符串的意义及简单获取方法。

### bi —— BIOS 序列号

在命令提示符中，使用以下命令获取 BIOS 序列号：

```
wmic bios get serialnumber
```

下面为上述命令的输出示例：

```
SerialNumber
AAA88B2
```

则“`AAA88B2`”即为 BIOS 序列号，转换为小写后（“`aaa88b2`”），计算 MD5 值得到`3dad02e1538575a83b3844d29d3ce1ce`。其它字段的计算方法与此相同，不再重复，后面仅列出获取特征字符串的命令行。

### bb —— 主板序列号

```
wmic baseboard get serialnumber
```

### sm —— SMBIOS 序列号

```
wmic csproduct get identifyingnumber
```

### ma —— 计算机生产厂商

```
wmic computersystem get manufacturer
```

### mo —— 计算机型号

```
wmic computersystem get model
```

### ni —— 全部物理网卡 MAC 地址列表

```
wmic nic where "PNPDeviceID like 'PCI\\%'" get macaddress
```

### uu —— SMBIOS UUID

```
wmic csproduct get uuid
```
