# 店铺：shops
***

## 业主开店
## 请求
### POST /shops
```json
{
  "code": "010",
  "name": "华仔4号店",
  "address": "江宁区胜太路44号",
  "telephone": "02544444444",
  "merchantID": "154d4534a48e475",
  "status": "open",
  "openRes": [
    {
      "name": "桌子",
      "type": "table",
      "serviceability": 1,
      "code": "16",
      "codename": "桌号",
      "sceneID": 1016
    }
  ],
  "location": {
    "latitude": 23.137466,
    "longitude": 113.352425,
    "precision": 119.38504
  },
  "createdAt": 1364967296480
}
```
### 必要项目
* `code`
* `name`
* `merchantID`
* `createdAt`

### 默认项目
* `status` - "open" 。(共4种状态`open`, `suspend`, `closed`, `removed`)

### 备注
* `code` - 商户内唯一

## 响应
### `201` - 添加成功(目前：200)
```json
{
  "id": "154d4534a48e475",
  "code": "010",
  "name": "华仔4号店",
  "address": "江宁区胜太路44号",
  "telephone": "02544444444",
  "merchantID": "154d4534a48e475",
  "status": "open",
  "openRes": [
    {
      "name": "桌子",
      "type": "table",
      "serviceability": 1,
      "code": "16",
      "codename": "桌号"
    }
  ],
  "location": {
    "latitude": 23.137466,
    "longitude": 113.352425,
    "precision": 119.38504
  },
  "createdAt": 1364967296480,
  "closedAt":
}
```
### `400` - 请求参数错误
### `401` - 权限不够
### `409` - 请求冲突(目前：400)
***

## 业主查询店铺信息
## 请求
### GET /shops
### 查询条件
* `code` - 商店编码；示例：?code=010
* `name` - 店铺名称；示例：?name=华仔4号店
* `createdAt` - 开店时间；示例：?{"createdAt":{"$gt":1000}}
* `closedAt` - 关店时间：示例：?{"closedAt":{"$gt":1000}}
* `status` - 店铺状态；示例：?status=closed
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20

### 默认项目
* `skip` - 0
* `limit` - 20

## 响应
### `200` - 成功返回
```json
[{
  "id": "154d4534a48e475",
  "code": "010",
  "name": "华仔4号店",
  "address": "江宁区胜太路44号",
  "telephone": "02544444444",
  "merchantID": "154d4534a48e475",
  "status": "open",
  "openRes": [
    {
      "name": "桌子",
      "type": "table",
      "serviceability": 1,
      "code": "16",
      "codename": "桌号"
    }
  ],
  "location": {
    "latitude": 23.137466,
    "longitude": 113.352425,
    "precision": 119.38504
  },
  "createdAt": 1364967296480,
  "closedAt": 
}]
```
### `204` - 无内容(目前：200)
### `304` - not modified(目前：200)
### `400` - 请求参数错误
### `401` - 权限不够
### `409` - 请求冲突(目前：400)
***

## 业主更新店铺信息
## 请求
### PUT /shops/:id
```json
{
  "name": "华仔4号店",
  "address": "江宁区胜太路44号",
  "telephone": "02544444444",
  "status": "open",
  "openRes": [
    {
      "name": "桌子",
      "type": "table",
      "serviceability": 1,
      "code": "16",
      "codename": "桌号"
    }
  ],
  "location": {
    "latitude": 23.137466,
    "longitude": 113.352425,
    "precision": 119.38504
  }
}
```
## 备注
* `code` - 不能更改
* `merchantID` - 不能更改
* `createdAt` - 不能更改
* `closeAt` - 不能直接更改(关店时，服务端自动更新)

## 响应
### `200` - 更新成功
### `400` - 请求参数错误
### `401` - 权限不够
### `409` - 请求冲突(目前：400)
***

## 业主关店
## 请求
### PUT /shops/:id
```json
{
  "status": "closed"
}
```
### 必要项目
* `status`

## 响应
### `200` - 更新成功
### `400` - 请求参数错误
### `401` - 权限不够
### `409` - 请求冲突(目前：400)

## 打印机管理
## 请求
### PUT /shops/:id
```json
{
  "printers": {$push:"000000007985f65b"}
}
```

## 响应
### `200` - 更新成功
### `400` - 请求参数错误
### `401` - 权限不够

