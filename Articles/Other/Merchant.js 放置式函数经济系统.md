# 💰Merchant.js💰 放置游戏函数式经济系统
## 简介
本文档是 Merchant.js 官方 README 的翻译。

Merchant.js（商人.js）是一个数值系统，用以创建和管理随时间变化的数字。

这套系统对放置游戏（增量游戏）最合适，但也可以用于其它游戏类型。

Merchant 很适合和 Redux 一起使用，但独立使用也可以。它使用函数式编程的，只返回数据副本而不直接修改数据状态。由于使用不可变数据的理念，它的大多数内容都会被存储为不可变对象。

坦率地讲，Merchant 只是一些功能的模式的集合，它相当简单，但能够在不牺牲效率的前提下对游戏的开发提供极大帮助。

## 安装
支持 yarn 和 npm 安装，前置 immutable 和 require.js
```bash
yarn add merchant.js
npm install --save merchant.js
```

## 系统
### 分类账 Ledgers，钱包 Wallet，货币 Currency
“货币”为一类资源的名称，最好写在单独的定义文件中以供查阅。
```javascript
const GOLD = "GOLD";
```

“分类账”是一个不可变的 Map 对象，键是“货币”，值是 Number 格式。

“钱包”为游戏中的“主分类账”，保存主状态。所有“分类账”都为“钱包”服务。
```javascript
const { Map } = require("immutable");
const ledger = Map({ GOLD: -5, SLIVER: 10 });
```

### 物品
“物品”指可购买项，它们可以作用于“钱包”内的数值状态。

“物品”通常为JSON格式，并需要写在包文件中。
```javascript
import { GOLD, POWER } from "./currencies";

export const MagicSword = {
	type: "MagicSword", // Must
	cost: () => { // Can
		return Map({ [GOLD]: -5 });
	},
	effect: (state) => { // Can
		return Map({ [POWER]: state.currentPowerLevel });
	}
}

// use state
const newWallet = buy(MagicSword, wallet, state);
const newLedger = effects(pouch, wallet, state);
```

cost 函数用于 buy 函数，确定物品购买成本，若要有“花费”，值应该是负数。

effect 函数用于 effects 函数，用于生成分类账。

这两个函数都可以接受“状态 State”，若想让成本随时间或购买数量而变化也可以很方便地进行设置。

物品可以作为一个货币放在钱包（Wallet）中。
```javascript
const wallet = Map({ GOLD:0, MagicSword:2 })
```

## 其它实用 Merchant 函数
```javsacript
import { sum, scale, inTheBlack, currencies, buy } from "merchant.js";
const ledger1 = Map({ GOLD: 2, SILVER: -10 });

// 成比例放缩
const ledger2 = scale(ledger1, 2);
ledger2.get(GOLD); // 4
ledger2.get(SILVER); // -20

// 合并，参数无上限
const wallet = sum(ledger1,ledger2);
wallet.get(GOLD); // 6 = 4 + 2

// 是否所有值都为正/负
intheBlack(wallet); // False
intheRed(Map({ GOLD: -2, SILVER: -10 })); // True

// 获取不重复键
const ledger4 = Map({ GOLD: 2, MAGIC_POWER: 1 });
currencies(wallet, ledger4); // ["GOLD", "SILVER", "MAGIC_POWER"]```

// “购买”物品，也可有 state 参数
wallet = buy(MagicSword, wallet, state);

// 返回给定多个分类帐的特定货币值，参数无上限
const cost1 = Map({ GOLD: 5, SILVER: -2, });
const cost2 = Map({ GOLD: 2 });
const goldCost = totalOf("GOLD", cost1, cost2); // 7

// 给出一系列物品，计算总价，没有官方示例
// allCosts()
// param: items(immutable.Map | Obj)
// param: state({})
// return: immutable.Map
```

## 源码
源码只有一个文件，复制即可，实际不必下载。
```javascript
const { Map, List } = require("immutable");
const invariant = require("invariant");
const { maybe, throwIfCostNotFunc, throwIfNotMap } = require("./util");

const sum = (...ledgers) => {
  if (!ledgers || ledgers.length === 0) {
    return Map({});
  }
  // Really simple check to make sure we're only using maps
  throwIfNotMap(ledgers[0], "add");

  if (ledgers.length === 1) {
    return ledgers[0];
  }

  return ledgers[0].mergeWith((one, two) => one + two, ...ledgers.slice(1));
};

const scale = (ledger, scale) => {
  throwIfNotMap(ledger, "scale");
  return ledger.map(x => x * scale);
};

const inTheBlack = ledger => {
  throwIfNotMap(ledger, "inTheBlack");
  return ledger.every(val => val >= 0);
};

const inTheRed = ledger => {
  throwIfNotMap(ledger, "inTheRed");
  return ledger.every(val => val < 0);
};

const currencies = (...ledgers) => {
  if (!ledgers || ledgers.length === 0) {
    return List();
  }
  throwIfNotMap(ledgers[0], "currencies");

  if (ledgers.length === 1) {
    return ledgers[0].keySeq().toList();
  }

  const mergedLedgers = ledgers[0].merge(...ledgers.slice(1));
  return mergedLedgers.keySeq().toList();
};

const totalOf = (currency, ...ledgers) => {
  if (!ledgers || ledgers.length === 0) {
    return 0;
  }
  throwIfNotMap(ledgers[0], "totalOf");

  return maybe(sum(...ledgers).get(currency), 0);
};

const cost = (item, state = {}) => {
  if (!item || !item.cost) {
    return Map();
  }
  throwIfCostNotFunc(item);
  return item.cost(state);
};

const allCosts = (items, state = {}) => {
  if (!Map.isMap(items) && typeof items === "object") {
    items = Map(items);
  }

  return items.map(item => {
    return cost(item, state);
  });
};

const buy = (item, wallet, state = {}) => {
  if (!item || !item.cost) {
    return wallet;
  }
  throwIfCostNotFunc(item);
  const cost = item.cost(state);
  // Check that the cost actually returns an immutable Map
  invariant(
    Map.isMap(cost),
    `The item of type: "${
      item.type
    }" returns something other than an Immutable.js Map.`
  );

  return sum(item.cost(state), wallet);
};

const add = (item, wallet, amount = 1) => {
  return sum(wallet, Map({ [item.type]: amount }));
};

const effects = (items, wallet, state = {}) => {
  const ledgers = items
    .map(item => {
      if (!item.effect) return;
      return scale(item.effect(state), maybe(wallet.get(item.type), 0));
    })
    .filter(n => n);
  return sum(...ledgers);
};

module.exports = {
  sum,scale,inTheBlack,
  inTheRed,currencies,
  totalOf,buy,add,
  effects,cost,allCosts
};
```