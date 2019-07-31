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


## Wrapper[래퍼]란?
'element오브젝트_body |css 선택자'를 감싸는 jQuery( ... )을 의미


### 래퍼의 안전한 사용을 위해서
$(엘리먼트)와 JQuery(element)는 같은 의미지만, $를 사용하는 다른 라이브러리들의 충돌을 막기위해서 다음과 같이 JQuery와 $를 작성한다.
> 1.JQuery(element)를 사용하는 경우
```
 <script type="text/javascript">
      jQuery('body').html('hello');
  </script>
```
> 2.function안에서 $(엘리먼트)를 사용하는 경우
```
<script type="text/javascript">
(function($){
    $('body').html('hello');
      })(jQuery)
  </script>
```

### Tip. script의 위치
> 1.head에 위치한 경우  
간단한 설정, JavaScript 라이브러리 import시 사용.  
> 2.body에 위치한 경우  
대부분의 경우, script는 body내부에 위치함.


## Selector(선택자) 란?
JQuery wrapper 안에는 CSS 선택자가 위치 할수 있는데, 이를 통해서 엘리먼트를 빠르고 정확하게 지정할 수 있다.

> 1. Wildcard Selector(전체 선택자) _ *
:HTML 페이지에 있는 모든 문서 객체를 선택.
```
<script scr="jquery-1.10.2.js"></script>
<script type ="text/javascript>
        $(document).ready(function(){
                $('*').css('color','red');
        });
</script>
```
$('*')의 선택자, .css('color','red')메서드로 구성 됌.


> 2. Tag Selector _ 태그명
:특정한 태그를 선택.
```
<script scr="jquery-1.10.2.js"></script>
<script type ="text/javascript>
        $(document).ready(function(){
                $('h1').css('color','red');
        });
</script>
```


> 3. Id Selector _ #아이디명
:특정한 id속성이 있는 문서 객체를 선택.
```
<head>
...
<script scr="jquery-1.10.2.js"></script>
<script type ="text/javascript>
        $(document).ready(function(){
                $('h1#아이디명').css('color','red');
        });
</script>
</head>
<body>
    <h1 id="header1">Header</h1>
</body>      
```


> 4. Class Selector _ .클래스명
:특정한 class속성이 있는 문서 객체를 선택.
```
<head>
...
<script scr="jquery-1.10.2.js"></script>
<script type ="text/javascript>
        $(document).ready(function(){
                $('h1.item').css('color','red');
                $('.item1, .item2').css('color','blue');
        });
</script>
</head>
<body> 
    <h1 class="item1">Header1</h1>
    <h1 class="item1">Header2</h1>
    <h1 class="item">Header3</h1>
</body>      
```
body를 기준으로 출력됌.  
결과: red(Header1)->red(Header2)->blue(Header3)


## Chain이란?
JQuery의 메소드들은 자기 자신을 반환해야 한다는 규칙이 있다.
이를 이용해서, 한번 선택한 대상에 대해서 연속적인 제어를 할수 있다.

> Chain의 장점
-코드의 간결화
-인간의 언어와 유사해서, 사고의 자연스러운 과정과 일치함.
