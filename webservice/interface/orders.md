# 订单：orders
***

* 订单不等同于交易单，其可以作为交易单的来源，多条订单可以汇总形成一条交易单。
* 适用于交易环节持续时间较长的业态，例如餐饮服务业等。


订单状态|顾客|方向|门店|备注  
:--|:--:|:--:|--:|:--:  
placed|已下单|---->||  
accepted||<----|已接受|  
rejected||<----|已拒绝|  
executed|已签到|<--->|已出品|顾客可以签到触发打印出品单，也可以由商户手动打印出品单。  
canceled|已取消|---->||  
paid|已支付|---->||商户打印结算单，并新增一笔交易  

订单类型|说明|备注
-----|-----|----     
booking|预订|下单后需要顾客签到才会自动打印出品单，商户也可以手动走单    
deliver|外送|下单后直接进入到executed打印出品单

结算项目|说明
-----|-----    
类型| cash、weixin    
状态| paid、unpaid 

***
## 提交订单
### 请求
### POST /orders
```json
{
  "createdAt": 1387529885,
  "updateAt": 1387529885,
  "status": "placed",
  "payment": {
    "type": "weixin",
    "status": "unpaid"
  },
  "memo": [
    {
      "name": "门店",
      "createdAt": 1387529885
    },
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    }
  ],
  "type": "booking",
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1620
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1620,
      "quantity": 1
    },
    {
      "item": {
        "id": "221f47e56134f82d",
        "name": "拉面",
        "price": 1000
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC89",
      "dealPrice": 1000,
      "quantity": 2
    }
  ],
  "customer": {
    "id": "6d97c241f56a8873",
    "name": "顾客张三",
    "phone": "18912345678",
    "merchants": [
      {
        "merchantID": "e20dccdf039b3874",
        "memberID": "087442b616a1e8dc",
        "merchantName": "泛盈科技",
        "balance": 40,
        "point": 0,
        "level": "会员"
      }
    ]
  },
  "openRes": {
    "code": "16"
  },
  "agent": {
    "id": "6d97c241f56a8873",
    "name": "泛盈微信订餐"
  },
  "shop": {
    "id": "903d6f6ce857a9eb",
    "name": "泛盈总店",
    "address": "胜太路68号3层",
    "phone": "025-58679066"
  }
}
```

### 响应
#### 200 - 成功
```json
{
  "id": "2834910281d26a76",
  "createdAt": 1387529885,
  "updateAt": 1387529885,
  "status": "placed",
  "payment": {
    "type": "weixin",
    "status": "unpaid"
  },
  "memo": [
    {
      "name": "门店",
      "createdAt": 1387529885
    },
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    }
  ],
  "type": "booking",
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1620
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1620,
      "quantity": 1
    },
    {
      "item": {
        "id": "221f47e56134f82d",
        "name": "拉面",
        "price": 1000
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC89",
      "dealPrice": 1000,
      "quantity": 2
    }
  ],
  "customer": {
    "id": "6d97c241f56a8873",
    "name": "顾客张三",
    "phone": "18912345678",
    "merchants": [
      {
        "merchantID": "e20dccdf039b3874",
        "memberID": "087442b616a1e8dc",
        "merchantName": "泛盈科技",
        "balance": 40,
        "point": 0,
        "level": "会员"
      }
    ]
  },
  "openRes": {
    "code": "16"
  },
  "agent": {
    "id": "6d97c241f56a8873",
    "name": "泛盈微信订餐"
  },
  "shop": {
    "id": "903d6f6ce857a9eb",
    "name": "泛盈总店",
    "address": "胜太路68号3层",
    "phone": "025-58679066"
  }
}
```
##### 备注
* `status` - 订单状态

* `type` - 订单类型

* 当`payment`为

```
type: 'prepay',
status: 'paid'
```

且`status`为`paid`时，则为一次储值交易，后台需根据order产生deal

#### 400 - 参数错误
#### 401 - 未登录
#### 403 - 权限错误


## 查询订单
### 请求
### GET /orders
#### 查询条件

#### 默认项目

### 响应
#### 200 - 成功
```json
{
  "id": "2834910281d26a76",
  "createdAt": 1387529885,
  "updateAt": 1387529885,
  "status": "placed",
  "memo": [
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    }
  ],
  "type": "booking",
  "fee": 1600,
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1600
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1600,
      "quantity": 1
    }
  ],
  "quantity": 1,
  "sequenceNumber": 1,
  "customer": {
    "id": "6d97c241f56a8873",
    "name": "顾客张三",
    "address": "江宁区胜太路68号408"
  },
  "agent": {
    "id": "6d97c241f56a8873",
    "name": "泛盈微信订餐"
  },
  "shop": {
    "id": "2834910281d26a76",
    "name": "泛盈总店",
    "address": "胜太路68号3层",
    "phone": "025-58679066"
  }
}
```

#### 400 - 参数错误
#### 401 - 未登录
#### 403 - 权限错误

## 更新订单
### 请求
### PUT /orders/:id
```json
{
  "status": "accepted",
  "memo": [
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    }
  ],
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1600
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1600,
      "quantity": 1
    }
  ]
}
```

### 响应
#### 200 - 成功
```json
{
  "id": "2834910281d26a76",
  "createdAt": 1387529885,
  "updateAt": 1387529885,
  "status": "accepted",
  "memo": [
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    },
    {
      "name": "泛盈总店",
      "createdAt": 1387529885,
      "message": ""
    }
  ],
  "type": "booking",
  "fee": 1600,
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1600
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1600,
      "quantity": 1
    }
  ],
  "quantity": 1,
  "sequenceNumber": 1,
  "customer": {
    "id": "6d97c241f56a8873",
    "name": "顾客张三",
    "address": "江宁区胜太路68号408"
  },
  "agent": {
    "id": "6d97c241f56a8873",
    "name": "泛盈微信订餐"
  },
  "shop": {
    "id": "2834910281d26a76",
    "name": "泛盈总店",
    "address": "胜太路68号3层",
    "phone": "025-58679066"
  }
}
```

#### 400 - 参数错误
#### 401 - 未登录
#### 403 - 权限错误
