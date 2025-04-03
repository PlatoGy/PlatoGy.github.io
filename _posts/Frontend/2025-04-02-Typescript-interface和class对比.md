---
layout: post
title: TypeScript 中的 `interface` 与 `class` 区别与使用场景对比
author: Patrick Gao
date: 2025-04-02 22:18
categories:
  - Frontend
tags:
  - Typescript
mermaid: true
math: true
pin: false
---

# TypeScript 中的 `interface` 与 `class` 区别与使用场景对比

## ✅ interface 是什么？

- 只负责**描述数据结构**（字段、类型、方法签名）
- 没有实际实现逻辑
- 编译后不会出现在 JS 中（**开发时用，运行时无踪影**）
- 通常用于 API、表单、对象的类型定义

```ts
interface Beer {
  name: string;
  style: string;
  rating: number;
}

const myBeer: Beer = {
  name: 'Heady Topper',
  style: 'NEIPA',
  rating: 5,
};
```

---

## ✅ class 是什么？

- 可以描述结构（字段），也可以实现方法逻辑
- 可以通过 `new` 来创建对象
- 编译后会变成 JavaScript 的构造函数
- 通常用于服务类、逻辑类、可实例化对象

```ts
class BeerService {
  private beers: Beer[] = [];

  addBeer(beer: Beer) {
    this.beers.push(beer);
  }

  getAllBeers(): Beer[] {
    return this.beers;
  }
}
```

---

## 🆚 interface vs class 对比表格

| 对比项 | interface | class |
|--------|-----------|-------|
| 能否实例化（new） | ❌ 不可以 | ✅ 可以 |
| 是否有实际实现逻辑 | ❌ 没有 | ✅ 有 |
| 编译后是否存在于 JS 中 | ❌ 不存在 | ✅ 存在 |
| 是否能做类型注解 | ✅ 可以 | ✅ 可以 |
| 是否适合做依赖注入（Angular） | ❌ 不可以 | ✅ 可以 |
| 是否可以被继承 | ✅ 支持 extends | ✅ 支持 extends / implements |
| 推荐用途 | 定义结构类型，如数据对象、API 返回值 | 实现服务类、工具类、状态管理、组件类等 |

---

## 📝 使用建议

- 如果只是定义对象结构 👉 用 `interface`
- 如果要封装逻辑、状态、行为 👉 用 `class`
- 如果你需要依赖注入 / Angular 服务 👉 必须用 `class`

---

## 📌 示例：配合使用

```ts
interface Beer {
  name: string;
  style: string;
  rating: number;
}

class BeerService {
  constructor(private data: Beer[]) {}

  filterByStyle(style: string): Beer[] {
    return this.data.filter(beer => beer.style === style);
  }
}
```

