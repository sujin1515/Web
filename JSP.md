## JSP




## JSTL(JSP Standard Tag Library)이란?
JSP에서 기본적으로 지원하는 태그형 표현식.

JSTL의 축약형 표현식 => *EL(Expression Language)


### *<EL 이란?> 
:자바코드가 아니라 스크립트 언어이다.  
${ } 표현법을 사용해서 범위를 정함.   


<<EL의 연산자>>
| 연산자 | 종류 |
:----: |----
|관계 연산자| >  <   =   ==   !=  lt  gt  ge  eq  ne|
|산술 연산자| +  -  *  /  %  div  mod|
|논리 연산자| &&  ||  !  and  or  not|
|타당성 검사| empty/not empty|

Example.
```
${empty memPointList }   //빈 여부 확인

${(x >= min) && (x <= max) 
```
DB에서 가져온 데이터를 표현하기 위해서,  JAVA의 경우 지정한 타입명으로 표현.
```java
//1
setAttribute(“name”, name);
//2
List list = (List)request.getAttribute("list"); 
list.get(0); 
```
=>**EL로 표현을 단순화하여 표현가능.**
```
//1
${name}
//2
${list["0"]}
```


## JSTL의 태그[JSTL 표기법]
## 1. c:out
변수의 값 출력. (즉, like.System.out.print의 역할)
```
<c:out value="${list.reg_date_format }"/>  
```
value를 출력/[El도 사용o]


## 2. c:set 
변수설정. (변수에 값/프로퍼티값 설정[jsp에서 setAttribute역할] )
```
<c:set var="title" value="제목 입니다." />
<c:out value="${title}" />
```
**<c:set>태그의 속성들**
- target 속성 : 프로퍼티를 설정할 빈 또는 맵을 가짐. [EL을 사용 o]ex)${map}
- property 속성 : 설정할 프로퍼티. [EL을 사용 o]ex)title
- var 속성 : (값이 저장되는) 변수명.
- value 속성 : 값 입력.  [EL을 사용 o] x)제목 입니다.
- scope 속성 : 변수가 저장된  Scope. page, request, session, application 을 가질 수 있고, 기본값은 page.


## 3. c.remove
설정한 변수를 제거.
```
<c:remove var="title" [scope="영역"] />
```
주의사항) 삭제할 변수의 scope을 지정하지 않을 경우, 동일한 이름의 모든영역의 변수를 모두삭제함.


## 4. 흐름제어
### <c:if>
```
<c:forEach items="${memPointList }" var="list" varStatus="row"> //list변수 선언
    <c:if test="${list.proc_gb eq '1'}">  //If 헤당 변수의proc_gb 속석이 1과 같다면
                ${list.add_nm }         //이문장을 실행.
    </c:if>
 </c:forEach> 
```
<c:if test="조건">  
...  
</c:if>  


### <c:forEach>
```
<c:forEach items="${memPointList }" var="list" varStatus="row">
...
</c:forEach> 
```
<c:forEach var="변수" itmes="아이템" [begin="시작번호"] [end=끝번호"] >  
...  
</c:forEach>  


### <c:choose> [like. switch]
```
<c:choose>
    <c:when test="${name eq '김철수'}"> ... </c:when>
    <c:when test="${name eq '박영희'}"> ... </c:when>
    <c:otherwise> ... </c:otherwise>
</c:choose>
```
<c:choose>  
    <c:when test="조건1"> ...실행문/out(출력)문... </c:when>  
    <c:when test="조건2"> ...실행문/out(출력)문... </c:when>  
    <c: otherwise> 위조건 모두 만족하지 않을때 실행문/out문 </c:otherwise>  
</c:choose>  

## 5. URL작동<c:url>
## 6. c:import를 통한 컨텐츠 삽입
```
<c:import url="http://media.daum.net/" charEncoding="euc-kr" var ="urlValue" scope="request"/>
    <c:param name="_top_G" value="news"/>
</c:import>
```
<c:import url="URL" charEncoding="읽어온 결과를 저장할때 사용할 인코딩" var ="읽어온 결과를 저장할 변수명" scope="변수를 저장할 영역"/>
    <c:param name="_top_G" value="news"/> //<c:param>태그는 지정url(사이트)에 연결할때, 전송할 파라미터를 입력한다.
</c:import>


## 7. 요청 redirection









