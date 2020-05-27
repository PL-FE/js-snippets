# js snippets
> 一些 js 片段，可能是常见的，可能是有用的，更可能还是乱七八糟的 😢

### Sort by array 
一个对象数组按照另一个对象数组进行自身排序
```js
const target = [{id: 1},{id: 2},{id: 3}, {id: 4}]
const source = [{id: 2},{id: 4},{id: 1}, {id: 3}]

const targetArr = target.map(it => it.id)
source.sort((a,b)=>{
    return targetArr.indexOf(a.id) - targetArr.indexOf(b.id)
})
// source: [{id: 2},{id: 4},{id: 1}, {id: 3}] => [ { id: 1 }, { id: 2 }, { id: 3 }, { id: 4 } ]
```

### Array complementing 
两个数组之间的补集
```js
const source1 = [1,2,3,4]
const source2 = [2,3,4,5]

const sA = new Set(source1), sB = new Set(source2);
const res = [...source1.filter(x => !sB.has(x)), ...source2.filter(x => !sA.has(x))]

// [1,2,3,4], [2,3,4,5] => [1,5]
```