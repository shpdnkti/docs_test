### 请求地址

/api/c/compapi/v2/cc/clone_host_property/

### 请求方法

POST

### 功能描述

克隆主机属性

### 请求参数

#### 通用参数

| 字段 | 类型 | 必选 | 描述 |
|-----------|------------|--------|------------|
| bk_app_code | string | 是 | 应用 ID |
| bk_app_secret| string | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用 ID -&gt; 基本信息 获取 |
| bk_token | string | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username | string | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |

#### 接口参数

| 字段 | 类型 | 必选 | 描述 |
|-------------|---------|--------|-----------------------------|
| bk_org_ip | string | 是 | 源主机 ip, 只支持传入单 ip |
| bk_dst_ip | string | 是 | 目标主机 ip, 多个 ip 用","分割 |
| bk_biz_id | int | 是 | 业务 ID |
| bk_cloud_id | int | 否 | 云区域 ID |

### 请求参数示例

```json
{
    "bk_biz_id":2,
    "bk_org_ip":"127.0.0.1",
    "bk_dst_ip":"127.0.0.2",
    "bk_cloud_id":0
}
```

### 返回结果示例

```json
{
    "result": true,
    "code": 0,
    "message": "",
    "data": null
}
```

### 返回结果参数说明

| 字段 | 类型 | 描述 |
|-----------|-----------|-----------|
| result | bool | 请求成功与否，true:请求成功，false:请求失败 |
| code | string | 组件返回错误编码 |
| message | string | 请求失败返回的错误消息 |
| data | object | 请求成功返回的数据 |
