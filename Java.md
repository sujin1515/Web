## Stream란?
collection/배열 등 저장요소를 참조하여 람다식을 적용하여 반복적으로 처리할 수 있도록 하는 기능.  
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


## Thread란?
하나의 프로세스 내부에서 독립적으로 실행되는 작업단위.  
**main안에 실행문들 하나의 스레드**(그동안 만들어온 class들은 main하나의 스레드에 의해 실행되옴.)

## <Thread 생성 방법>
1. Thread 클래스 상속
Example.
```java
public class SingleThreadEx extends Thread{
    private int[] temp;
    public SingleThreadEx(String threadname){
	super(threadname);
	temp = new int[10];
		
	for(int start=0;start<temp.length;start++){
		temp[start]=start;
	}
    }
	
    public void run(){
	    for(int start:temp){
		try {
			Thread.sleep(1000);
				
		} catch (InterruptedException ie) {
			ie.printStackTrace();
			// TODO: handle exception
		}
		System.out.println("스레드이름:"+currentThread().getName());
		System.out.println("temp value :"+start);
	}
    }
	
    public static void main(String[] args) {
	SingleThreadEx st = new SingleThreadEx("첫번째");
	st.start();
    }
}
```

2. Runnable 인터페이스 상속(많이 사용되는 방법)
```java
public class SingleThreadEx2 implements Runnable{

    private int[] temp;
	
    public SingleThreadEx2(){
	temp = new int[10];
		
	for(int start=0;start<temp.length;start++){
		temp[start]=start;
	}
    }
	
    @Override
    public void run() {
	// TODO Auto-generated method stub
	for(int start:temp){
		try {
			Thread.sleep(1000);
				
		} catch (InterruptedException ie) {
			ie.printStackTrace();
			// TODO: handle exception
		}
			
		System.out.println("스레드이름:"+Thread.currentThread().getName());
		System.out.println("temp value :"+start);
	}
    }
	
    public static void main(String[] args) {

	SingleThreadEx2 ct = new SingleThreadEx2();
	Thread t = new Thread(ct,"첫번째");

	t.start();
    }
}
```

main에서 생성한 스레스들을 사용[*멀티 스레딩]
```java
public class Main {
    public static void main(String[] args) {
	ThreadEX threadex = new ThreadEX();
	ThreadEX threadex2 = new ThreadEX();
	Thread thread1 = new Thread(threadex,"A");
	Thread thread2 = new Thread(threadex2,"B");
		
	thread1.start();
	thread2.start();
		
	Thread.currentThread().getName();
    }
}

public class ThreadEX implements Runnable{

    int TestNum=0;
    @Override
    public /*synchronized 하나가 끝나야 실행됨*/ void run() {
	// TODO Auto-generated method stub
	for(int i=0;i<10;i++){
		if(Thread.currentThread().getName().equals("A")){
			System.out.println("=======================");
			TestNum++;
		}
		System.out.println("ThreadName ="+Thread.currentThread().getName()+"TestNum ="+TestNum);
			
		try {
			Thread.sleep(500);
		} catch (InterruptedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	 }
      }
}
```

*멀티스레딩 : **여러 스레드를 동시에 실행시키는** 응용프로그램을 작성하는 기법.
<장점>
1. 메모리공유로 인한 시스템 자원 소모를 줄임.
2. 동시에 두가지 이상의 활동 가능.
<단점>
1. 서로 자원을 소모하다 충동의 가능성 존재 =>**synchronized(동기화)된 공유객체 생성시, slove!!**
2. 코딩이 난해해져 버그 생성활률 높아짐.
