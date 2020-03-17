---
title: 学习Typescript(一)
date: 2019-08-09 15:54:16
tags: 学习
categories: 编程
---

现在TypeScript被越来越多的人推荐，处于好奇我也准备学习学习。以下是学习笔记，不是啥厉害的文章。

TypeScript的特点就是赋予了javaScript类型吧，看到有人调侃称TypeScript为AnyScript，讽刺大量使用any类型的现象吧。

通过React+TypeScript以及Angular（官方使用TypeScript开发）发觉了一些TypeScript的优点：

1. 可以极大程度的避免在程序运行时类型预判错误造成的问题。
2. 定义好接口后，在vscode中会获得非常方便的提醒能力。

开始学习：

#### 基础

###### Boolean

```typescript
let isDone: boolean = false;
```

###### Number

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
```

###### String

```typescript
let color: string = "blur";
color = 'red';
```

###### Array

使用<>声明方式的情况在file.tsx中由于jsx语法的判断可以改为使用 as 替代。

```typescript
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```

###### Tuple

```typescript
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"]; // Error
```

###### Enum

```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

默认情况下从0开始，c应该等于1，也可以自定义设置它的值

```typescript
// 设一个
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green;
// 设所有
enum Color {Red = 1, Green = 2, Blue = 4}
let c: Color = Color.Green;
// 
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];
console.log(colorName); // Displays 'Green' as its value is 2 above

```

###### Any

可以为所欲为了，就像回到了js。

###### Void

函数没有返回值，或

```typescript
let unusable: void = undefined;
```

###### Null and Undefind

```typescript
// Not much else we can assign to these variables!
let u: undefined = undefined;
let n: null = null;
```

默认Null and Undefind 是其他类型的子类，比如number也可以返回undefind。

可以使用 --strictNullChecks 标记，null and undefind 只匹配any



###### Never

Some examples of functions returning `never`:

```typescript
// Function returning never must have unreachable end point
function error(message: string): never {
    throw new Error(message);
}

// Inferred return type is never
function fail() {
    return error("Something failed");
}

// Function returning never must have unreachable end point
function infiniteLoop(): never {
    while (true) {
    }
}

```

#####  与 `void` 的差异

一旦有人告诉你，`never` 表示一个从来不会优雅的返回的函数时，你可能马上就会想到与此类似的 `void`，然而实际上，`void` 表示没有任何类型，`never` 表示永远不存在的值的类型。

当一个函数没有返回值时，它返回了一个 `void` 类型，但是，当一个函数根本就没有返回值时（或者总是抛出错误），它返回了一个 `never`，`void` 指可以被赋值的类型（在 `strictNullChecking` 为 false 时），但是 `never` 不能赋值给其他任何类型，除了 `never`。

###### Object

就和js的Object没啥区别





#### Tips:

我使用vscode作为编辑器，有个插件叫做**Code Runner**能够直接在vscode中运行代码片段，非常方便。不过对于typescript还需要安装ts-node，使用npm安装一哈就好了。