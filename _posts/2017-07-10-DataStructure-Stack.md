---
layout: post
title: "[學習筆記 | 基礎資料結構] Stack-使用Javascript"
author: "Yumi Chen"
categories: dataStructure
tags: [Javascript,data structure]
---

<iframe height="315" src="https://www.youtube.com/embed/Gj5qBheGOEo" frameborder="0" allowfullscreen></iframe>
  
[程式碼來源/ 教學程式碼](https://codepen.io/beaucarnes/pen/yMBGbR?editors=0012)
  

## 概念簡述
- 先進先出(First in first out), 可以想像成在常柱狀盒子裡投入馬卡龍，包裝完成後須取出時，最後放入的會是最先可以拿出來的
- 瀏覽器上一頁，下一頁的歷史紀錄即是使用Stack實作
  

## 基礎結構
Javascript裡的陣列已實作Stack(有push, pop等方法)，但仍可自己實作Stack

1. 課程中使用Palindrome範例示範了Javascript陣列Stack的特性  
```javascript
    // 陣列, Stack
    var letters = []; // this is our stack

    // 要確認的單字
    var word = "freeCodeCamp"

    // 儲存反轉後字母的變數
    var rword = "";

    // put letters of word into stack
    // 將字母由前至後依序放入Stack
    for (var i = 0; i < word.length; i++) {
    letters.push(word[i]);
    }

    // pop off the stack in reverse order
    // 將陣列的元素從後開始一一刪除
    for (var i = 0; i < word.length; i++) {
    rword += letters.pop(); 
    // pop執行完畢後回傳被刪除的元素
    }

    if (rword === word) {
    console.log(word + " is a palindrome.");
    }
    else {
    console.log(word + " is not a palindrome.");
    }
```

2. Stack方法
- push  加入新元素
- pop  刪除最後加入的元素
- peek  查看頂端/最後加入的元素
- size  Stack元素總數, 陣列長度

  
## 實作步驟
1. 建立物件，加入count和storage屬性
```javascript
var Stack = function() {
    this.count = 0;  // Stack長度
    this.storage = {};  // Stack元素
}
```
  
2. 實作push方法
```javascript
...
    this.push = function(value) {
        this.storage[this.count] = value;
        this.count++;
    }
...
```

3. 實作pop方法
```javascript
...
    this.pop = function() {
        if (this.count === 0) {
            return undefined;
        }

        this.count--;
        var result = this.storage[this.count];
        delete this.storage[this.count];
        return result;
    }
...
```

4. 實作size方法
```javascript
...
    this.size = function() {
      return this.count;
    }
...
```

5. 實作peek方法
```javascript
...
    this.peek = function() {
        return this.storage[this.count-1];
    }
...
```
6. 即完成,完整程式碼如下:
```javascript
var Stack = function() {
    this.count = 0;  // Stack長度
    this.storage = {};  // Stack元素
    
    // push
    this.push = function(value) {
        this.storage[this.count] = value;
        this.count++;
    }

    // pop
        this.pop = function() {
        if (this.count === 0) {
            return undefined;
        }

        this.count--;
        var result = this.storage[this.count];
        delete this.storage[this.count];
        return result;
    }
    
    this.size = function() {
        return this.count;
    }

    // size
    this.size = function() {
      return this.count;
    }

    // peek
    this.peek = function() {
        return this.storage[this.count-1];
    }
}
```


  
## 使用範例
```javascript
  var myStack = new Stack();

  myStack.push(1);
  myStack.push(2);
  console.log(myStack.peek());
  console.log(myStack.pop());
  console.log(myStack.peek());
  myStack.push("freeCodeCamp");
  console.log(myStack.size());
  console.log(myStack.peek());
  console.log(myStack.pop());
  console.log(myStack.peek());

  // 結果
  // "freeCodeCamp is not a palindrome."
  // 2
  // 2
  // 1
  // 2
  // "freeCodeCamp"
  // "freeCodeCamp"
  // 1
```

