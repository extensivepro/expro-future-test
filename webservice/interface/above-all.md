# expro-future 总体说明

## 依赖关系
* add-deal为添加交易接口，依赖的collection为deal,bill，相关数据存储在deal,bill中。
* add-return为添加退货接口，依赖的collection为return,bill，相关数据存储在return,bill中。
* bill同时作为充值接口存在。

## 备注
* internal api:仅针对deployd collection/resource间的内部访问，不对外开放(404)

## 目录
* [users](users.md)
* [members](members.md)
* [employes](employes.md)
* [merchants](merchants.md)
* [shops](shops.md)
* [items](items.md)
* [skus](skus.md)
* [deals](deals.md)
* [returns](returns.md)
* [bills](bills.md)
* [accounts](accounts.md)
* [add-deal](add-deal.md)
* [add-return](add-return.md)
* [inventories](inventories.md)
