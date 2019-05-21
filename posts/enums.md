# 枚举

- 英文文档：[http://www.typescriptlang.org/docs/handbook/enums.html](http://www.typescriptlang.org/docs/handbook/enums.html)
- 中文文档：[https://www.tslang.cn/docs/handbook/enums.html](https://www.tslang.cn/docs/handbook/enums.html)

使用枚举我们可以定义一些带名字的常量。 使用枚举可以清晰地表达意图或创建一组有区别的用例。 TypeScript 支持数字的和基于字符串的枚举。

## 数字枚举

```ts
enum Direction {
  Up = 1,
  Down, // 自增为2，依次类推
  Left,
  Right,
}

function move(message: Direction): void {
  // ...
}

move(Direction.Down)
```

## 字符串枚举

```ts
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}
```

## 枚举是实际存在的对象

```ts
enum E {
  X,
  Y,
  Z,
}

function f(obj: { X: number }) {
  console.log(obj.X)
}

f(E) // 0
```

## 反向映射

`数字枚举成员`还具有了 反向映射，从枚举值到枚举名字。 例如，在下面的例子中：

```ts
enum Enum {
  A,
}
let a = Enum.A
let nameOfA = Enum[a] // "A"
```

ts 会把它编译为:

```ts
var Enum
;(function(Enum) {
  Enum[(Enum["A"] = 0)] = "A"
})(Enum || (Enum = {}))
var a = Enum.A
var nameOfA = Enum[a] // "A"
```

> 要注意的是 不会为字符串枚举成员生成反向映射。

## 常量枚举

常量枚举，编译期间会被删除。使用`const`修饰符来定义。常量枚举不允许包含计算成员。

```ts
const enum Directions {
  Up,
  Down,
  Left,
  Right,
}

let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right]
```

生成代码:

```ts
var directions = [0 /* Up */, 1 /* Down */, 2 /* Left */, 3 /* Right */]
```
