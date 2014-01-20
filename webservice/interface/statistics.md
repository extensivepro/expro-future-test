# 统计信息 statistics

## 查询销售统计信息
### 请求
### GET /statistics

#### QueryString
* `period` - 统计周期单位: `daily`，`weekly`，`monthly`
* `keyID` - 统计对象ID可以是: `employeID`, `shopID`, `merchantID`
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20

## 返回
### 200 - OK

#### 月销售
```json
[
    {
        "id": "6d97c241f56a8873#1970-1", 
        "value": {
            "keyID": "6d97c241f56a8873", 
            "prepay": {
                "count": 0, 
                "total": 0
            }, 
            "return": {
                "count": 0, 
                "total": 0
            }, 
            "sale": {
                "count": 5, 
                "total": 1404850
            }, 
            "statAt": "1970-1"
        }
    }
]
```

#### 周销售
```json
[
  {
    "value": {
      "sale": {
        "total": 12765,
        "count": 14
      },
      "return": {
        "total": 0,
        "count": 0
      },
      "prepay": {
        "total": 0,
        "count": 0
      },
      "keyID": "6d97c241f56a8873",
      "statAt": "2297"
    },
    "id": "6d97c241f56a8873#2297"
  }
]
```

#### 日销售
```json
[
  {
    "value": {
      "sale": {
        "total": 11925,
        "count": 12
      },
      "return": {
        "total": 0,
        "count": 0
      },
      "prepay": {
        "total": 0,
        "count": 0
      },
      "keyID": "6d97c241f56a8873",
      "statAt": "1389628800000"
    },
    "id": "6d97c241f56a8873#1389628800000"
  }
]
```

#### 备注
`id` - 可以忽略
`value.keyID` - 请求的对象ID
`value.statAt` - 统计时间段， 月报为年-月，周边为周数自1970，日报为毫秒数自1970
`value.prepay` - 储值金额与次数
`value.return` - 退货额与次数
`value.sale` - 销售额与成交次数