---
title: 六角node語法筆記
date: 2021-07-16 14:53:19
categories: [程式]
tags: [nodeJS]
---

### 找到firebase目錄

```js
firebase.database().ref();
```
<!-- more -->

### 新增值
```js
firebase.database().ref().set();
```
### 查值
```js
firebase.database().ref().once('value', function(snapshop){});
```

### 刪值
```js
firebase.database().ref().child().remove();
```

### 排序
```js
firebase.database().ref().orderByChild('weight').once('value', function(snapshop){
  // 排序要搭配forEach
  snapshop.forEach(function(itme){
    console.log(item.val());
  })
});
```

### 查範圍
```js
// startAt()找3000以上 endAt()4500以下，equalTo(2000)
firebase.database().ref().orderByChild('weight').startAt(3000).endAt(4500).once('value', function(snapshop){
  // 排序要搭配forEach
  snapshop.forEach(function(itme){
    // 抓值
    console.log(item.val());
    //抓key
    console.log(item.key);
  })
});
```

### 要撈出筆數
```js
// limitToFirst(1) 從前面撈出第一筆 limitToLast 從最後面撈最後一筆
firebase.database().ref().orderByChild('weight').startAt(3000).limitToFirst(1).once('value', function(snapshop){
  snapshop.forEach(function(itme){
    // 抓值
    console.log(item.val());
  })
});
```
### express 路由參數params, :name可自訂
```js
app.get('/user/:name',function(req,res){
  var myName = req.params.name;
  console.log(req.query);// 可印出來看看 在網址後加?
  if(myName!== 'tom'){
      res.send('<html><head></head><body><h1>'+ '查無此人' +'</h1></body></html>');
  }else{
      res.send('<html><head></head><body><h1>'+ myName +'</h1></body></html>');
  }
})
```
### 守門員 middleware
```js
app.use(function(req,res,next){
  if(req.url !== '/'){
      res.send('查無此網址')
  }else{
      next();
  }
});
```
### 轉址
```js
res.redirect('/user');
```
### 抓目錄路徑
```js
path.dirname('/xx/yy/zz.js') // 回傳 /xx/yy
```
### 路徑合併
```js
path.join(__dirname,'/xx') // 回傳 前後路徑合併
```
### 抓檔名
```js
path.basename('/xx/yy/zz.js') // 回傳 zz.js
```
### 抓副檔名
```js
path.extname('/xx/yy/zz.js') // 回傳 js
```
### 分析路徑
```js
path.parse('/xx/yy/zz.js') // 回傳 上述綜合物件
```


