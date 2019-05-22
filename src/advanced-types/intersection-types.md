# 交叉类型

交叉类型是将多个类型合并为一个类型。使用 `&` 连接, 比如 `T & U`。

## 代码示例

`T & U`这个类型的对象同时拥有了`T`和`U`两种类型的成员。

```ts
function extend<T, U>(first: T, second: U): T & U {
  let result = <T & U>{}
  for (let id in first) {
    ;(<any>result)[id] = (<any>first)[id]
  }
  for (let id in second) {
    if (!result.hasOwnProperty(id)) {
      ;(<any>result)[id] = (<any>second)[id]
    }
  }
  return result
}

class Person {
  constructor(public name: string) {}
}
class ConsoleLogger {
  log() {
    // ...
  }
}
var jim = extend(new Person("Jim"), new ConsoleLogger())
var n = jim.name
jim.log()
```
