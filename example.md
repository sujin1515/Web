## JQuery란?

JavaScript의 생산성을 향상시켜주는 JavaScript 라이브러리

[*라이브러리:자주 사용되는 코드들/로직들의 묶음형태로 가공해서, 재활용/유통의 효율을 높여주는 코드들]


## 사용법
>1.직접 서비스하는 경우  
>1.http://jquery.org에서 소스코드 download.  
>2.해당 파일을 서버에 업로드 한 후 웹페이지에 javaScript를 삽입하기.  

>2.구글의 JavaScript 라이브러리를 사용하는 경우  
>1.http://code.google.com/intl/ko-KR/apis/libraries/devguide.html#jquery  
```html
<html>
    <body>
        <div class="Welcome"></div>
        <div class="Welcome"></div>
        <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js"></script>
        <script type="text/javascript"> 
              $('.welcome').html('hello world!').css('background-color', 'yellow');
         </script>
     </body>
</html>
```
## JavaScript 와 JQuery 비교
탭을 클릭시, 포커스를 변경하는 예제코드(2가지 version)
### 1. JavaScript
```html
<html>
  <head>
  <script type="text/javascript">
    function addEvent(target, eventType, eventHandler, userCapture){
    if(target.addEventListener){
      target.addEventListener(eventType, eventHandler, userCapture? userCapture:false);
      
    }else if(target.attachEvent){
      var r =target.attachEvent("on"+eventType, eventHandler);
    }
  }

  function clickHandler(event){
    var nav =document.getElementById('navigation');
    for(var i=0; i<nav.childNodes.length;i++)
    {
      var child=nav.childNodes[i]; 
      if(child.nodeType==3)
        continue;
      child.className ='';
    }
    event.target.className ='selected';
  }
  addEvent(window, 'load', function(eventObj){
      var nav =document.getElementById('navigation');
      for(var i=0; i<nav.childNodes.length;i++){
        var child=nav.childNodes[i];
        if(child.nodeType ==3)
          continue;
       addEvent(child,'click',clickHAndler);
      }
  })
  </script>
  </head>

//동일구간
  <body>
       <ul id="navigation">
           <li>HTML</li>
           <li>CSS</li>
           <li>javascript</li>
           <li class="selected">jQuery</li>
           <li>PHP</li>
           <li>mysql</li>
       </ul>
   </body>
</html>
```  


### 2. JQuery  
```html
<html>
  <head>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js"><script>
    <script type="text/javascript">
      $('#navigation li').on('click', function(){  //이벤트 핸들러
          $('#navigation li').removeClass('selected');
          $(this).addClass('selected');
      })
        
      </script>
      </head>
      <body>
        <ul id="navigation">
            <li>HTML</li>
            <li>CSS</li>
            <li>javascript</li>
            <li class="selected">jQuery</li>
            <li>PHP</li>
            <li>mysql</li>
        </ul>
    </body>
</html>
```  

javascript의 이벤트 핸들러사용의 번거로움을 jquery의 경우 간편하게 표현가능하다.


## [참고 정보]
### $와 JQuery의 사용법 비교
> 1.function안에서 $(엘리먼트)를 사용하는 경우
```
$('#navigation li').on('click', function(){  //이벤트 핸들러
          $('#navigation li').removeClass('selected');
          ...
      }))
```
 > 2.JQuery(element)를 사용하는 경우
 ```
      jQuery('#navigation li').removeClass('selected');
```
### script의 위치
> 1.<head>에 위치한 경우
간단한 설정, JavaScript 라이브러리 import시 사용.
> 2.<body>에 위치한 경우
대부분의 경우, script는 body내부에 위치함.
