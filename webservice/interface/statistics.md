# 统计信息 statistics

## 查询销售统计信息
### 请求
### GET /statistics

#### QueryString
* `period` - 统计周期单位: `daily`，`weekly`，`monthly`
* `keyID` - 统计对象ID可以是: `employeID`, `shopID`, `merchantID`
* `skip` - 查询起始位置跳过的单位个数，默认是0；示例：?skip=1，查月报的时候表示从上个月的前一个月开始查询
* `limit` - 查询单位数量的长度，默认是7；示例：?limit=20 返回20个单位的记录

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
            "statAt": "197001"
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
`value.statAt` - 统计时间单位数量， 全部是距离1970年1月1日以来，数量 月报为月数，周报为周数，日报为天数
`value.prepay` - 储值金额与次数
`value.return` - 退货额与次数
`value.sale` - 销售额与成交次数