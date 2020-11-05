
### 请求地址

/api/c/compapi/v2/iam/authorization/instance/



### 请求方法

POST


### 功能描述

资源实例授权回收

### 请求参数


#### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用ID -&gt; 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token与bk_username必须一个有效，bk_token可以通过Cookie获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |

#### 接口参数

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| asynchronous |  布尔  | 是   | 是否异步调用, 默认 否, 当前只支持同步 |
| operate |  字符串   | 是   | grant或revoke |
| system |  字符串  | 是   | 系统id |
| action |  字符串   | 是   | 操作 |
| subject |  字符串   | 是   | 授权对象 |
| resources |  数组[对象]   | 是   | 资源实例 |

#### action

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| id    |  字符串  | 是   | 操作ID |

#### subject

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| type    |  字符串  | 是   | 授权对象类型, 当前只支持 user |
| id    |  字符串  | 是   | 授权对象ID |

#### resources

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| system |  字符串  | 是   | 资源系统ID |
| type |  字符串  | 是   | 资源类型ID |
| id | 字符串 | 是 | 资源实例ID |
| name | 字符串 | 是 | 资源实例名称 |

### 请求参数示例

```python
{
  "asynchronous": false,  # 默认false, 当前只支持同步
  "operate": "grant",   # grant 授权 revoke 回收
  "system": "bk_cmdb",
  "action": {
    "id": "edit_host"
  },
  "subject": {  # 当前只能对user授权
    "type": "user",
    "id": "admin"
  },
  "resources": [{  # 操作依赖多个资源类型的情况下, 表示一个组合资源
    "system": "bk_cmdb",
    "type": "host",
    "id": "host1",
    "name": "host1"
  }]
}
```

### 返回结果示例

```python
{
  "data": {
    "policy_id": 1,
    "expression": {
      "field": "host.id",
      "op": "in",
      "value": ["host1", "host2"]
    }
  },
  "result": true,
  "code": 0,
  "message": "OK"
}
```

### 返回结果参数说明

#### data

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| policy_id   | 数值     | 权限策略id |
| expression   | 对象     | 权限表达式 |