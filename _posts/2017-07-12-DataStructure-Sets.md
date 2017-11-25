---
layout: post
title: "[學習筆記 | 基礎資料結構] Sets-使用Javascript"
author: "Yumi Chen"
categories: dataStructure
tags: [Javascript,data structure]
---

<iframe height="315" src="https://www.youtube.com/embed/wl8u02IdVxo" frameborder="0" allowfullscreen></iframe>
  
[程式碼來源/ 教學程式碼](https://codepen.io/beaucarnes/pen/dvGeeq?editors=0012)
  

## 概念簡述
- Sets是無順序，無重複元素的集合
  

## 基礎結構
Javascript裡已實作Set物件，但仍可自己實作Set

1. Javascript內建Set的使用範例 
```javascript
    var setC = new Set();  
    var setD = new Set();  
    setC.add("a");  
    setD.add("b");  
    setD.add("c");  
    setD.add("a");  
    setD.add("d");  
    console.log(setD.values())
    setD.delete("a");
    console.log(setD.has("a"));
    console.log(setD.add("d"));

    // [object Set Iterator] {}
    // false
    // [object Set] {}
```

2. Sets方法
- has 確認是否擁有否元素
- values 回傳所有儲存的元素
- add  加入新元素
- remove  刪除特定元素
- size  儲存元素總數
- union  回傳兩個Set所有元素的集合
- intersetion 回傳兩個Set相同元素的集合
- difference 回傳兩個Set相異元素集合
- subset 確認某Set是否包含某Set所有元素
  
## 實作步驟
1. 建立物件，加入collection變數
```javascript
var Stack = function() {
    var collection = [];
}
```
  
2. 實作has方法
```javascript
...
    this.has = function(element) {
        return (collection.indexOf(element) !== -1);
    };
...
```

3. 實作values方法
```javascript
...
    this.values = function() {
        return collection;
    };
...
```

4. 實作add方法
```javascript
...
    this.add = function(element) {
        if(!this.has(element)){
            collection.push(element);
            return true;
        }
        return false;
    };
...
```

5. 實作remove方法
```javascript
...
    this.remove = function(element) {
        if(this.has(element)){
            index = collection.indexOf(element);
            collection.splice(index,1);
            return true;
        }
        return false;
    };
...
```
6. 實作size方法
```javascript
...
    this.size = function() {
        return collection.length;
    };
...
```

7. 實作union方法
```javascript
...
    this.union = function(otherSet) {
        var unionSet = new mySet();
        var firstSet = this.values();
        var secondSet = otherSet.values();
        firstSet.forEach(function(e){
            unionSet.add(e);
        });
        secondSet.forEach(function(e){
            unionSet.add(e);
        });
        return unionSet;
    };
...
```

8. 實作intersection方法
```javascript
...
    this.intersection = function(otherSet) {
        var intersectionSet = new mySet();
        var firstSet = this.values();
        firstSet.forEach(function(e){
            if(otherSet.has(e)){
                intersectionSet.add(e);
            }
        });
        return intersectionSet;
    };
...
```
9. 實作difference方法
```javascript
...
    this.difference = function(otherSet) {
        var differenceSet = new mySet();
        var firstSet = this.values();
        firstSet.forEach(function(e){
            if(!otherSet.has(e)){
                differenceSet.add(e);
            }
        });
        return differenceSet;
    };
...
```
10. 實作subset方法
```javascript
...
    this.subset = function(otherSet) {
        var firstSet = this.values();
        return firstSet.every(function(value) {
          return otherSet.has(value);
        });
    };
...
```

11. 即完成,完整程式碼如下:
```javascript
function mySet() {
    // the var collection will hold the set
    var collection = [];
    // this method will check for the presence of an element and return true or false
    this.has = function(element) {
        return (collection.indexOf(element) !== -1);
    };
    // this method will return all the values in the set
    this.values = function() {
        return collection;
    };
    // this method will add an element to the set
    this.add = function(element) {
        if(!this.has(element)){
            collection.push(element);
            return true;
        }
        return false;
    };
    // this method will remove an element from a set
    this.remove = function(element) {
        if(this.has(element)){
            index = collection.indexOf(element);
            collection.splice(index,1);
            return true;
        }
        return false;
    };
    // this method will return the size of the collection
    this.size = function() {
        return collection.length;
    };
    // this method will return the union of two sets
    this.union = function(otherSet) {
        var unionSet = new mySet();
        var firstSet = this.values();
        var secondSet = otherSet.values();
        firstSet.forEach(function(e){
            unionSet.add(e);
        });
        secondSet.forEach(function(e){
            unionSet.add(e);
        });
        return unionSet;
    };
    // this method will return the intersection of two sets as a new set
    this.intersection = function(otherSet) {
        var intersectionSet = new mySet();
        var firstSet = this.values();
        firstSet.forEach(function(e){
            if(otherSet.has(e)){
                intersectionSet.add(e);
            }
        });
        return intersectionSet;
    };
    // this method will return the difference of two sets as a new set
    this.difference = function(otherSet) {
        var differenceSet = new mySet();
        var firstSet = this.values();
        firstSet.forEach(function(e){
            if(!otherSet.has(e)){
                differenceSet.add(e);
            }
        });
        return differenceSet;
    };
    // this method will test if the set is a subset of a different set
    this.subset = function(otherSet) {
        var firstSet = this.values();
        return firstSet.every(function(value) {
          return otherSet.has(value);
        });
    };
}
```


  
## 使用範例
```javascript
  var setA = new mySet();  
  var setB = new mySet();  
  setA.add("a");  
  setB.add("b");  
  setB.add("c");  
  setB.add("a");  
  setB.add("d");  
  console.log(setA.subset(setB));
  console.log(setA.intersection(setB).values());
  console.log(setB.difference(setA).values());

  // 結果
  // true
  // ["a"]
  // ["b", "c", "d"]
```

