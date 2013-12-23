# 积分记录 points


## 添加积分记录
## 请求
### POST /points

```json
{
    "agentID": "c82e1197884d8806", 
    "createdAt": 1386235335, 
    "memberID": "903d6f6ce857a9eb", 
    "point": 100, 
    "postPoint": 2300, 
    "postTotalPoint": 12300, 
    "reason": "consumption reward"
}
```

#### 备注

## 响应
### 201 添加成功（目前为200）
```json
{
    "id": "32445a458b45e", 
    "agentID": "c82e1197884d8806", 
    "createdAt": 1386235335, 
    "memberID": "903d6f6ce857a9eb", 
    "point": 100, 
    "postPoint": 2300, 
    "postTotalPoint": 12300, 
    "reason": "consumption reward"
}
```

### 400 参数错误 Bad Request
* `createdAt` - `is required`
* `memberID` - `is required`
* `point` - `is required`
* `postPoint` - `is required`
* `postTotalPoint` - `is required`


### 401 未授权 Unauthorized
`Unauthorized` - `please login` 未授权，请登录

### 403 禁止访问 Forbidden
`Forbidden` - `disallow operation` 禁止访问

### 406 不可接受
* `memberID` - `bad member` 会员不存在
* `agentID` - `bad agent` 经办人不存在
* `point` - `point should not equal zero` 积分数量不能等于0
* `postPoint` - `postPoint should not greate postTotalPoint` 累积积分不能大于累计积分

## 查询积分记录
## 请求
### GET /points
#### Example
/points?agentID=c82e1197884d8806&memberID=903d6f6ce857a9eb

#### 备注
所有字段均支持查询条件，数字字段支持范围查询。

## 响应

### 200 OK
```json
[{
    "id": "32445a458b45e", 
    "agentID": "c82e1197884d8806", 
    "createdAt": 1386235335, 
    "memberID": "903d6f6ce857a9eb", 
    "point": 100, 
    "postPoint": 2300, 
    "postTotalPoint": 12300, 
    "reason": "consumption reward"
}]
```

### 400 参数错误 Bad Request
查询参数类型和方法的校验，详细参见请求。

### 401 未授权 Unauthorized
`Unauthorized` - `please login` 未授权，请登录

### 403 禁止访问 Forbidden
`Forbidden` - `disallow operation` 禁止访问
 
## 查询积分记录ByID
## 请求
### GET /points/:id
`:id` - 32445a458b45e 积分的ID

#### 备注

## 响应

### 200 OK
```json
{
    "id": "32445a458b45e", 
    "agentID": "c82e1197884d8806", 
    "createdAt": 1386235335, 
    "memberID": "903d6f6ce857a9eb", 
    "point": 100, 
    "postPoint": 2300, 
    "postTotalPoint": 12300, 
    "reason": "consumption reward"
}
```

### 401 未授权 Unauthorized
`Unauthorized` - `please login` 未授权，请登录

### 403 禁止访问 Forbidden
`Forbidden` - `disallow operation` 禁止访问