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


## 订单付款
### 请求
### PUT /orders/:id
```
{
  "payment": {
    "type": 'alipay',
    "status": 'paid'
  }
}
```

#### 备注
* `sequenceNumber` - 订单号也做流水号，在更新订单付款状态前需要通关过sequenceNumber查询出具体的订单id
* `payment.status` - 为`paid`时，后台需根据order产生deal
* `payment.type` - 付款方式
  * `weixin` - 微信支付
  * `alipay` - 支付宝支付
  * `cash` - 现金支付
  * `prepay` - 储值支付

### 响应
```
{
  "agent": {
    "id": "6d97c241f56a8873",
    "name": "泛盈微信订餐"
  },
  "createdAt": 1387529885,
  "customer": {
    "account": {
      "balance": 20000,
      "updateAt": 1393210578.764,
      "id": "e55825da3bd8d8c3"
    },
    "code": "100001",
    "createdAt": -57261283574,
    "dueAt": 1403106826,
    "email": "caocao@fankahui.com",
    "level": "会员",
    "merchant": {
      "merchantID": "c82e1197884d8806",
      "name": "泛盈科技",
      "fullName": "泛盈信息科技有限公司"
    },
    "name": "曹操",
    "phone": "18912345678",
    "point": 0,
    "postPoint": 5000,
    "postTotalPoint": 10000,
    "registerShopID": "903d6f6ce857a9eb",
    "shop": {},
    "sinceAt": 1371570826,
    "status": "active",
    "weixin": {
      "openID": "o6_bmjrPTlm6_3sgVt7hM77kkOPf08M",
      "nickname": "张三"
    },
    "updateAt": 1393210578.813,
    "id": "9a0714826e347a64"
  },
  "deal": {
    "id": "759abcac0d96292b",
    "bill": {
      "id": "4dab8987361ff9dc"
    }
  },
  "fee": 3620,
  "items": [
    {
      "item": {
        "id": "221f47e56134f82e",
        "name": "黑咖啡",
        "price": 1620
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1620,
      "quantity": 1
    },
    {
      "item": {
        "id": "221f47e56134f82f",
        "name": "牛奶",
        "price": 1000
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC89",
      "dealPrice": 1000,
      "quantity": 2
    }
  ],
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
  "payment": {
    "type": "alipay",
    "status": "paid"
  },
  "quantity": 3,
  "receipt": {
    "name": "顾客张三",
    "phone": "13987654321",
    "address": "未提供"
  },
  "sequenceNumber": 1402304633001,
  "shop": {
    "code": "10011",
    "createdAt": 1386235335,
    "location": {
      "latitude": 23.137466,
      "longitude": 113.352425,
      "precision": 119.38504
    },
    "merchantID": "c82e1197884d8806",
    "name": "总店",
    "telephone": "02558679066",
    "address": "江苏省南京市江宁开发区胜太路68号303",
    "openRes": [
      {
        "name": "桌子",
        "type": "table",
        "serviceability": 1,
        "code": "16",
        "codename": "桌号",
        "sceneID": 1016,
        "ticket": "gQGV7zoAAAAAAAAAASxodHRwOi8vd2VpeGluLnFxLmNvbS9xL3gwd1JpLVRsMzNlbWl4b0dfV0RlAAIE8FlnUwMEAAAAAA==",
        "originID": "gh_af0c5d6c7b60"
      },
      {
        "name": "桌子",
        "type": "table",
        "serviceability": 2,
        "code": "18",
        "codename": "桌号"
      }
    ],
    "printers": [
      "000000007985f65b"
    ],
    "status": "open",
    "updateAt": 1398058924.049,
    "id": "903d6f6ce857a9eb",
    "merchant": {
      "address": "jl",
      "createdAt": 1386235335,
      "email": "",
      "fullName": "泛盈信息科技有限公司",
      "name": "泛盈科技",
      "newestDeviceCode": 100001,
      "owner": {
        "name": "新业主",
        "displayName": "泛盈科技业主",
        "idcard": "432828198307052525",
        "phone": "18912345678",
        "email": "owner@fankahui.com",
        "male": true,
        "createdAt": 1386235335,
        "username": "18912345678",
        "roles": [
          "user"
        ],
        "id": "af968c00fcaf8b0a"
      },
      "shopIDs": [
        "903d6f6ce857a9eb"
      ],
      "pointRule": {
        "newMember": {
          "type": "fixed",
          "amount": "200"
        },
        "consumption": {
          "type": "ratio",
          "ratio": "1"
        },
        "referrer": {
          "type": "fixed",
          "amount": "300"
        }
      },
      "weixin": {
        "originID": "gh_af0c5d6c7b60",
        "devToken": {
          "appid": "wxdff210e6548a2eab",
          "secret": "66333b7b129109dc145d5b16330f1c9a"
        }
      },
      "status": "open",
      "telephone": "02586861234",
      "zip": "",
      "id": "c82e1197884d8806"
    },
    "sequenceNumber": 0
  },
  "status": "paid",
  "type": "deliver",
  "updateAt": 1402304635,
  "id": "e334b788339cf855"
}
```
