---
layout: post
title: "[學習筆記 | 基礎資料結構] Queue-使用Javascript"
author: "Yumi Chen"
categories: dataStructure
tags: [Javascript,data structure]
---
<iframe height="315" src="https://www.youtube.com/embed/bK7I79hcm08" frameborder="0" allowfullscreen></iframe>
  
[程式碼來源/ 教學程式碼](https://codepen.io/beaucarnes/pen/QpaQRG?editors=0012)
  

## 概念簡述
- 先進後出(First in last out), 就像是演唱會入場的排隊隊伍，先排隊的人可以先進入演唱會會場(離開隊伍)
- 影片中介紹了兩種Queue: Queue及Priority Queue，Priority Queue不同的地方是元素排序依據並非加入順序，而是各元素的權重(Priority)屬性，權重愈重的元素會被排在愈後方，刪除元素時也首先會從權重低的元素開始。

## 基礎結構
1. Queue方法
- print  印出所有元素
- enqueue  加入新元素
- dequeue  刪除最後加入的元素
- front  查看頂端/最後加入的元素
- size Queue元素總數
- isEmpty 是否有儲存元素
  
2. Priority Queue方法
- printCollection  印出所有元素
- enqueue  加入新元素
- dequeue  刪除最後加入的元素
- front  查看頂端/最後加入的元素
- size Queue元素總數
- isEmpty 是否有儲存元素
  
## 實作步驟
- Queue
1. 建立物件，加入collection屬性
```javascript
var Queue = function() {
    collection = []; // Queue元素
}
```
  
2. 實作print方法
```javascript
...
    this.print = function() {
        console.log(collection);
    };
...
```

3. 實作enqueue方法
```javascript
...
    this.enqueue = function(element) {
        collection.push(element);
    };
...
```

4. 實作dequeue方法
```javascript
...
    this.dequeue = function() {
        return collection.shift(); 
    };
...
```

5. 實作front方法
```javascript
...
    this.front = function() {
        return collection[0];
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

7. 實作isEmpty方法
```javascript
...
    this.isEmpty = function() {
        return (collection.length === 0); 
    };
...
```

8. 即完成,完整程式碼如下:
```javascript
function Queue () { 
    collection = [];

    this.print = function() {
        console.log(collection);
    };
    
    this.enqueue = function(element) {
        collection.push(element);
    };
    
    this.dequeue = function() {
        return collection.shift(); 
    };
    
    this.front = function() {
        return collection[0];
    };
    
    this.size = function() {
        return collection.length; 
    };
    
    this.isEmpty = function() {
        return (collection.length === 0); 
    };
}
```

- Priority Queue  
Priority Queue方法實作與Queue大致相同，唯一不同的是enqueue方法。  

```javascript
...
    this.enqueue = function(element){
        if (this.isEmpty()){ 
            collection.push(element);
        } else {
            var added = false;
            for (var i=0; i<collection.length; i++){
                 if (element[1] < collection[i][1]){ //checking priorities
                    collection.splice(i,0,element);
                    added = true;
                    break;
                }
            }
            if (!added){
                collection.push(element);
            }
        }
    };
...
```
  
修改後完整程式碼如下:
```javascript
function Queue () { 
    collection = [];

    this.print = function() {
        console.log(collection);
    };
    
    this.enqueue = function(element){
        if (this.isEmpty()){ 
            collection.push(element);
        } else {
            var added = false;
            for (var i=0; i<collection.length; i++){
                 if (element[1] < collection[i][1]){ //checking priorities
                    collection.splice(i,0,element);
                    added = true;
                    break;
                }
            }
            if (!added){
                collection.push(element);
            }
        }
    };
    
    this.dequeue = function() {
        return collection.shift(); 
    };
    
    this.front = function() {
        return collection[0];
    };
    
    this.size = function() {
        return collection.length; 
    };
    
    this.isEmpty = function() {
        return (collection.length === 0); 
    };
}
```

  
## 使用範例
- Queue
```javascript
    var q = new Queue(); 

    q.enqueue('a'); 
    q.enqueue('b');
    q.enqueue('c');
    q.print();
    q.dequeue();
    console.log(q.front());
    q.print();

  // 結果
  // ["a", "b", "c"]
  // "b"
  // ["b", "c"]
```  

- Priority Queue
```javascript
    var pq = new PriorityQueue(); 

    pq.enqueue(['Beau Carnes', 2]); 
    pq.enqueue(['Quincy Larson', 3]);
    pq.enqueue(['Ewa Mitulska-Wójcik', 1])
    pq.enqueue(['Briana Swift', 2])
    pq.printCollection();
    pq.dequeue();
    console.log(pq.front());
    pq.printCollection();

  // 結果
  // [[Ewa Mitulska-Wójcik,1],[Beau Carnes,2],[Briana Swift,2],[Quincy Larson,3]]
  // ["Beau Carnes", 2]
  // [[Beau Carnes,2],[Briana Swift,2],[Quincy Larson,3]]
```  
