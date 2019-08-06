## Stream란?
:컬랙션/배열 등 저장요소를 참조하여 람다식을 적용하여 반복적으로 처리할 수 있도록 하는 기능
**사용법: Collections같은 객체 집합.스트림생성().중개연산().최종연산();**
  
### Example 1
```java
List <string names =Arrays.asList("jeong", "pro", "jdk", "java");
Stream <String> a =names.stream().filter(x-> x.contains("o");
```
결과: "jeong", "pro"만 담긴 a 스트림이 반환된다.

### Example 2
```java
List <string names =Arrays.asList("jeong", "pro", "jdk", "java");
names.parallerStream().map((x) -> {return x.concat("s");}).forEach(x -> System.out.println(x));
```
결과: jeongs, pros, jdks, javas이 출력된다. 
 


### 파일 I/O Stream 사용법 
```java
FileOutputStream fileout = null; //생성
      try{
           fileout =new FileOutputStream("./test.txt",true);  //현 디렉토리에  파일 생성, (true)덮어씌우기 옵션
    }

FileInputStream input = null;   //생성된 파일내용 일기
        try{
            // 화면에 표시하고자 하는 파일을 선택한다.
            File file = new File("c:\\example\\File\\umejintan_new.txt");  
            input = new FileInputStream(file);
            }
```
*주의사항 ) exception 다루기 =>try ,catch사용하기
