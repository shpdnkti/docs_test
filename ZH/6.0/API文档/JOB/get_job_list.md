
### 请求地址

/api/c/compapi/v2/job/get_job_list/



### 请求方法

GET


### 功能描述

查询作业执行方案列表

### 请求参数


#### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用ID -&gt; 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token与bk_username必须一个有效，bk_token可以通过Cookie获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |

#### 接口参数

| 字段       |  类型      | 必选   |  描述      |
|----------------------|------------|--------|------------|
| bk_biz_id              |  long       | 是     | 业务ID |
| creator                |  string    | 否     | 作业执行方案创建人帐号 |
| name                   |  string    | 否     | 作业执行方案名称，模糊匹配 |
| create_time_start      |  string    | 否     | 创建起始时间，YYYY-MM-DD格式 |
| create_time_end        |  string    | 否     | 创建结束时间，YYYY-MM-DD格式 |
| last_modify_user       |  string    | 否     | 作业执行方案修改人帐号 |
| last_modify_time_start |  string    | 否     | 最后修改起始时间，YYYY-MM-DD格式 |
| last_modify_time_end   |  string    | 否     | 最后修改结束时间，YYYY-MM-DD格式 |
| start                  |  int       | 否     | 默认0表示从第1条记录开始返回 |
| length                 |  int       | 否     | 返回记录数量，不传此参数默认返回全部 |

### 请求参数示例

```python
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_biz_id": 1,
    "creator": "admin",
    "name": "test",
    "create_time_start": "2016-02-22",
    "create_time_end": "2016-02-22",
    "last_modify_user": "admin",
    "last_modify_time_start": "2016-02-22",
    "last_modify_time_end": "2016-02-22",
    "start": 0,
    "length": 100
}
```

### 返回结果示例

```python
{
    "result": true,
    "code": 0,
    "message": "success",
    "data": [
        {
            "bk_biz_id": 1,
            "bk_job_id": 100,
            "name": "test",
            "creator": "admin",
            "last_modify_user": "admin",
            "create_time": "2018-01-23 15:05:41 +0800",
            "last_modify_time": "2018-01-23 16:04:51 +0800"
        }
    ]
}
```

### 返回结果参数说明

#### data

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| bk_biz_id       | long       | 业务ID |
| bk_job_id       | long       | 作业执行方案ID |
| name            | string    | 作业执行方案名称 |
| creator         | string    | 创建人帐号 |
| create_time     | string    | 创建时间，YYYY-MM-DD HH:mm:ss格式 |
| last_modify_user| string    |修改人帐号 |
| last_modify_time| string    | 最后修改时间，YYYY-MM-DD HH:mm:ss格式 |