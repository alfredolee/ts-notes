# 函数

- 英文文档：[http://www.typescriptlang.org/docs/handbook/functions.html](http://www.typescriptlang.org/docs/handbook/functions.html)
- 中文文档：[https://www.tslang.cn/docs/handbook/functions.html](https://www.tslang.cn/docs/handbook/functions.html)

```js
let myAdd = (x, y) => {
  return x + y
}
```

写成`完整函数类型`就称下面的样子, 当然你仍旧可以省略其中的一部分，ts 会自己推断类型：

```ts
let myAdd: (baseValue: number, increment: number) => number = (x: number, y: number): number => {
  return x + y
}
```

## 可选参数

```ts
function buildName(firstName: string, lastName?: string) {
  // ...
}
```

## 默认参数

```ts
function buildName(firstName = "alfredo", lastName: string) {
  // ...
}
```

## 剩余参数

```ts
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + " " + restOfName.join(" ")
}
```

## 重载

因为前两句话的重载，`pickCard`在调用的时候就会进行类型检查。

```ts
function pickCard(x: { suit: string; card: number }[]): number
function pickCard(x: number): { suit: string; card: number }
function pickCard(x): any {
  // Check to see if we're working with an object/array
  // if so, they gave us the deck and we'll pick the card
  if (typeof x == "object") {
    let pickedCard = Math.floor(Math.random() * x.length)
    return pickedCard
  }
  // Otherwise just let them pick the card
  else if (typeof x == "number") {
    let pickedSuit = Math.floor(x / 13)
    return { suit: suits[pickedSuit], card: x % 13 }
  }
}
```
