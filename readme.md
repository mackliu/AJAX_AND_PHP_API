# AJAX 非同步的javascript及XML技術
在早期的網頁應用上，如果要取得更新後的資料，必須重新對伺服器再發一次請求(使用連結，F5，或表單傳送都算是對伺服器發出請求)，才能得到更新後的內容，這樣的過程如果遇到較慢的網路或是其它的網路狀況，會造成網頁呈現中斷並且無法操作的狀況，這會讓使用者的體驗非常不好，因此後來提出了這類非同步的技術，目的是不中斷主要頁面的呈現，讓不確定回應時間的資訊在背景去執行，等執行完畢後再回應到頁面上。

HTML原生就有XMLHttpRequest的方法可以用來實踐非同步的功能，後來HTML5又推出了FETCH的方法，可以簡化非同步請求的使用，除了原生的API，也陸續有第三方社群或開發者推出相應的函式庫供大眾使用，最有名的是jQuery的$.ajax系列方法，另外axios函式庫近年也愈來愈多人使用，甚至被vue.js列為建議的輔助函式庫。

---

## XML與JSON
早期的http傳輸資料以xml為主，在前後端收到資料後，需要去進行解析，才能進一步應用，後來又推出JSON格式，資料量比XML小，解析和應用也較方便，因此近年來的資料傳輸逐漸以JSON來取代XML，因此也有人改稱為AJAJ技術。

---

## XMLHttpRequest
XMLHttpRequest在2006年正式被W3C列入標準，也是目前所有瀏灠器都有支援的標準。

語法：
```javascript
//宣告XHR物件
var xhr=new XMLHttpRequest

//建立設定
xhr.open(
    Method,
    URL,
    async);

//處理回應
xhr.onload=function(){  
    var type=xhr.getResponseHeader(“Content-Type”);
    var status=xhr.status
    var response=xhr.responseText
    document.write(response)
}

//執行請求及傳送內容
xhr.send(context);

```
---

## Fetch
在2015年時推出，由主流的幾家瀏灠器所支援，包括Firefox與Chrome、Opera等，IE也宣布在後續的版本會支援Fetch，Fetch的最大特色是引入了Promise的概念，同時透過鏈式呼叫來改善語法結構。

語法：
```javascript
//建立請求
fetch(url,{method:’get’})
.then(function(response){
    
    return response.json()

}).then(function(data){
	
    console.log(data)

})
.catch(function(err){
    //error
})

```
---

## jQuery函式庫
jQuery最早只是重新包裝XMLHttpRequest的使用方法，推出比較容易操作的自訂函式供使用，不過後來也自行加入了延遲的概念，讓非同步的事件可以更容易的進行管理。

CDN：`https://code.jquery.com/`

語法：
```javascript
//$.ajax方法
$.ajax({
    type:get/post/patch/delete/update…,
    url:"http://.....",
    success: (callback),
    error: (callback),
    data:{json/xml/string},
    complete: (callback)
})

//$.get方法
$.get(url,data,callback)

//$.post方法
$.post(url,data,callback)

//().load()方法
$(selector).load(url)

```
---

## axios函式庫
axios是一個基於Promise標準而建立的非同步請求函式庫，除了提供簡便的語法操作外，由於axios只專注在非同步的請求上，因此整個函式庫相較jQuery小很多，也因此成為許多框架或是不想使用jQuery的使用者喜歡。

CDN：`https://cdnjs.com/libraries/axios`

語法：
```javascript
axios.get(url)
.then(function(response){

//處理回應

})
.catch(function(err){
//error

})

```

