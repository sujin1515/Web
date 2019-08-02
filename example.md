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

## 기본 형식
```
$(document).ready(function(){
       //code here.(변수/함수/EventHandler...등등 작성)->JQuery의 내용
       
});
```
=단축형태
```
$(function(){
       //code here.(변수/함수/EventHandler...등등 작성)->JQuery의 내용
       
});
```


Example
```
<script>
$(document).ready(function(){
      $("button").click(function(){
        $("h1").hide("slow");
        $("h2").hide("fast");
        $("img").slideUp();
     }); 
});
</script>
```
$("selector").jQuery명령문|메서드로 내용이 구성됌


[참조]
![selector](https://user-images.githubusercontent.com/42289304/62188045-2ea4b500-b3a6-11e9-9094-3fec6cd76c4b.png)


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
                $('h1#header1_아이디명').css('color','red');
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

간단히 표현하자면 다음과 같다.

![selector](https://user-images.githubusercontent.com/42289304/62188045-2ea4b500-b3a6-11e9-9094-3fec6cd76c4b.png)



## Chain이란?
JQuery의 메소드들은 자기 자신을 반환해야 한다는 규칙이 있다.
** 이를 이용해서, 한번 선택한 대상에 대해서 연속적인 제어를 할 수 있다.

> Chain의 장점  
-코드의 간결화  
-인간의 언어와 유사해서, 사고의 자연스러운 과정과 일치함.  
> 1. JQuery의 경우  
```html
<html>
        <body>
            <a id ="tutorial" hrdf="http://jquery.com" target="_self">jQuery</a>
            <script type="text/javascript" src ="https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js"></script>
                <script type="text/javascript">
                    jQuery('#tutorial').attr('href', 'http://jquery.org').attr('target', '_blank').css('color', 'red');
            </script>
    </body>
</html>
```
한번 선택한 대상에 대해서 연속적으로 제어(.attr/.css /.메서드/...)를 한다. => 메서드Chain  

대상.메서드();

> 2. JavaScript의 경우  
```html
<html>
        <body>
            <a id ="tutorial" hrdf="http://jquery.com" target="_self">jQuery</a>
            <script type="text/javascript">
                var tutorial=document.getElementById('tutorial');
                tutorial.setAttribute('href', 'http://jquery.org');
                tutorial.setAttribute('target', '_blank');
                tutorial.style.color='red';
            </script>
    </body>
</html>
```
한번 선택한 대상에 대해서 연속적으로 제어(setAttribute)를 한다. => Chain과 같다 


### Traversing(탐색)
:chain 의 대상을 바꿔서 체인을 계속 연장시킬 수 있는 방법  


예제) JQuery의 경우 
```html
<script type="text/javascript">
                    jQuery('#tutorial').find('.foo').css('color', 'red').end().find('.bar')..css('color', 'blue');
 </script>
```
find대상 -> 메서드 적용 -> end -> find대상 -> 메서드 적용-> ... 

#### 메서드


| 메서드 | 설명|
:----: |----
|children()| 선택된 노드의 모든 자식노드만 선택한다.|
|find()|선택한 노드의 조건에 맞는 자식노드를 선택한다.|
|next()|선택한 노드의 다음 노드를 선택한다.|
|nextAll()|선택한 노드의 다음 모든 노드를 선택한다.|
|parent()|선택한 노드의 부모 노드를 선택한다.|
|parendts()|선택한 노드의 모든 부모 노드를 선택한다.|
|prev()|선택한 노드의 이전 노드를 선택한다.|
|prevAll()|선택한 노드의 모든 이전 노드를 선택한다.|
|closest()|선택한 노드를 포함하면서 가장 가까운 상위 노드를 선택한다.|
|nextUntil()|다음에 위치한 노드를 조건에 맞을 때까지 찾는다.|
|parentsUntil()|조건이 참이 될 때까지 부모 노드를 찾는다.|
|prevUntil()|이전에 위치한 노드를 조건에 맞을 때까지 찾는다.|
|siblings()|형제 노드들을 모두 찾는다.|


## Event 란?
시스템에서 일어나는 사건을 의미.  
-JavaScript, JQuery에게 Event란 브라우져에서 일어나는 사건(ex)click, typing, page loading, mouse moving)  
-해당 Event가 발생시, 시스템은 작성해둔 로직을 호출한다.  

