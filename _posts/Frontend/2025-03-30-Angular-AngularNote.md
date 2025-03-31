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

---

👉 本笔记涵盖了 Angular 中常见的结构、语法、指令、依赖注入、路由、表单、图片优化等核心知识。



