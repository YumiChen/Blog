---
layout: post
title: "使用LocalStorage"
author: "Yumi Chen"
categories: Javascript
tags: [Javascript]
---
LocalStorage擁有比cookies更大的容量(5mb),是除了cookies外另外一個在使用者的瀏覽器中儲存資料的選擇。

在進入這次的主題之前，先談談Storage。Storage分為兩種:
» LocalStoarge
» SessionStorage
前者沒有資料消失的期限，後者則是在tab關閉後資料便消失了。(特別注意並非關閉瀏覽器之後)

首先:
(1)確認瀏覽器支援與否

透過確認全域變數Storage的data type,來確認使用者的瀏覽器是否支援LocalStorage:
(注意: typeOf()回傳的是字串)
```javascript
if(typeOf(Storage) !== “undefined”){
// put code here…
}else{
Alert(“Your browser doesn’t support LocalStorage!”);
}
```
(2)方法實做

在瀏覽器中存取資料的效果，主要透過兩個方法來實現:
» LocalStorage.setItem( {key} , {data} )
» LocalStorage.getItem( {key} , {data} )

LocalStorage可存放多筆資料，用各自獨一無二的Key來作為取出和讀取的依據。

在實做上，一開始載入時會確認LocalStorage裡是否有存放資料。
若有，便存入變數中; 反之，則存入空值，如:
```javascript
var data = LocalStorage.getItem(“myData”) | null;
```
新增更改或刪除資料時，則將新的資料存入LocalStorage中:
```javascript
// after adding, editing or deleting data
LocalStorage.setItem(“myData”,data);
```
如此透過簡單的API便可以輕鬆地使用LocalStorage了。

參考資料:
- [w3c介紹](https://www.w3schools.com/html/html5_webstorage.asp)  
- [瀏覽器支援表](https://caniuse.com/#search=LocalStorage)