---
title: "關於 ESLint v9"
date: 2024-06-11T19:23:04+08:00
draft: true
tags: ["note", "javascript", "typescript", "eslint"]
---

## 前情提要

近期比較有空閒來處理重構的一些東西，  
手上的 `Vue.js` 專案剛好可以來試一下 `ESLint`，  
順便理解一下目前 ESLint 發展到什麼樣子。(上次使用應該有五年前了...)  

## 哪些雷被我踩到

首先，很重要的一段話，先分享給大家，
```
如果是使用 typescript 的話，千萬不要使用到 ESLint v9！！！
如果是使用 typescript 的話，千萬不要使用到 ESLint v9！！！
如果是使用 typescript 的話，千萬不要使用到 ESLint v9！！！
```

當下的時空背景(2024/06)，`ecosystem` 都還未完善(包含`typescript-eslint`)，直接被炸爛。  

當時沒先多做研究，以為 ESLint 很單純，就裝套件+寫 config 就好，  
所以我就看著官網，安裝了 ESLint (理所當然是最新的 v9)，

並且注意到，原來現在設定檔有新的寫法 flat config，  
看起來是 v8 就開始有，具體的好處，自己查唄不贅述，  
檔案也從以前建議的 `.eslintrc.js` 轉換成 `eslint.config.js`。  

試跑了一次 `npx eslint .`，理所當然炸了一堆錯ＸＤ，  
主要可以歸類以下：
1. 無法識別 typescript
2. 無法識別 vue 的語法
3. 需要忽略 dist 底下的靜態檔案 以及 node_modules

首先，發現使用 `typescript` 的話，需要多裝 `typescript-eslint` 來幫助識別，
所以我到了 [TS 版官網](https://typescript-eslint.io/getting-started/)，按照提供的步驟安裝(自行省略已安裝的套件)，
```
結果就踩到雷引爆了...裝不了啊...
```
原因是 `typescript-eslint` 版本還沒匹配 ESLint v9，  
所以只能選擇退版，否則無法使用...  
最簡單的方式是先移除 ESLint ，比照 TS 版官網，一次安裝下去所有相關的套件(會`自動`去匹配版本)
```
npm install --save-dev eslint @eslint/js @types/eslint__js typescript typescript-eslint
```

裝好之後，就參考 TS 版官網寫設定，  
設定檔這邊也有小踩雷，flat config 的寫法，還沒有很廣泛使用，  
如果是一開始就看 TS 版官網的說明，  
會有點搞不清楚怎麼加設定(有些要展開有些不用)，  
其他相關的 ecosystem 的說明甚至都還停留在舊寫法，  
以至於撰寫時有點混亂+痛苦(一開始問 chatgpt 也是提供舊寫法ＸＤ)。  

接下來，添加 `vue-eslint-parser` 來識別 vue 檔，  
此時的設定說明，就是舊版寫法，難受，  
還好 TS 版官網有 [FAQ](https://typescript-eslint.io/troubleshooting/#i-am-running-into-errors-when-parsing-typescript-in-my-vue-files) 可以參考，  
同時，可以順便添加 `ignores` 來處理需要忽略的目錄。  

最終設定檔會類似以下：
```
...
```

## 小整理
