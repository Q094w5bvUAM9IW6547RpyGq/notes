## [Map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map)

> **`Map`** 对象保存键值对，并且能够记住键的原始插入顺序。任何值(对象或者[原始值](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive)) 都可以作为一个键或一个值。

### Map() [构造函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map/Map)

```
let myMap = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
])
```

```
let myMap = new Map();
myMap.set(NaN, "not a number");
myMap.get(NaN); // "not a number"
let otherNaN = Number("foo");
myMap.get(otherNaN); // "not a number"
```

