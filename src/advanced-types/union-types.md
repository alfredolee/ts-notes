## 联合类型

联合类型使用`|`分隔每个类型。例如： `number | string | boolean`表示一个值可以是 `number`， `string`，或 `boolean`。

### 代码示例

```ts
function print(value: number | string) {
  if (typeof value === "number") {
    console.log(`这是一个数字: ${value}`)
  }
  if (typeof value === "string") {
    console.log(`这是一个长度为${value.length}的字符串`)
  }
}

print(1) // 这是一个数字: 1
print("1") // 这是一个长度为1的字符串
```

> 如果一个值是联合类型，我们只能访问此联合类型的所有类型里共有的成员。因为`|`可以理解为或，我们不知道你到底是哪个类型，所以只能让你访问共有的成员。
