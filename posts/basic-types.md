# 基础类型

- 英文文档：[http://www.typescriptlang.org/docs/handbook/basic-types.html](http://www.typescriptlang.org/docs/handbook/basic-types.html)
- 中文文档：[https://www.tslang.cn/docs/handbook/basic-types.html](https://www.tslang.cn/docs/handbook/basic-types.html)

`基本类型`，如果你有 javascript 基础，可以扫一遍就过好了。

## 布尔值,数字，字符串，数组

```ts
let isDone: boolean = false
let num: number = 6
let str: string = "blue"
let list1: number[] = [1, 2, 3]
let list2: Array<number> = [1, 2, 3]
```

## 元祖

> 元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。 比如，你可以定义一对值分别为 `string`和`number`类型的元组。

```ts
// 声明一个元祖类型
let x: [string, number]
// 初始化
x = ["hello", 10] // OK
// 下面这种赋值就是错误的
x = [10, "hello"] // Error
```

当访问一个已知索引的元素，会得到正确的类型：

```ts
console.log(x[0].substr(1)) // OK
console.log(x[1].substr(1)) // Error, 'number' does not have 'substr'
```

当访问一个越界的元素，会使用联合类型替代：

```ts
x[3] = "world" // OK, 字符串可以赋值给(string | number)类型

console.log(x[5].toString()) // OK, 'string' 和 'number' 都有 toString

x[6] = true // Error, 布尔不是(string | number)类型
```

## 枚举

```ts
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green
```

手动指定元素编号：

```ts
enum Color {
  Red = 1,
  Green,
  Blue,
}
let c: Color = Color.Green
```

## Any

`any`, 当你使用 Any 的时候，其实和使用 js 没什么区别，表示可以为任意类型。

```ts
let list: any[] = [1, true, "free"]

list[1] = 100
```

## Viod

`void`, 一般用在函数没有返回值的时候，只可以给他赋值`undefined`或者`null`。

```ts
function warnUser(): void {
  console.log("This is my warning message")
}
```

## Null 和 Undefined

```ts
let u: undefined = undefined
let n: null = null
```

> 默认 Null 和 Undefined 是所有类型的子类型。当设置`--strictNullChecks`后，null 和 undefined 只能赋值给 void 和它们各自。

## Never

`never`类型是任何类型的子类型，也可以赋值给任何类型；然而，没有类型是`never`的子类型或可以赋值给`never`类型（除了`never`本身之外）。 即使 `any`也不可以赋值给`never`。

```ts
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
  throw new Error(message)
}

// 推断的返回值类型为never
function fail() {
  return error("Something failed")
}

// 返回never的函数必须存在无法达到的终点
function infiniteLoop(): never {
  while (true) {}
}
```

## Object

```ts
let o: Object = { name: "alfredo" }
let n: Object = null
```

## 类型断言

通过`类型断言`这种方式可以告诉编译器，“相信我，我知道自己在干什么”。

类型断言有两种形式。 其一是“尖括号”语法：

```ts
let someValue: any = "this is a string"

let strLength: number = (<string>someValue).length
```

另一个为`as`语法：

```ts
let someValue: any = "this is a string"

let strLength: number = (someValue as string).length
```
