# 类

- 英文文档：[http://www.typescriptlang.org/docs/handbook/classes.html](http://www.typescriptlang.org/docs/handbook/classes.html)
- 中文文档：[https://www.tslang.cn/docs/handbook/classes.html](https://www.tslang.cn/docs/handbook/classes.html)

## 示例代码

```ts
class Person {
  static total = 0 // 每个实例想要访问这个属性的时候，都要通过 Person.total 访问。
  protected name: string // protected成员只能在声明它的类和派生类中访问。
  private age: number // 不能在声明它的类的外部访问。
  readonly id: number // 只读属性必须在声明时或构造函数里被初始化。

  // 构造函数也可以被标记成 protected。 这意味着这个类不能在包含它的类外被实例化，但是能被继承。
  protected constructor(name: string, age: number, id: number) {
    this.name = name
    this.age = age
    this.id = id
  }
}

class Employee extends Person {
  private department: string

  constructor(name: string, age: number, id: number, department: string) {
    super(name, age, id)
    this.department = department
  }

  public printEmployee() {
    return `Hello, my name is ${this.name} and I work in ${this.department}.`
  }
}
```

## 参数属性

参数属性通过给构造函数参数前面添加一个访问限定符来声明。使用 private 限定一个参数属性会声明并初始化一个私有成员；对于 public 和 protected 来说也是一样。

```ts
class Person {
  readonly id: number

  constructor(id: number) {
    this.id = id
  }
}
```

通过参数属性可以写为:

```ts
class Person {
  constructor(readonly id: number) {}
}
```

## 存取器(getters/setters)

通过 getters/setters 来截取对对象成员的访问, 它能帮助你有效的控制对对象成员的访问。

```ts
let passcode = "secret passcode"

class Employee {
  private _fullName: string

  get fullName(): string {
    return this._fullName
  }

  set fullName(newName: string) {
    if (passcode && passcode == "secret passcode") {
      this._fullName = newName
    } else {
      console.log("Error: Unauthorized update of employee!")
    }
  }
}
```

> 只带有 get 不带有 set 的存取器自动被推断为 readonly。

## 抽象类

抽象类做为其它派生类的基类使用。 它们一般不会直接被实例化。 不同于接口，抽象类可以包含成员的实现细节。 abstract 关键字是用于定义抽象类和在抽象类内部定义抽象方法。

```ts
abstract class Department {
  constructor(public name: string) {}

  printName(): void {
    console.log("Department name: " + this.name)
  }

  abstract printMeeting(): void // 抽象方法, 必须在派生类中实现
}

class AccountingDepartment extends Department {
  constructor() {
    super("Accounting and Auditing") // 在派生类的构造函数中必须调用 super()
  }

  printMeeting(): void {
    console.log("The Accounting Department meets each Monday at 10am.")
  }

  generateReports(): void {
    console.log("Generating accounting reports...")
  }
}

let department: Department // 允许创建一个对抽象类型的引用
// department = new Department(); // 错误: 不能创建一个抽象类的实例
department = new AccountingDepartment() // 允许对一个抽象子类进行实例化和赋值
department.printName()
department.printMeeting()
// department.generateReports(); // 错误: 方法在声明的抽象类中不存在
```
