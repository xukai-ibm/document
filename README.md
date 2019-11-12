# data-manager-server 接口文档

## data 接口

- 接口形式为HTTP

### 新增或者更新 updateData

#### 接口行为

- 会将以下属性相同的数据进行合并

  	"productLine"
  	"productNumber"
  	"product"
  	"project"

例如：

```
# 第一次数据
{
	"productLine": "12",
	"productNumber": "2",
	"product": "3",
	"project": "4",
	"metadata": {
		"c": 1,
		"v": {
			"e":"f"
		}
	}
}

# 第二次数据
{
	"productLine": "12",
	"productNumber": "2",
	"product": "3",
	"project": "4",
	"metadata": {
		"a": "bbbb",
		"b": {
			"t":111
		}
	}
}

# 数据中合并的数据
{
    "productLine": "12",
    "productNumber": "2",
    "product": "3",
    "project": "4",
    "metadata": {
        "c": 1,
        "v": {
            "e": "f"
        },
        "a": "bbbb",
        "b": {
            "t": 111
        }
    }
}
```



#### 接口类型

- HTTP  POST

#### 请求参数

- 无

#### 请求body

- json格式

```
{
	"productLine": "1",
	"productNumber": "2",
	"product": "3",
	"project": "4",
	"metadata": {
		"c": 1,
		"v": {
			"e":"f"
		}
	}
}
```

| 字段          | 类型   | 是否必须 | 说明     |
| ------------- | ------ | -------- | -------- |
| productLine   | string | 是       | 批号     |
| productNumber | string | 否       | 批号     |
| product       | string | 否       | 备注信息 |
| project       | string | 否       | 备注信息 |
| metadata      | object | 否       | 元数据   |




#### 请求头

- 无

#### 响应头

- 无

#### 返回值

- 返回数据格式为json
- 具体格式规范见 gateway api 规范

```
// success
{
    "status_code": "200",
    "status_message": "success"
}
// failed
{
    "status_code": "400",
    "status_message": "no access right"
}
```



### 流数据上传 streamData

#### 接口行为

- 数据会被传递到kafka 中

#### 接口类型

- HTTP  POST

- #### 请求参数

  - 无

  #### 请求body

  - json格式

  ```
  {
  	"productLine": "1",
  	"productNumber": "2",
  	"product": "3",
  	"project": "4",
  	"metadata": {
  		"c": 1,
  		"v": {
  			"e":"f"
  		}
  	}
  }
  ```

  | 字段          | 类型   | 是否必须 | 说明     |
  | ------------- | ------ | -------- | -------- |
  | productLine   | string | 是       | 产线     |
  | productNumber | string | 否       | 批号     |
  | product       | string | 否       | 产品     |
  | project       | string | 否       | 所属计划 |
  | metadata      | object | 否       | 元数据   |

#### 返回值

- 返回数据格式为json
- 具体格式规范见 gateway api 规范

```
// success
{
    "status_code": "200",
    "status_message": "success",
}
// failed
{
    "status_code": "400",
    "status_message": "no access right"
}

```



### 查询 searchData

#### 接口类型

- HTTP  Get

#### 请求参数

| 字段          | 是否必须 | 说明                    |
| ------------- | -------- | ----------------------- |
| productLine   | 否       | 群组名                  |
| productNumber | 否       | 群组类型                |
| product       | 否       | 默认值为0，用于分页查询 |
| project       | 否       | 所属计划                |

#### 请求头

- 无

#### 响应头

- 无

#### 返回值

- 返回数据格式为json
- 具体格式规范见 gateway api 规范，以下仅举例

```
// success
{
    "status": 200,
    "message": "success",
    "payload": [
        {
            "productLine": "1",
            "productNumber": "2",
            "product": "3",
            "project": "4",
            "metadata": {
                "a": 1,
                "b": {
                    "e": "f"
                },
                "c": 1,
                "d": {
                    "e": "f"
                },
                "v": {
                    "e": "f"
                }
            }
        }
    ]
}
// failed
{
    "status_code": "400",
    "status_message": "no access right"
}

```
