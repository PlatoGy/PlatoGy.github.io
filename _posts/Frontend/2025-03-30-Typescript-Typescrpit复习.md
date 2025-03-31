---
layout: post
title: Typescript复习
author: Patrick Gao
date: 2025-03-30 16:59
categories:
  - Frontend
tags:
  - Typescript
mermaid: true
math: true
pin: false
---


# TypeScript 复习笔记 & 问题解答

## 📘 快速复习

### 1. 基础类型

```ts
let num: number = 42;
let str: string = "Hello";
let isDone: boolean = true;
let arr: number[] = [1, 2, 3];
let tuple: [string, number] = ["age", 30];
let anyValue: any = "can be anything";
let unknownValue: unknown = "safer any";
```

---

### 2. 函数类型

```ts
function add(x: number, y: number): number {
  return x + y;
}

const multiply: (a: number, b: number) => number = (a, b) => a * b;
```

---

### 3. 接口（Interface）

```ts
interface Person {
  name: string;
  age?: number;
}

const p1: Person = { name: "Alice" };
```

---

### 4. 类型别名（Type Alias）

```ts
type ID = string | number;

function printId(id: ID) {
  console.log(id);
}
```

---

### 5. 类（Class）

```ts
class Animal {
  constructor(public name: string) {}

  move(distance: number): void {
    console.log(`${this.name} moved ${distance}m.`);
  }
}
```

---

### 6. 泛型（Generics）

```ts
function identity<T>(arg: T): T {
  return arg;
}

let output = identity<string>("myString");
```

---

### 7. 枚举（Enum）

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}
```

---

### 8. 类型断言（Type Assertion）

```ts
let someValue: unknown = "this is a string";
let strLength: number = (someValue as string).length;
```

---

### 9. 联合类型 & 类型守卫

```ts
function log(input: string | number) {
  if (typeof input === "string") {
    console.log("String:", input);
  } else {
    console.log("Number:", input);
  }
}
```

---

### 10. 模块导入导出

```ts
// math.ts
export function square(x: number): number {
  return x * x;
}

// main.ts
import { square } from "./math";
```

---

## ❓ 你的提问 & 解答

### 1️⃣ tuple 是什么？
> Tuple（元组）是一个固定长度、每个位置类型都确定的数组。

```ts
let tuple: [string, number] = ["Alice", 30];
```

---

### 2️⃣ unknown 和 any 区别？

| 特点 | any | unknown |
|------|-----|---------|
| 安全性 | 不安全 | 更安全 |
| 是否能直接用 | ✅ 可以 | ❌ 不行，需类型判断 |

```ts
let a: any = "hello";
let u: unknown = "hello";
if (typeof u === "string") {
  u.trim(); // OK
}
```

---

### 3️⃣ interface 是干什么用的？

> 定义对象的结构，规定属性、类型等。

```ts
interface Person {
  name: string;
  age?: number;
}
```

---

### 4️⃣ 问号（age?）是什么意思？

> 表示可选属性，即可以有也可以没有。

---

### 5️⃣ 泛型是什么？和 type 有什么区别？

> 泛型是“类型参数化”，type 是“类型别名”。

```ts
function identity<T>(arg: T): T {
  return arg;
}

type ID = string | number;
```

---

### 6️⃣ 枚举是什么？

> 一组命名常量的集合。

```ts
enum Direction {
  Up, Down, Left, Right
}
```

---

### 7️⃣ 类型断言是干什么的？

> “我知道这个值的类型是什么”，告诉 TS 编译器不要担心。

```ts
let val: any = "hello";
let len = (val as string).length;
```

---

## ✅ 小结

- tuple：固定类型的数组
- unknown vs any：unknown 更安全
- interface：对象结构定义
- ?：可选属性
- 泛型：写通用函数/类
- type：类型别名
- enum：一组常量
- 类型断言：告诉编译器你知道它的类型



