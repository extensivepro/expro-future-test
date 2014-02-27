# 统计信息 statistics

## 查询销售统计信息
### 请求
### GET /statistics

#### QueryString
* `tagert` - 统计标的：`bills`销售金额（含储值，默认项目）, `deals`销售数量, `returns`退货数量, `skus`出入库。选填项目
* `period` - 统计周期单位: `daily`，`weekly`，`monthly`，必须提交项目
* `keyID` - 统计对象ID可以是: `employeID`, `shopID`, `merchantID`, `itemID`, 必须提交项目。keyID可以是shopID数组、agentID数组、merchantID数组（ angular里keyID数组在querystring中的呈现形式：keyID=6d97c241f56a8873&keyID=e20dccdf039b3874）。
* `end` - 查询的截止的时间，单位为距离1970年1月1日的天数、周数、月数，必须提交。；示例：?end=16093，查2014-01-23的日报
* `limit` - 查询单位数量的长度，默认是7；示例：?limit=20 返回20个单位的记录



## 返回
### 200 - OK

#### 月销售额
返回结果是一个数组，数组的每个元素都是一个对象，对象的key是querystring中的keyID,对象的value是一个数组，包含这个keyID查到的
所有销售统计数据。

```json
[
  {
    "value": {
      "sale": {
        "total": 0,
        "count": 0
      },
      "return": {
        "total": 0,
        "count": 0
      },
      "prepay": {
        "total": 120000,
        "count": 24
      },
      "keyID": "aa97c241f56a8873",
      "statAt": 16078
    },
    "id": "aa97c241f56a8873#16078"
  },
  {
    "value": {
      "sale": {
        "total": 0,
        "count": 0
      },
      "return": {
        "total": 0,
        "count": 0
      },
      "prepay": {
        "total": 120000,
        "count": 24
      },
      "keyID": "e234c241f56a8873",
      "statAt": 16078
    },
    "id": "e234c241f56a8873#16078"
  }
]
```


#### 周销售额
```json
参照月销售
```

#### 日销售额
```json
参照月销售
```

##### 备注
* `id` - 可以忽略
* `value.keyID` - 请求的对象ID
* `value.statAt` - 统计时间单位数量， 全部是距离1970年1月1日以来，数量 月报为月数，周报为周数，日报为天数
* `value.prepay` - 储值金额与次数
* `value.return` - 退货额与次数
* `value.sale` - 销售额与成交次数

#### 月出入库
```json
[
  {
    "_id": "fc2e4f3db2160a69#529",
    "value": {
      "keyID": "fc2e4f3db2160a69",
      "statAt": 529,
      "add": {
        "quantity": 100,
        "cost": 12000,
        "count": 1,
        "type": "add"
      },
      "sub": {
        "quantity": 0,
        "cost": 0,
        "count": 0,
        "type": "sub"
      }
    }
  },
  {
    "_id": "fda478b9f3cc7987#528",
    "value": {
      "keyID": "fda478b9f3cc7987",
      "statAt": 528,
      "add": {
        "quantity": 7,
        "cost": 1420,
        "count": 2,
        "type": "add"
      },
      "sub": {
        "quantity": 0,
        "cost": 0,
        "count": 0,
        "type": "sub"
      }
    }
  }
]
```

##### 备注
* 周出入库、日出入库参考月出入库
* `value.keyID` - 请求的对象ID
* `value.statAt` - 统计时间单位数量， 全部是距离1970年1月1日以来，数量 月报为月数，周报为周数，日报为天数
* `_id` - 可以忽略
* `value.add` - 进货操作
* `value.sub` - 核销操作