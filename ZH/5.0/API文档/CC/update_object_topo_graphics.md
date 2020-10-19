
### 请求地址

/api/c/compapi/v2/cc/update_object_topo_graphics/



### 请求方法

POST


### 功能描述

更新拓扑图

### 请求参数


#### 通用参数

| 字段 | 类型 | 必选 | 描述 |
|-----------|------------|--------|------------|
| bk_app_code  | string    | 是 | 应用 ID     |
| bk_app_secret| string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用ID -&gt; 基本信息 获取 |
| bk_token     | string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  | string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |

#### 接口参数

| 字段      | 类型      | 必选   | 描述      |
|-----------|------------|--------|------------|
| bk_supplier_account | string     | 否     | 开发商账号 |
| scope_type          | string    | 是     | 图形范围类型,可选 global,biz,cls(当前只有 global) |
| scope_id            | string    | 是     | 图形范围类型下的 ID,如果为 global,则填 0   |
| action              | string    | 是     | 更新方法,可选 update,override   |
| data                | list      | 否     | 更新数据   |

#### data

| 字段      | 类型      | 必选   | 描述      |
|-----------|------------|--------|------------|
| node_type   | string | 是 | 节点类型,可选 obj,inst |
| bk_obj_id   | string | 是 | 对象模型的 ID |
| bk_inst_id  | int    | 是 | 实例 ID |
| position    | dict   | 否 | 节点在图中的位置 |
| ext         | dict   | 否 | 前端扩展字段 |
| bk_obj_icon | string | 否 | 对象模型的图标 |


**注意**：

- scope_type,scope_id 唯一确定一张图

- node_type,bk_obj_id,bk_inst_id 三者唯一确定每张图的一个节点，故必填

### 请求参数示例

```json
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_supplier_account": "123456789",
    "scope_type": "global",
    "scope_id": 0,
    "action": "update",
    "data": [
        {
            "node_type": "obj",
            "bk_obj_id": "switch",
            "bk_inst_id": 0,
            "position": {
                "x": 100,
                "y": 100
            },
            "ext": {},
            "bk_obj_icon": "icon-cc-switch2"
        }
    ]
}
```

### 返回结果示例

```json
{
    "result": true,
    "code": 0,
    "message": "success",
    "data": "success"
}
```

### 返回结果参数说明

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| result    | bool      | 请求成功与否，true:请求成功，false:请求失败 |
| code      | string    | 组件返回错误编码，0 表示success，>0 表示失败错误 |
| message   | string    | 请求失败返回的错误消息 |
| data      | object    | 请求返回的数据 |
