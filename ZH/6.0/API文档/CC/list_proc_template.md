
### 请求地址

/api/c/compapi/v2/cc/list_proc_template/



### 请求方法

POST


### 功能描述

根据服务模板ID查询进程模板信息

### 请求参数


#### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用ID -&gt; 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token与bk_username必须一个有效，bk_token可以通过Cookie获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |

#### 接口参数

| 字段                 |  类型      | 必选	   |  描述                 |
|----------------------|------------|--------|-----------------------|
| service_template_id | int  | 否   | 服务模板ID |


### 请求参数示例

```python

{
  "bk_biz_id": 1,
  "limit": {
    "start": 0,
    "limit": 1
  },
  "with_name": true,
  "bk_set_id": 15,
  "bk_module_id": 8,
  "bk_host_id": 11,
  "service_instance_ids": [49],
  "selectors": [{
    "key": "key1",
    "operator": "notin",
    "values": ["value1"]
  }]
}


```

### 返回结果示例

```python
{
    "result": true,
    "code": 0,
    "message": "success",
    "data": {
        "count": 1,
        "info": [
            {
                "id": 50,
                "bk_process_name": "p1",
                "bk_biz_id": 1,
                "service_template_id": 51,
                "property": {
                    "proc_num": {
                        "value": null,
                        "as_default_value": false
                    },
                    "stop_cmd": {
                        "value": "",
                        "as_default_value": false
                    },
                    "restart_cmd": {
                        "value": "",
                        "as_default_value": false
                    },
                    "face_stop_cmd": {
                        "value": "",
                        "as_default_value": false
                    },
                    "bk_func_name": {
                        "value": "p1",
                        "as_default_value": true
                    },
                    "work_path": {
                        "value": "",
                        "as_default_value": false
                    },
                    "priority": {
                        "value": null,
                        "as_default_value": false
                    },
                    "reload_cmd": {
                        "value": "",
                        "as_default_value": false
                    },
                    "bk_process_name": {
                        "value": "p1",
                        "as_default_value": true
                    },
                    "pid_file": {
                        "value": "",
                        "as_default_value": false
                    },
                    "auto_start": {
                        "value": false,
                        "as_default_value": false
                    },
                    "auto_time_gap": {
                        "value": null,
                        "as_default_value": false
                    },
                    "start_cmd": {
                        "value": "",
                        "as_default_value": false
                    },
                    "bk_func_id": {
                        "value": null,
                        "as_default_value": false
                    },
                    "user": {
                        "value": "",
                        "as_default_value": false
                    },
                    "timeout": {
                        "value": null,
                        "as_default_value": false
                    },
                    "description": {
                        "value": "",
                        "as_default_value": false
                    },
                    "bk_start_param_regex": {
                        "value": "",
                        "as_default_value": false
                    },
                    "bind_info": {
                        "value": [
                            {
                                "enable": {
                                    "value": false,
                                    "as_default_value": true
                                },
                                "ip": {
                                    "value": "1",
                                    "as_default_value": true
                                },
                                "port": {
                                    "value": "100",
                                    "as_default_value": true
                                },
                                "protocol": {
                                    "value": "1",
                                    "as_default_value": true
                                },
                                "row_id": 1
                            }
                        ],
                        "as_default_value": true
                    }
                },
                "creator": "admin",
                "modifier": "admin",
                "create_time": "2019-06-19T15:24:04.763+08:00",
                "last_time": "2019-06-19T15:24:04.763+08:00",
                "bk_supplier_account": "0"
            }
        ]
    }
}
```

### 返回结果参数说明

#### response

| 名称  | 类型  | 描述 |
|---|---|---|
| result | bool | 请求成功与否。true:请求成功；false请求失败 |
| code | int | 错误编码。 0表示success，>0表示失败错误 |
| message | string | 请求失败返回的错误信息 |
| data | object | 请求返回的数据 |

#### data 字段说明

| 字段|类型|说明|描述|
|---|---|---|---|
|count|integer|总数||
|info|array|返回结果||

#### info 字段说明

| 字段|类型|说明|Description|
|---|---|---|---|
|id|integer|进程模板ID||
|bk_process_name|string|进程模板名称||
|property|object|进程模板属性||

#### data.info[x].property.bind_info.value[n] 字段说明
| 字段|类型|说明|
|---|---|---|---|
|enable|object|端口是否启用||
|ip|object|绑定的ip||
|port|object|绑定的端口||
|protocol|object|使用的协议||
|row_id|int|模板行索引，进程内唯一|