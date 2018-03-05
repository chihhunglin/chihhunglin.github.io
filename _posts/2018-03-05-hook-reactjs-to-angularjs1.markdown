---
layout: post
title:  "How to hook ReactJs to your existing AngularJS 1.X app [筆記]"
date:   2018-03-05 12:03:06 +0800
categories: AngularJS ReactJS
---
[原文出處][reactjstoangularjs]

此篇文章有很好的範例，並且解釋了AngularJS 跟 React 的不同：

> Angular puts JS into HTML while React puts HTML into JS.

總結:

1. 創建一個 directive 包裹 React app
2. 通過隔離的 scope 從 parent 輸入 data 到 directive
3. 利用 `scope.$watch()` 擷取更新的值，並且實作在 `link()`
4. 數入值給 react app 的 `props`

[reactjstoangularjs]: https://codeburst.io/how-to-hook-reactjs-to-your-existing-angularjs-1-x-app-5ab1ac59c0c1
