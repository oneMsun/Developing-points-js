### ajax的知识整理
##### ajax原理：
Ajax的原理简单来说通过XMLHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。这其中最关键的一步就是从服务器获得请求数据。

##### ajax实现的步骤：
1).创建XMLHTTPRequest对象<br/>
2).注册回调函数 xhr.onreadystatechange = callback;<br/>
3).设置和服务器端的链接信息。xhr.open(http请求方式（get，post）,url,设置异步或同步方式交互（true,false）);<br/>
4).发送数据开始交互。xhr.send(null); <br/>
5).接受响应数据。xhr.onload = function(){}

发送get请求实例：

```
searchBtn.onclick = function (){
    const xhr = new XMLHttpRequest();
    xhr.open('get', 'search_movie?search=' + encodeURIComponent(searchText.value), true);
    xhr.send();
    xhr.onload = function (){
      let imgData = JSON.parse(xhr.responseText);
     };
  };
```


发送post请求实例：

```
form2.btn.onclick = function (e){
      e.preventDefault();
      let json = {
        userName: form2.userName.value,
        passWord: form2.passWord.value
      };
      const xhr = new XMLHttpRequest();
      xhr.open('post', '/ajax_post_form', true);
      // 如果传的数据格式是一个JSON格式的，那么需要设置下面的请求头信息
      xhr.setRequestHeader('Content-Type', 'application/json');  
      // 如果是一个表单格式的 也就是 带 queryString
      // xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
      // 如果是json格式的，那么数据放在 send 方法中发送给后端
      xhr.send(JSON.stringify(json));  // 这里面的参数必须是一个标准的json
      // 如果是表单格式的，那么 send 的参数 为 空 就行了
      xhr.onload = function (){
        console.log(xhr.responseText);
      }
    }
```

##### Ajax的优点：
1）最大的一点是页面无刷新，在页面内与服务器通信，给用户的体验非常好。<br/>
2）使用异步方式与服务器通信，不需要打断用户的操作，具有更加迅速的响应能力。<br/>
3）把以前一些服务器负担的工作转嫁到客户端，利用客户端闲置的能力来处理，减轻服务器和带宽的负担，节约空间和宽带租用成    本。ajax的原则是“按需取数据”，可以最大程度的减少冗余请求，和响应对服务器造成的负担。

##### Ajax的一些面试问题：
1、说说对Ajax的理解，怎么实现局部刷新，怎么将获取到的JSON 数据在页面中显示出来，JSON 序列化成了字符串后应该怎么处理?
局部刷新：从服务器获得数据，然后用javascript来操作DOM而更新页面,如果返回的是JSON数据，<br/>
1). var str=xhr.responseText; 获取响应数据<br/>
2). var obj=JSON.parse(str); 解析JSON数据成为JS对象<br/>
3). 操作JS对象

##### jsonp
在客户端声明回调函数之后，客户端通过script标签向服务器跨域请求数据，然后服务端返回相应的数据并动态执行回调函数。


```
function jsonpCallback(result) {  
        //alert(result);  
        for(var i in result) {  
            alert(i+":"+result[i]);//循环输出a:1,b:2,etc.  
        }  
    }  
    var JSONP=document.createElement("script");  
    JSONP.type="text/javascript";  
    JSONP.src="http://crossdomain.com/services.php?callback=jsonpCallback";  
    document.getElementsByTagName("head")[0].appendChild(JSONP);
```
