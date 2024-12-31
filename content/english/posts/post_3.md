---
title: "什麼是微前端？"
meta_title: "微前端"
description: "Zachary的微前端筆記"
date: 2024-12-31T11:11:00Z
author: "Zachary Tu"
image: "/images/posts/post_3.jpg"
categories: ["筆記", "前端"]
tags: ["微前端"]
draft: false
---

> *學得越多，懂得越少*

工作上主管問到微前端是什麼，於是就查了資料整理一份筆記。

在應答上可以回答主管大部分的問題，但距離實作還有好一段路要走。

頗有學得越多，懂得越少的感觸。

<hr>

## 微前端是什麼？
微前端是一種將單個應用程式拆分成多個獨立部署的軟體架構模式。  
每個微前端都可以由不同的團隊獨立開發、部署和維護，技術選型也不受限制。這使得大型複雜的應用程式能夠更加靈活、可維護，並能更好地適應不斷變化的業務需求。


![image](https://docs.aws.amazon.com/images/prescriptive-guidance/latest/micro-frontends-aws/images/mfe-architectures.png)
圖例：微前端架構應用示意圖，展示不同子應用如何組合成一個整體應用。


目前我們的 Web application 是由單一的前端搭配 BFF（Backend for Frontend）組成，可以參考上圖上半部分的最左邊一個橘色虛線方塊。 
現行銀行系統大多與上圖下半部分「Domain services」的情況相似：藉由輕量 EAI（API gateway）作為一個統一的入口，負責接收外部請求，並將請求傳送到相應的微服務。

### 微前端的優點
- 獨立開發部署： 各個微前端可以獨立開發、測試、部署，減少團隊之間的協調成本。
- 技術選擇靈活： 各個微前端可以自由選擇適合的技術（框架），無需強求統一。
- 可伸縮性強： 可以根據業務需求，增減微前端，實現系統的靈活擴展。
- 降低風險： 單個系統功能發生錯誤，不會影響其他系統功能。
- 易於維護： 每個微前端的代碼量較小，更容易維護。

### 微前端的缺點
- 複雜性增加： 微前端架構增加了系統的複雜性，需要更多的基礎設施和協調。
- 初次搭建成本高： 建立微前端架構需要投入較多的時間和精力。
- 開發規範增加：應用程式唯一資料的控制需要進行團隊的規範（router、語系、storage）。
- 用戶體驗可能受影響： 如果微前端之間的整合（路由設置）不夠順暢，可能會影響用戶體驗。

<hr>

## 微前端的使用場景
- 大型應用：單一前端專案變得龐大，影響開發效率與編譯速度。
- 多團隊協作：跨部門合作，難以同步維護單一應用。
- 業務元件復用：需要將某些功能模塊對外開放或複用。

### 何時該使用微前端
- 業務模塊獨立性強： 應用程序邏輯可以被拆分成明確的子模塊。
- 跨團隊協作： 不同團隊各自負責不同模塊，能大幅降低協作成本。
- 技術堆疊多樣： 需要多技術堆疊共存，滿足不同團隊需求。

### 何時不該使用微前端
- 小型應用： 微前端引入的架構成本大於收益。
- 小團隊資源有限： 難以負擔微前端的基礎設施建設與運營。
- 性能要求極高： 首屏加載和交互性能需優先考量時。
- 快速迭代項目： 搭建微前端基礎設施可能會拖慢進度。

<hr>

## 評估導入微前端的可行性
1. 現狀分析：應用的規模、複雜度是否需要微前端來提升效率？
2. 團隊能力：團隊是否具備架構設計與技術選型的經驗？
3. 成本與效益：微前端是否能在合理的投入內帶來顯著效益？

<hr>

## 相關名詞與工具
### 技術概念
- Native Federation：基於原生瀏覽器功能（如 ES 模組）進行動態模組共享。
- Module Federation：Webpack 5 引入的模組共享技術，支持跨應用的動態加載與共享。
- SSR (Server-Side Rendering)：在伺服器端渲染頁面以提升 SEO 和首屏速度。
- CSR (Client-Side Rendering)：所有渲染工作在用戶端完成，適用於 SPA 應用。
### 工具與框架
- ESBuild：快速 JavaScript/TypeScript 打包工具，性能優於傳統工具。
- Vite：專注於快速開發和熱更新的現代前端建置工具。
- Nx：適合管理大型單一代碼庫的工具集，支持微前端架構。
- Webpack：模組打包工具，支持微前端的核心技術（如 Module Federation）。
### 微前端架構專有名詞
- Shell App / Host：主應用，負責載入與管理子應用。
- Micro App / Remote：子應用，獨立運行並由 Shell App 動態載入。
- Monorepos：單一代碼庫管理方式，適用於微前端的代碼組織。

<hr>

## 參考資料
- [《Angular Architects》 使用現代 Angular 的微前端](https://www.angulararchitects.io/en/blog/micro-frontends-with-modern-angular-part-1-standalone-and-esbuild/)
- [《Angular.love》 Angular 微前端](https://angular.love/angular-micro-frontends-a-modern-approach-to-complex-app-development)
- [《AWS》 瞭解並實作微前端](https://docs.aws.amazon.com/prescriptive-guidance/latest/micro-frontends-aws/introduction.html)
- [《AWS》 什麼是企業應用整合（EAI）？](https://aws.amazon.com/what-is/enterprise-application-integration/?nc1=h_ls)
- [《DEV》 用 Native Federation 的微前端 ](https://dev.to/florianrappl/micro-frontends-with-native-federation-56j4)
- [《iT邦幫忙》 前端也可以搞微服務？！前端最複雜的一種架構 ](https://ithelp.ithome.com.tw/m/users/20132666/ironman/7130)
- [《Medium》 用 Nx 一起建立 Angular 和 React 應用程式](https://qiankun.umijs.org/zh/guide)
- [《Medium》 與 Jimy Dolores 一起使用 Angular 進行微前端](https://medium.com/angularidades/microfrontends-in-angular-with-jimy-dolores-c59f54bb5599)
- [《Medium》 與 Bezael Pérez 一起使用 Angular 進行微前端](https://medium.com/angularidades/microfrontends-in-angular-with-bezael-p%C3%A9rez-ea73930dfcb7)
- [《qiankun》 微前端指南](https://qiankun.umijs.org/zh/guide)
- [《single-spa》 開始使用 single-spa](https://single-spa.js.org/docs/getting-started-overview)
- [《Telerik》 微前端與 Monorepos](https://www.telerik.com/blogs/react-basics-microfrontend-vs-monorepos)
- [《XENONSTACK》 微前端架構與最佳實踐](https://www.xenonstack.com/insights/micro-frontend-architecture)

<hr>

## 參考專案
- [ 乾坤 ](https://github.com/umijs/qiankun)
- [ Single-spa ](https://github.com/nitinreddy3/react-ng-spa-app)
- [ Module Federation ](https://github.com/manfredsteyer/module-federation-plugin-example)