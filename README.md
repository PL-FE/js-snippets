# js snippets

> 记录日常使用到的 js 碎片

### Sort by array

一个对象数组按照另一个对象数组进行自身排序

```js
const target = [{ id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }]
const source = [{ id: 2 }, { id: 4 }, { id: 1 }, { id: 3 }]

const targetArr = target.map((it) => it.id)
source.sort((a, b) => {
  return targetArr.indexOf(a.id) - targetArr.indexOf(b.id)
})
// source: [{id: 2},{id: 4},{id: 1}, {id: 3}] => [ { id: 1 }, { id: 2 }, { id: 3 }, { id: 4 } ]
```

### Array complementing

两个数组之间的补集

```js
const source1 = [1, 2, 3, 4]
const source2 = [2, 3, 4, 5]

const sA = new Set(source1),
  sB = new Set(source2)
const res = [
  ...source1.filter((x) => !sB.has(x)),
  ...source2.filter((x) => !sA.has(x)),
]

// [1,2,3,4], [2,3,4,5] => [1,5]
```

### Decimal Rounding

小数取整

```js
const n = 2.4 | 0

// 2.4 | 0 => 2
```

### Date Range

日期区间

```js
// 今天
const start = new Date(new Date(new Date().toLocaleDateString()).getTime())
const end = new Date(
  new Date(new Date().toLocaleDateString()).getTime() + 24 * 60 * 60 * 1000 - 1
)

// Thu May 28 2020 00:00:00 GMT+0800 (中国标准时间)
// Thu May 28 2020 23:59:59 GMT+0800 (中国标准时间)
```

```js
// 本周
const start = new Date(new Date(new Date().toLocaleDateString()).getTime())
const end = new Date(
  new Date(new Date().toLocaleDateString()).getTime() + 24 * 60 * 60 * 1000 - 1
)
// 0 为 周日，此处直接设为 7 代表周日
let day = start.getDay() || 7
let noeDay = 3600 * 24 * 1000
let startWeek = new Date(start - (7 - day) * noeDay)
// 原式为 end + (7 - day) * noeDay，加法会自动被拼接字符串
let endWeek = new Date(end - (-7 + day) * noeDay)

// Mon May 25 2020 00:00:00 GMT+0800 (中国标准时间)
// Sun May 31 2020 23:59:59 GMT+0800 (中国标准时间)
```

```js
// 本月
const start = new Date(new Date(new Date().toLocaleDateString()).setDate(1))
const end = new Date(new Date(start).setMonth(start.getMonth() + 1) - 1)

// Fri May 01 2020 00:00:00 GMT+0800 (中国标准时间)
// Sun May 31 2020 23:59:59 GMT+0800 (中国标准时间)
```

### Scroll Position

获取当前页面的滚动位置

```js
const getScrollPosition = (el = window) => ({
  x: el.pageXOffset !== undefined ? el.pageXOffset : el.scrollLeft,
  y: el.pageYOffset !== undefined ? el.pageYOffset : el.scrollTop,
})

// 事例
getScrollPosition() // {x: 0, y: 200}
```

### deepFlatten

多维数组转换为一维

```js
const deepFlatten = (arr) =>
  [].concat(...arr.map((v) => (Array.isArray(v) ? deepFlatten(v) : v)))
// deepFlatten([1,[2],[[3],4],5]) -> [1,2,3,4,5]

// 当然 ES6 flat() 也很香
const deepFlatten = (arr) => arr.flat(Infinity)
```
