# Why java return void?
## 왜 자바의 메인함수는 public static void main (String[] args)일까요?
먼저 java API문서를 찾아보았습니다.
https://docs.oracle.com/javase/specs/jls/se8/html/jls-12.html

![image](https://user-images.githubusercontent.com/117427075/231462984-dd0e97ab-14f2-4e0d-b23e-f44c0e256670.png)  
보시면 must be declare로써 public static void를 쓰라고 합니다.

즉 그냥 외우라는 것인데요

하지만 1,2학년이였다면 넘어갔을지 몰라도 지금은 이에 의문을 가져보려고 합니다.  

또 인터넷에 찾아봐도 다들 두루뭉실하게 설명하고 정보가 흩어져있어서 제가 공부한 내용을 요약해보자합니다.  




## 먼저 public입니다
main 메소드의 접근 제어자는 public입니다.public 접근 제어자를 사용할 경우 어디에서나 해당 메소드에 접근이 가능하게 됩니다.  

즉, main 메소드를 어디에서나 접근 가능하게 만들고 싶다라는 의도를 가지고 있습니다.  

## 두번째로 static입니다
![image](https://user-images.githubusercontent.com/117427075/231470890-374c4842-c930-4720-a171-cc44c83f367e.png)  
만약 main메소드가 heap영역에 선언되면 어떻게 될까요?  

main메소드는 프로그램에 없어서는 안되는 기본함수인데요  

만약 이 힘수가 Garbage Collector에 의해 메모리에서 정리되면 어떻게 될까요?  

기본이 되는 함수가 정리되었으니 프로그램이 죽습니다.  

따라서 static으로 선언하여 메모리에 항상 상주하도록 합니다.  


## 세번째로 반환값은 왜 void인가?
먼저 진행하기에 앞서 c언어를 살펴보겠습니다.  

어? c언어에서는 main함수의 리턴값은 void가 아니라 int형입니다.   

main함수가 종료되면 프로그램이 종료되는 게 아닌가? 그럼 반환을 누구한테 해준다는 말인까요?  

바로 운영체제입니다. 왜냐면 운영체제에서 프로그램을 실행시켜주었으니 당연히 운영체제에 반환을 해주어 에러를 찾아줄 수 있습니다.  


![image](https://user-images.githubusercontent.com/117427075/231470998-1bd4e17b-29dc-4c76-bd60-bd9a1873daff.png)  
![image](https://user-images.githubusercontent.com/117427075/231471560-71acb861-d4bd-447b-b52d-26e52f1e1938.png)  
즉 여기서 반환값은 마음대로 정하면 되는데 이 값으로써 어디에서 무엇이 종료되었는지 알 수 있습니다.  

0 정상종료, -1 에러 그외 마음대로입니다  


어? 그럼 자바에서는 어떻게 에러가 났는지 알까요?  

바로 System클래스를 이용하면 됩니다.  

즉 System.exit(0), System.exit(1), System.out(2) …. System.out(999)같이 쓰면 되는데요.  

→ 이것을 안쓰면 항상 0을 돌려준다고 합니다.  
![image](https://user-images.githubusercontent.com/117427075/231472362-76329895-a27b-412a-9e3d-8e2f4ed074a4.png)  
![image](https://user-images.githubusercontent.com/117427075/231472535-e41fcc05-c504-4c0c-aeb4-f7ffdce75bae.png)  

  


그렇다면 System클래스는 무엇일까요?    


먼저 자바 프로그램은 운영체제상에서 바로 실행되는 것이 아니라 JVM 위에서 실행됩니다. 따라서 운영체제의 모든 기능을 자바 코드로 직접 접근하기란 어렵습니다.  

하지만 java.lang 패키지에 속하는 System클래스를 이용하면 운영체제의 일부 기능을 이용할 수 있습니다.  


즉 프로그램 종료, 키보드로부터 입력, 모니터로 출력, 메모리 정리, 현재 시간 읽기, 시스템 프로퍼티 읽기, 환경 변수 읽기 등이 가능합니다.  


이로써 알 수 있는 내용을 정리하자면  

즉 c에서는 운영체제에 main리턴값을 반환해줘서 그 역할을 하지만  

java에서는 운영체제에 반환을 안해주며 JVM에 직접 반환하게됩니다.

java에서는 JVM에 System클래스가 그 역할을 해줘서 main의 반환값이 void인 것입니다.    

## 즉 return;은 종료의 기능만을 하며 에러구문은 System(System.exit)에서 처리해줌으로써  
## 단순 void만 반환해줄 수 있는 것입니다.
