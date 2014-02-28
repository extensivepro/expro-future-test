# 统计信息 statistics

## 查询销售统计信息
### 请求
### GET /statistics

#### QueryString
* `taget` - 统计标的：`bills`销售金额（含储值，默认项目）, `deals`销售数量, `returns`退货数量, `skus`出入库。选填项目
* `period` - 统计周期单位: `daily`，`weekly`，`monthly`，必须提交项目
* `keyID` - 统计对象ID可以是: `employeID`, `shopID`, `merchantID`, 必须提交项目。keyID可以是shopID数组、agentID数组、merchantID数组（ angular里keyID数组在querystring中的呈现形式：keyID=6d97c241f56a8873&keyID=e20dccdf039b3874）。
* `end` - 查询的截止的时间，单位为距离1970年1月1日的天数、周数、月数，必须提交。；示例：?end=16093，查2014-01-23的日报
* `start` - 查询开始的时间，单位为距离1970年1月1日的天数、周数、月数，可选项目。默认是`end`的前7个单位
* `limit` - 查询单位数量的长度，默认是7；示例：?limit=20 返回20个单位的记录
* `itemID` - 统计对象的中商品的ID，可选提交。销售额中没有`itemID`。
* `type` - 统计对象的类型，可选提交。根据统计标的的不同`type`的值也不同，例如在`skus`中是`add`进货、`sub`核销。



## 返回
### 200 - OK

#### 月销售额 - bills
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

##### 备注
* 周销售额、日销售额参考月销售额
* `id` - 可以忽略
* `value.keyID` - 请求的对象ID
* `value.statAt` - 统计时间单位数量， 全部是距离1970年1月1日以来，数量 月报为月数，周报为周数，日报为天数
* `value.prepay` - 储值金额与次数
* `value.return` - 退货额与次数
* `value.sale` - 销售额与成交次数

#### 月出入库 - skus
```json
[
  {
    "_id": "e20dccdf039b3874#529#fbaf036bec45b8b0#add",
    "value": {
      "quantity": 2,
      "sumPrice": 1200,
      "count": 1,
      "keyID": "e20dccdf039b3874",
      "statAt": 529,
      "itemID": "fbaf036bec45b8b0",
      "type": "add"
    }
  },
  {
    "_id": "f0b780c8af555948#527#d944090ae1673961#add",
    "value": {
      "quantity": 1,
      "sumPrice": 1000,
      "count": 1,
      "keyID": "f0b780c8af555948",
      "statAt": 527,
      "itemID": "d944090ae1673961",
      "type": "sub"
    }
  }
]
```

##### 备注
* 周出入库、日出入库参考月出入库
* `_id` - 可以忽略
* `value.keyID` - 请求的对象ID
* `value.statAt` - 统计时间单位数量， 全部是距离1970年1月1日以来，数量 月报为月数，周报为周数，日报为天数
* `value.item` - 出入库商品的ID。
* `value.type` - 操作类型，例如`进货`、`核销`。

#### 月单品销售量 - deals
```json
[
  {
    "_id": "e20dccdf039b3874#529#fbaf036bec45b8b0",
    "value": {
      "quantity": 2,
      "sumPrice": 1240,
      "count": 2,
      "keyID": "e20dccdf039b3874",
      "statAt": 529,
      "itemID": "fbaf036bec45b8b0"
    }
  },
  {
    "_id": "ec2f3518057929c8#528#localID.initialItem2",
    "value": {
      "quantity": 1,
      "sumPrice": 450000,
      "count": 1,
      "keyID": "ec2f3518057929c8",
      "statAt": 528,
      "itemID": "localID.initialItem2"
    }
  }
]
```
##### 备注
* 周单品销售量、日单品销售量参考月单品销售量
* `_id` - 可以忽略
* `value.keyID` - 请求的对象ID
* `value.statAt` - 统计时间单位数量， 全部是距离1970年1月1日以来，数量 月报为月数，周报为周数，日报为天数
* `value.item` - 销售商品的ID。

#### 月单品退货量 - returns

```json
[
  {
    "_id": "e20dccdf039b3874#528#55FCB538-C110-4E96-97CF-B54A89A5F57D",
    "value": {
      "quantity": 1,
      "sumPrice": 520,
      "count": 1,
      "keyID": "e20dccdf039b3874",
      "statAt": 528,
      "itemID": "55FCB538-C110-4E96-97CF-B54A89A5F57D"
    }
  },
  {
    "_id": "e20dccdf039b3874#529#5FBFF931-F253-4AAD-807B-B7614CE816E7",
    "value": {
      "quantity": 1,
      "sumPrice": 800,
      "count": 1,
      "keyID": "e20dccdf039b3874",
      "statAt": 529,
      "itemID": "5FBFF931-F253-4AAD-807B-B7614CE816E7"
    }
  }
]
```
##### 备注
* 周单品退货量、日单品退货量参考月单品退货量
* `_id` - 可以忽略
* `value.keyID` - 请求的对象ID
* `value.statAt` - 统计时间单位数量， 全部是距离1970年1月1日以来，数量 月报为月数，周报为周数，日报为天数
* `value.item` - 退货商品的ID。