-> 즉, 사용자의 동작(Event)이 발행하면, 작성해둔 함수|EventHandler(로직)을 진행한다.

Example
```
<script>
$(document).ready(function(){
      $("button").click(function(){
        $("h1").hide("slow"); //hide 메서드
        $("h2").hide("fast");//hide 메서드
        $("img").slideUp();//slidUp 메서드(올라오는 효과)
     }); 
});
</script>
```
=단축 표기시,
```
<script>
$function(){
      $("button").click(function(){
        $("h1").hide("slow"); //hide 메서드
        $("h2").hide("fast");//hide 메서드
        $("img").slideUp();//slidUp 메서드(올라오는 효과)
     }); 
});
</script>
```

## JQuery의 이벤트
-bind로 eventHandler를 설치 /unbind로 제거  
-trigger로 eventHandler를 강제실행

```html
<html>
    <head>
        <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js"></script>
        <script type="text/javascript">
            function clickHandler(e){
                alert('thank you');
            }
            $(document).ready(function(){
                 $('#click_me').click(clickHandler);
                 $('#remove_event').click(function(e){
                     $('#click_me').unbind('click', clickHandler);
                 });
                 $('#trigger_event').click(function(e){
                     $('#click_me').trigger('click');
                 });
             })
        </script>
    </head>
    <body>
        <input id="click_me" type="button" value="click me" />
        <input id="remove_event" type="button" value="unbind" />
        <input id="trigger_event" type="button" value="trigger" />
    </body>
</html>
```
주의사항)''싱글과 ""더블 구분하기                     
## Element제어


| Element제어 | 해당 요소|
:----: |----
자식으로 삽입|.append() .appendTo() .html() .prepend() .prependTo() .text()|
형제로 삽입| .after() .before() .insertAfter() .insertBefore()|
부모로 감싸기|.unwrap() .wrap() .wrapAll() .wrapInner()|
삭제| .detach() .empty() .remove() .unwrap()|
치환| .replaceAll() replaceWith()|
클래스| .addClass() .hasClass() .removeClass() .toggleClass()|
속성제어| .attr() .prop() .removeAttr() .remoceProp() .val()|


.attr(): 선택된 요소집합의 첫번째요소에 대해 **속성값 가져오거나 or 선택된 모든 요소에 대해서 속성을 설정.**   
.val() : 폼 요소들에 대해서 일치하는/ 요소집합의 첫번째요소에 대해 **현재값 가져오거나 or 일치하는 모든 요소에 대해서 값을 설정.**  

## Form 이란?  
-서버로 데이터를 전송하기 위한 수단  
- JQuery는 form을 제어하는데 필요한 이벤트와 메소드 제공

예제 [.focuse() .blur() .change() .select()]
```html
<!DOCTYPE html>
<html>
    <head>
                <style>
                    span{
                    
                    }
               </style>
               <script src="http://code.jquery.com/jquery-latest.js"></script>
    </head>
    <body>
        <p>
            <input type="text"/>
            <span></span>
        </p>
        <script>
            $("input").focuse(function (){
                $(this).next("span").html('focus');
            }).blur(function (){
                $(this).next("span").html('blur');
            }).change(function() {
                 alert('change!' +$(e.target).val();
            }).select(function (){
                $(this).next("span").html('select');
            });
        </script>
    </body>
</html>
```  


예제 [.submit() .val()]
```html
<!DOCTYPE html>
<html>

    <head>
        <style>
            p{
                margin:0;
                color:blue;
            }
            div, p{
                margin-left:10px;
            }
            span{
                color:red;
            }
        </style>
        <script src="http://code.jquery.com/jquery-latest.js"></script>
    </head>

    <body>
        <p>
            Type 'correct' to validate.
        </p>
        <form acton ="javadscript:alert('success!');">
            <div>
                <input type ="text"/>
                <input type ="submit"/>
            </div>
        </form>
        <span></spane>

        <script>
            $("form").submit(function(){
                if($("input:first").val() =="correct"){
                    $("span").text("Validated..").show();
                    return true;
                }
                $("span").text("Not valid!").show().fadeout(1000);
                    return false;
            });
        </script>
    </body>
</html>
```
form영역 ->form 태그(element)대상에 submit(명령어)이벤트 발생시,   
if 입력이 correct문자열과 동일하다면, span태그 영역에 Vaildated text show하기(event Handler내용) &return true;  
if문에 걸리지 않는다면, span태그 영역에 Not valid! text show->fadeout효과(event Handler내용) &return false;  


