## JQuery란?

JavaScript의 생산성을 향상시켜주는 JavaScript *라이브러리

(*라이브러리: 자주 사용되는 로직들의 묶음으로 재활용, 유통가능하도록 한다.)


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
