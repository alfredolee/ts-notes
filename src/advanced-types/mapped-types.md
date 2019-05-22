## 映射类型

一个常见的任务是将一个已知的类型每个属性都变为可选的：

```ts
interface PersonPartial {
  name?: string
  age?: number
}
```

或者我们想要一个只读版本：

```ts
interface PersonReadonly {
  readonly name: string
  readonly age: number
}
```

这在 JavaScript 里经常出现，TypeScript 提供了从旧类型中创建新类型的一种方式 — 映射类型。 在映射类型里，新类型以相同的形式去转换旧类型里每个属性。 例如，你可以令每个属性成为 readonly 类型或可选的。 下面是一些例子：

```ts
type Readonly<T> = { readonly [P in keyof T]: T[P] }
```