## 애니메이션 이란?
-JavaScript와 CSS를 이용해서 HTML elemnent에 동적일 효과를 줌.  
-JQuery는 효과 메소드를 호출해서 효과를 줌.  
ex) click이벤트 핸들러 안에 animate함수를 연동해서 애니메이션 효과를 줌.  

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            div{
                background-color:#bca;
                width:100px;
                border:1px solid green;
            }
        </style>
        <script src="http://code.jquery.com/jquery-latest.js"></script>
    </head>
    <body>
        <button id="run">
            &raquo; Run
        </button>
        <div id="block">
            Hello!
        </div>
        <script>
            $("#run").click(function() {
                $("#block").animate({
                width:"300px",
                opacity:0.4,
                marginLeft:"50px",
                fontSize:"30px",
                borderWidth:"10px"
            }, 3000);
       });
        </script>
    </body>
</html>
```
run버튼 click이벤트가 발생시, block(element)대상에 .animate(명령어)를 실행한다.[click eventHandler 처리]


## Ajax란?
(Asynchronous JavaScript and Xml)
JavaScript를 이용해서 **비동기식**으로 서버와 통신하는 방식, 이때 XML을 이용.   
[최근에는 XML대신에 JSON을 많이 이용]  
* 비동기식: 여러가지일이 동시적으로 처리될수 있는 것 의미. 서버와 통신하는 동안 다른 작업을 할 수 있다는 의미.  
즉, 화면전체를 갱신하지 않고 **페이지의 일부만(json, xml형태의 필요한 data) 갱신하고도** 동일한 화면표시효과를 나타낼 수 있음.  


### Ajax 기본형식
```html
<script>
    ...
    $.ajax({
        url:'호출할 URL',
        dataType:'서버가 리턴하는 데이터 타입 ex)xml, json, script, html',
        type:'서버로 전송하는 데이터의 타입 ex)GET, POST',
        data:{서버에 전송 할 데이터, key/vlaue 형식의 객체},
        success:function(result){
            ajax통신을 성공했을때, 호출될 eventHandler
        }
    });
</script>
```
즉, browser --------------------------->서버  
      보내는 정보[data],전송타입[type] 
    browser <---------------------------서버  
     [url]페이지로 이동해서 데이터를 처리하고, 받는데이터(필요정보for. 일부갱신)타입[dataType]    
     -다시 현페이지(brower)에 돌아와서, 페이지 일부 만을 갱신함.   
     ->이러한 비동기 통신이 성공한경우, [success]에 기재된 eventHandler를 실행함.      
       

Example. 웹페이지
```html
<!DOCTYPE html>
<html>
       <head>
            <script src="http://code.jquery.com/jquery-latest.js"></script>
       </head>
        <body>
            <div id ="result"></div>
            <input type="text" id="img"/>
            <input type ="text" value="get result" id="getResult">
            <script>
                $('#getResult').click(function(){
                    $('#result).html('');
                    $.ajax({
                        url:'http://opentutorials.org/example/jquery/example.jquery.ajax.php',
                        data:'json',
                        type:'POST',
                        data:{'msg':$('#msg').val()},
                        success:function(result){
                            if(result['result'] ==true){
                                $('#result').html(result['msg']);
                                }
                            }
                   });
               })
            </script>
    </body>
</html>
```


Example. server 로직    
 ```
 <?
    echo json_encode(array('result' => true, 'msg'=>$_REQUEST['msg']));
 ?>
 ```
 
주의사항) 현재 url에 파일이 없으므로 해당예제는 작동하지 않을 것이다. 하지만 해당예제를 통해 Ajax의 작성방식을 익혀두자  
 
 
