# 泛型

- 英文文档：[http://www.typescriptlang.org/docs/handbook/generics.html](http://www.typescriptlang.org/docs/handbook/generics.html)
- 中文文档：[https://www.tslang.cn/docs/handbook/generics.html](https://www.tslang.cn/docs/handbook/generics.html)

在像 C#和 Java 这样的语言中，可以使用`泛型`来创建可重用的组件，一个组件可以支持多种类型的数据。

## 泛型函数

```ts
function identity<T>(arg: T): T {
  return arg
}

let output = identity<string>("myString")
```

## 泛型接口

```ts
interface GenericIdentityFn<T> {
  (arg: T): T
}

function identity<T>(arg: T): T {
  return arg
}

let myIdentity: GenericIdentityFn<number> = identity
```

## 泛型类

```ts
class GenericNumber<T> {
  zeroValue: T
  add: (x: T, y: T) => T
}

let myGenericNumber = new GenericNumber<number>()
myGenericNumber.zeroValue = 0
myGenericNumber.add = function(x, y) {
  return x + y
}
```

> 泛型类指的是实例部分的类型，所以类的静态属性不能使用这个泛型类型。

## 泛型约束

泛型约束，使得`loggingIdentity`接受的参数必须实现了`.length`属性，也就是说它不能再是任意类型了。

```ts
interface Lengthwise {
  length: number
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length) // Now we know it has a .length property, so no more error
  return arg
}
```

## 在泛型约束中使用类型参数

现在我们想要用属性名从对象里获取这个属性。 并且我们想要确保这个属性存在于对象 `obj`上，因此我们需要在这两个类型之间使用约束。

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K) {
  return obj[key]
}

let x = { a: 1, b: 2, c: 3, d: 4 }

getProperty(x, "a") // okay
getProperty(x, "m") // error: 类型“"m"”的参数不能赋给类型“"a" | "b" | "c" | "d"”的参数。
```

## 在泛型里使用类类型

```ts
function createInstance<A extends Animal>(c: new () => A): A {
  return new c()
}
```
