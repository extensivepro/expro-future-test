# 会员：members
***

## 雇员新增会员
## 请求
### POST /members
```json
{
  "name": "张三",
  "code": "23012584",
  "male": true,
  "phone": "15154588756",
  "email": "hello@qq.com",
  "idcard": "587452145874569852",
  "deliveryAddress": [
    {
      "address": "新街口2号",
      "recipient": "李四",
      "phone": "18912345678"
    }
  ],
  "userID": "2512a52c535e51",
  "shop": {
    "shopID": "251235a2c535e51"
  },
  "merchant": {
    "merchantID": "251235a2c535e51"
  },
  "sinceAt": 1366444157013,
  "dueAt": 1366444159013,
  "createdAt": 1366444157013
}
```
### 必要项目
* `code`
* `name`

~~* `phone` 或 `email` 两者至少有其一~~
* `merchant` -> `merchantID`
* `sinceAt`
* `dueAt`
* `createdAt`

### 默认项目
* `status` - `active`。(共4种状态：`active`, `suspend`, `expired`, `removed`)
* `level` - `"会员"`

### 备注
~~* 当`shop`信息不存在时，认为会员为商户级别会员~~
~~* 当`shop`信息存在时，认为会员为商店级别会员~~
* `point` - 初始值为： 0
* `createdAt`的时间格式一律为整型值的秒数
* `query.referrer` - 将推荐人的会员id放到querystring中，推荐人将获得推荐积分。 例如：?referre=abc123

## 响应
### `200` - 新增成功
```json
{
  "_id": "1a0714826e347a64",
  "name": "张飞",
  "code": "100002",
  "email": "caocao@fankahui.com",
  "phone": "18912345678",
  "idcard": "320103197912162012",
  "deliveryAddress": [
    {
      "address": "新街口2号",
      "recipient": "李四",
      "phone": "18912345678"
    }
  ],
  "merchant": {
    "merchantID": "c82e1197884d8806",
    "name": "泛盈科技",
    "fullName": "泛盈信息科技有限公司",
    "weixin": {
      "originID": "gh_af0c5d6c7b66"
    }
  },
  "postPoint": 5000,
  "postTotalPoint": 10000,
  "level": "会员",
  "status": "active",
  "sinceAt": 1371570826,
  "dueAt": 1403106826,
  "createdAt": 1371570826,
  "account": {
    "id": "e55825da3bd8d8c3",
    "name": "曹操",
    "balance": 10000
  },
  "registerShopID": "903d6f6ce857a9eb",
  "weixin": {
    "openID": "o6_bmjrPTlm6_3sgVt7hM77kkOPf08M"
  },
  "shop": {}
}
```
### `400` - 请求参数错误
~~### `401` - 权限不够~~
~~* 仅雇员有权限~~

### `409` - 请求冲突(暂时：400)
***

## 查询会员
## 请求
### GET /members
### 查询条件
* `name` - 会员姓名；示例：?name=张三
* `code` - 会员编码；示例：?code=23012584
* `email` - 会员email；示例：?email=hello@qq.com
* `phone` - 会员电话；示例：?phone=18925488965
* `point` - 会员积分；示例：?{"point":{"$lt":10025}}
* `level` - 会员等级；示例：?{"level":{"$lt":10}}
* `sinceAt` - 加入时间；示例：?{"sinceAt":{"$lt":1366445203233}}
* `dueAt` - 到期时间；示例：?{"dueAt":{"$lt":1366445203233}}
* `status` - 会员状态；示例：?status=active
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20
* `id` - 根据`id`进行查询；示例：/32445a458b45e
* `weixin.refresh_token` - 根据weixin的refresh_token查询；

#### 注：当用id查询时，得到的是单个json而非json数组，且查询不到时返回404

### 默认项目
* `skip` - 0
* `limit` - 10

## 响应
### `200` - 请求成功(`id`查询, 非`id`查询返回数组)
```json
{
  "id": "2512a52c535e51",
  "name": "张三",
  "code": "23012584",
  "male": true,
  "phone": "15154588756",
  "email": "hello@qq.com",
  "idcard": "587452145874569852",
  "deliveryAddress": [
    {
      "address": "新街口2号",
      "recipient": "李四",
      "phone": "18912345678"
    }
  ],
  "userID": "2512a52c535e51",
  "shop": {
    "shopID": "251235a2c535e51",
    "name": "北京烤鸭店江宁区分店",
    "address": "江宁区胜太路99号",
    "telephone": "02554785214"
  },
  "merchant": {
    "merchantID": "251235a2c535e51",
    "weixin":{
      "originID": "gh_af0c5d6c7b66"
    }
    "name": "烤鸭店",
    "fullName": "北京烤鸭店"
  },
  "postPoint": 0,
  "postTotalPoint": 0,
  "level": "会员",
  "status": "active",
  "sinceAt": 1366444157013,
  "dueAt": 1366444159013,
  "weixin": {
    "openID": "o6_bmjrPTlm6_3sgVt7hM77kkOPf08M"
  },
  "createdAt": 1366444157013
}
```
### `204` - 无内容(暂时：200)
### `304` - 未修改(暂时：200)
### `400` - 请求参数错误
### `401` - 权限不够
### `409` - 请求冲突(暂时：400)
***

## 微信OAuth获取会员信息
## 请求
### GET /wxoauth
### 查询条件
* `code` - 根据微信oauth的code查询会员信息；例如：?code=123
* `merchantID` - 商户ID，用来定位商户的appid和secret；

## 响应
参考[查询会员-响应](#%E5%93%8D%E5%BA%94-1)


## 更新会员信息
## 请求
### PUT /members/:id?weixin.refresh_token=abc123
```json
{
  "name": "张三",
  "male": true,
  "phone": "15154588756",
  "email": "hello@qq.com",
  "idcard": "587452145874569852",
  "level": "会员",
  "status": "active",
  "deliveryAddress": [
    {
      "address": "新街口2号",
      "recipient": "李四",
      "phone": "18912345678"
    }
  ],
  "sinceAt": 1366444157013,
  "dueAt": 1366444159013
}
```

#### 备注
* `postPoint` - 不可以由外部更新
* `postTotalPoint` - 不可以由外部更新
* `weixin.refresh_token` -  利用微信的token更新会员信息。

## 响应
### `200` - 更新成功
### `400` - 请求参数错误
### `401` - 权限不够

## 微信会员和现有会员关联
## 请求
### POST /wxoauth
```json
{
  "action": "pair",
  "member": {
    "id": "1a0714826e347a64",
    "merchant": {
      "merchantID": "c82e1197884d8806"
    },
    "weixin": {
      "openID": "o6_bmjrPTlm6_3sgVt7hM77kkOPf08M",
      "refresh_token": "OezXcEiiBSKSxW0eoylIeJrOiMurn_Wfi3OzbgXGwN3J9e7aTpRAEc8f4OshrEkh919Ci3FmQpb2k6Wb7GA5Iwt39OawW_x6HPRvqMLTRGuu5UiY8TRaS4OfYSwzmRDg8r1tThRHHYdIj2NwiDZwbg"
    }
  },
  "options": {
    "phone": "13357828347"
  }
}
```

## 响应
### `200` - 更新成功
### `400` - 请求参数错误
* action, `should have action`
* member, `should have member`
* member.id, `should have member id`
* member.weixin, `should have member with weixin`
* member.weixin.refresh_token, `should have member with weixin refresh token`
* member.merchant, `should have merchant`
* member.merchant.merchantID, `should have merchant id`
* options, `should have options`
* options.phone, `should have phone number`

### `401` - 权限不够
