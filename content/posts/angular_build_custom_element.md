---
title: "Angular build custom element"
date: 2023-10-30T09:22:36+08:00
draft: false
categories: [Angular]
---

## Intro

當使用 Angular 時, 有時會有需要自己建立一個自定義的元素

通常這個都是為了重複使用

這時會有兩種作法

1. 自己建立一個元件, 再把這元件處理成 module, 這樣就可以有自定義元素了

2. 使用 angular create lib 的方式(https://angular.io/guide/creating-libraries)

如果是在公司內部自己使用, 用 1 或是 2 都沒差

如果是要做成給外部或是別人使用, 甚至是開源出去, 那就是得用 2

順帶一提如果要使用自己定義的元素, 需要安裝 `@angular/elements`

```shell
yarn add @angular/elements
```

## 自己建立元件

這邊會用 `custom-element` 當成元件名字舉例

```shell
ng generate component custom-element
```

建立起一個 `custom-element` 元件

之後就是依照寫元件的方式開發

只是得自己手動處理一下在 `custom-element/custom-element.module.ts` 得添加和輸出與建立自定義元素的設定

```typescript
import { createCustomElement } from '@angular/elements';
import { createCustomElement } from '@angular/elements';
import { NgModule, Injector } from '@angular/core';
import { CustomElementComponent } from './custom-element.component';

@NgModule({
  declarations: [CustomElementComponent],
  exports: [CustomElementComponent],
})
export class CustomElementModule {
  constructor(private injector: Injector) {
  }

  ngDoBootstrap() {
    const customElement = createCustomElement(CustomElementComponent, { injector: this.injector });
    customElements.define('app-custom-element', customElement);
  }
}
```

之後要使用的元件或是直接在最頂部的 `app.module.ts` 添加 import

例如在最頂部的 `app.module.ts` 添加

```typescript
import { CustomElementModule } from './custom-element/custom-element.module';

@NgModule({
  imports: [
    CustomElementModule
  ]
})
```

這樣就可以直接在 HTML 使用了

```html
<app-custom-element></app-custom-element>
```

## 使用 angular create lib

這個方式會比較多步驟

最後如果要發佈到 npm 還需要做發佈的動作

也可以做打包給別人用

但如果不需要打包或發佈

也可以單純建好後從 lib 載入來使用

基本上跟著官方文件(https://angular.io/guide/creating-libraries)走就可以了

這裡就補充下打包的部分

```shell
ng build my-lib
cd dist/my-lib
npm pack
```

這樣沒有意外的話會產生 `my-lib-0.0.1.tgz` (0.0.1 這個是隨著這個 lib 的 package.json)

### 安裝打包的套件

```shell
yarn add ./my-lib-0.0.1.tgz
```

這樣就可以安裝了

之後就正常載入使用

### 注意事項

目前測試 `ng generate library my-lib` 創建出來的東西打包後

有注意到如果本身有 import 其他套件的話

套件 source code 並不會一起放進來

應該是需要在該 lib 底下的 `package.json` 添加

打包後, 這樣之後安裝時才會一起安裝

例如 `projects/my-lib/package.json` 添加需要的套件

或是在 `projects/my-lib/` 安裝套件, 讓 `package.json` 有紀錄到安裝什麼套件

另外因為在開發與測試時如果同一個名字, 版號也一樣, yarn 會 cache, angular 也可能會 cache

所以移掉後再安裝前建議先下

```shell
yarn cache clean
```

也一起移出掉專案目錄底下的 `.angular` 資料夾