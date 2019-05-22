# 接口

- 英文文档：[http://www.typescriptlang.org/docs/handbook/interfaces.html](http://www.typescriptlang.org/docs/handbook/interfaces.html)
- 中文文档：[https://www.tslang.cn/docs/handbook/interfaces.html](https://www.tslang.cn/docs/handbook/interfaces.html)

## 接口基本示例

```ts
interface User {
  name: string
  nickName?: string // 可选属性
  readonly age: number // 只读属性
  [propName: string]: any // 任意数量的属性
}

// 接口继承
interface Student extends User {
  number: number
}

function printUser(stu: Student): void {
  console.log(stu)
}

printUser({
  name: "alfredolee",
  age: 25,
  number: 1,
})
```

## 函数类型

`SearchFunc`定义了函数的签名类型和返回值类型，`mySearch`实现了这个接口。

```ts
interface SearchFunc {
  (source: string, subString: string): boolean
}

let mySearch: SearchFunc = function(source: string, subString: string) {
  let result = source.search(subString)
  return result > -1
}
```

> 函数的参数名不需要与接口里定义的名字相匹配。

## 可索引的类型

示例：

```ts
interface StringArray {
  [index: number]: string
}

let myArray: StringArray
myArray = ["Bob", "Fred"]

let myStr: string = myArray[0]
```

TypeScript 支持两种索引签名：`字符串`和`数字`。 可以同时使用两种类型的索引，但是`数字索引的返回值必须是字符串索引返回值类型的子类型`。 这是因为当使用 number 来索引时，JavaScript 会将它转换成 string 然后再去索引对象。 也就是说用 100（一个 number）去索引等同于使用"100"（一个 string）去索引，因此两者需要保持一致。

```ts
class Animal {
  name: string
}
class Dog extends Animal {
  breed: string
}

// 错误：使用数值型的字符串索引，有时会得到完全不同的Animal!
interface NotOkay {
  [x: number]: Animal
  [x: string]: Dog
}
```

## 类类型

与 C#或 Java 里接口的基本作用一样，TypeScript 也能够用它来明确的强制一个类去符合某种契约。

```ts
interface ClockInterface {
  currentTime: Date
  setTime(d: Date)
}

class Clock implements ClockInterface {
  currentTime: Date
  setTime(d: Date) {
    this.currentTime = d
  }
  constructor(h: number, m: number) {}
}
```

> 接口描述了类的公共部分，而不是公共和私有两部分。 它不会帮你检查类是否具有某些私有成员。

## 混合类型

一个对象可以同时做为函数和对象使用，并带有额外的属性。

```ts
interface Counter {
  (start: number): string
  interval: number
  reset(): void
}

function getCounter(): Counter {
  let counter = <Counter>function(start: number) {}
  counter.interval = 123
  counter.reset = function() {}
  return counter
}

let c = getCounter()
c(10)
c.reset()
c.interval = 5.0
```

## 接口继承类

`接口继承类`,接口继承类的所有成员(包括私有成员和受保护成员),但不会实现。如果继承的类中含有私有成员或受保护成员，这个接口类型只能被这个类或其子类所实现。

```ts
class Control {
  private state: any
}

interface SelectableControl extends Control {
  select(): void
}

class Button extends Control implements SelectableControl {
  select() {}
}

// 错误：“Image”类型缺少“state”属性。
class Image implements SelectableControl {
  select() {}
}
```
