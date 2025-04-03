---
layout: post
title: Angular笔记
author: Patrick Gao
date: 2025-03-30 03:46
categories:
  - Frontend
tags:
  - Angular
mermaid: true
math: true
pin: false
---


# 🅰️ Angular 笔记

---

## ✅ @Component 装饰器及常用属性

```ts
@Component({
  selector: 'app-user',           // HTML 中使用的标签名
  standalone: true,               // 是否为独立组件
  templateUrl: './user.component.html', // 模板路径
  styleUrls: ['./user.component.css'],  // 样式路径
  imports: [CommonModule, FormsModule] // 依赖模块（standalone 时用）
})
export class UserComponent {
  name = 'Angular';
}
```

---

## ✅ 控制结构指令

### 🔹 `@if`

```html
@if (isLoggedIn) {
  <p>Welcome back!</p>
}
```

### 🔹 `@for`

```html
@for (item of items; track item.id) {
  <li>{{ item.name }}</li>
}
```

---

## ✅ 绑定语法（Binding）

- **属性绑定**：`[src]="imgUrl"`
- **事件绑定**：`(click)="handleClick()"`
- **双向绑定**：`[(ngModel)]="username"`
- **模板表达式**：`{{ title | uppercase }}`

---

## ✅ 事件处理（Event Handling）

```html
<button (click)="handleClick()">Click me</button>
```

```ts
handleClick() {
  console.log('Clicked!');
}
```

---

## ✅ @Input() 和 @Output()

### 子组件：

```ts
@Input() name: string = '';
@Output() addItem = new EventEmitter<string>();
```

### 父组件：

```html
<app-child [name]="parentName" (addItem)="handleAdd($event)"></app-child>
```

---

## ✅ @defer(on viewport)

延迟加载组件：

```html
@defer (on viewport) {
  <expensive-component />
}
```

---

## ✅ @placeholder 和 @loading(minimum)

```html
@defer (on viewport) {
  @placeholder {
    <p>Loading preview...</p>
  }
  @loading(minimum 300ms) {
    <p>Loading actual content...</p>
  }
  <expensive-component />
}
```

---

## ✅ NgOptimizedImage

内建图像优化支持：

```html
<img [ngSrc]="'/assets/banner.jpg'" width="600" height="400" />
```

---

## ✅ 路由 Router 使用

### 1. 定义路由（app.routes.ts）

```ts
export const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent },
];
```

### 2. 添加到 `RouterModule`

```ts
imports: [RouterModule.forRoot(routes)]
```

### 3. 使用 `<router-outlet>`

```html
<router-outlet></router-outlet>
```

### 4. 使用 `routerLink`

```html
<a routerLink="/about">About</a>
```

---

## ✅ 双向绑定 ngModel 的使用

```ts
imports: [FormsModule]
```

```html
<input [(ngModel)]="username" />
<p>{{ username }}</p>
```

---

## ✅ 表单 Forms 和校验 Validation

### 模板驱动表单：

```html
<form #f="ngForm" (ngSubmit)="submitForm(f)">
  <input name="email" ngModel required />
  <button type="submit" [disabled]="!f.valid">Submit</button>
</form>
```

---

## ✅ @inject() 与构造函数注入

```ts
import { inject } from '@angular/core';

@Component({ ... })
export class ExampleComponent {
  private service = inject(MyService);
}
```

也可以传统构造函数方式：

```ts
constructor(private myService: MyService) {}
```

---

## ✅ 管道 Pipes & 自定义 Pipe

### 使用内置管道：

```html
{{ username | lowercase }}
{{ birthday | date:'longDate' }}
```

### 自定义管道：

```ts
@Pipe({ name: 'reverse' })
export class ReversePipe implements PipeTransform {
  transform(value: string): string {
    return value.split('').reverse().join('');
  }
}
```

## 📌 模板引用变量 `#text`

```html
<input #text />
<button (click)="add(text.value)">Add</button>
```

### ✅ 含义：
- `#text` 是**模板引用变量**，可以在模板中引用该 DOM 元素。
- 在 `(click)="add(text.value)"` 中，`text.value` 表示获取 input 输入框的当前值。

### 🔍 类似原生 JavaScript：
```js
const text = document.getElementById('text');
add(text.value);
```

---

## 🔢 `$index` 用法

```html
@for (todo of todos; track $index) {
  <p>
    <input type="checkbox" (change)="toggle($index)" />
  </p>
}
```

### ✅ 含义：
- `$index` 是 `@for` 循环中自带的局部变量，表示当前元素在数组中的索引（从 `0` 开始）。
- 可用于操作当前项，比如点击按钮时传入当前索引。

---

## 🆕 `@for` 和 `@empty` 控制结构

```html
@for (todo of todos; track $index) {
  <!-- 列出 todo 项 -->
} @empty {
  <p>No todos</p>
}
```

### ✅ 含义：
- `@for` 是 Angular 17 引入的新控制结构，用于替代传统的 `*ngFor`。
- `@empty` 是 `@for` 的一部分，用于处理**数组为空时**的情况。

### 🔁 对比旧写法（使用 *ngIf + *ngFor）：
```html
<div *ngIf="todos.length > 0; else noTodos">
  <div *ngFor="let todo of todos">{{ todo.text }}</div>
</div>
<ng-template #noTodos>
  <p>No todos</p>
</ng-template>
```



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

---

