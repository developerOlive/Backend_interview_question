# Backend_interview_question  

## [ CS 관련 내용 ]  

<details>
<summary>TCP와 UDP의 차이점에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

![image](https://user-images.githubusercontent.com/67456294/185793406-cb3f0b74-5235-4e61-ae1a-9f1e084c8df2.png)

![image](https://user-images.githubusercontent.com/67456294/185793419-df382525-a5d8-4008-a9cb-2b6cf73e36b8.png)

  
- TCP와 UDP는 둘 다 전송 계층에서 데이터를 보내기 위해 사용하는 프로토콜 입니다.  

[ TCP ] <br>
- TCP는 연결형 서비스로 가상 회선 방식을 제공합니다. <br>
  - 3-way handshaking과정을 통해 연결을 설정하고, 4-way handshaking을 통해 연결을 해제 <br>
- 높은 신뢰성을 보장하며, 연속성보다 신뢰성있는 전송이 중요할 때에 사용됩니다. <br>
- 인터넷 상에서 데이터를 메세지의 형태(세그먼트 라는 블록 단위)로 보내기 위해 IP와 함께 사용하는 프로토콜이며 <br>
  - TCP와 IP를 함께 사용하는데, IP가 데이터의 배달을 처리한다면 TCP는 패킷을 추적 및 관리합니다. <br><br>
  
[ UDP ] <br>
- UDP는 비연결형 서비스로 데이터그램 방식을 제공합니다. <br>
  - 연결을 위해 할당되는 논리적인 경로가 없습니다. <br>
  - 그렇기 때문에 각각의 패킷은 다른 경로로 전송되고, 각각의 패킷은 독립적인 관계를 지니게 됩니다. <br>
- 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않습니다. <br>
- 신뢰성보다는 연속성이 중요한 서비스, 예를 들면 실시간 서비스(streaming)에 사용됩니다. <br><br>

[ 참고 ] <br>
- UDP와 TCP는 각각 별도의 포트 주소 공간을 관리하므로 같은 포트 번호를 사용해도 무방합니다. <br>
즉, 두 프로토콜에서 동일한 포트 번호를 할당해도 서로 다른 포트로 간주합니다. <br>

- 또한 같은 모듈(UDP or TCP) 내에서도 클라이언트 프로그램에서 동시에 여러 커넥션을 확립한 경우에는 서로 다른 포트 번호를 동적으로 할당합니다. <br><br>

</div>
</details>
  
  
  
<details>
<summary>TCP의 3-way Handshaking 역할 및 과정을 설명해주세요. </summary>
<div markdown="1">  
<br>

TCP의 3-way Handshaking 역할은 <br>
TCP/IP프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전,<br>
데이터를 보내는 쪽과 받는 쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고 <br>
실제로 데이터 전달을 시작하기전에 한 쪽이 다른 쪽에 준비되었다는 것을 알리는 것입니다. <br><br>

![image](https://user-images.githubusercontent.com/67456294/185748722-8db7622a-6c1f-44fe-a197-708decb46473.png)

TCP의 3-way Handshaking 과정은 다음과 같습니다. <br><br>
[STEP 1]<br>
A클라이언트는 B서버에 접속을 요청하는 SYN 패킷을 보냅니다. <br>
이때 A클라이언트는 SYN 을 보내고 SYN/ACK 응답을 기다리는SYN_SENT 상태가 되는 것입니다.

[STEP 2]<br>
B서버는 SYN요청을 받고 A클라이언트에게 요청을 수락한다는 ACK 와 SYN flag 가 설정된 패킷을 발송하고 <br>
A가 다시 ACK으로 응답하기를 기다립니다.<br>
이때 B서버는 SYN_RECEIVED 상태가 됩니다.

[STEP 3]<br>
A클라이언트는 B서버에게 ACK을 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 되는것입니다. <br> 
이때의 B서버 상태가 ESTABLISHED 입니다.
</div>
</details>
  
  
  
<details>
<summary> TCP의 4-way Handshaking의 역할 및 과정에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
4-way Handshaking은 세션을 종료하기 위해 수행되는 절차입니다.<br>

![image](https://user-images.githubusercontent.com/67456294/185749379-f26f220e-809a-4e46-815f-438438d142d0.png)

TCP의 4-way Handshaking 과정은 다음과 같습니다. <br><br>
[STEP 1]<br>
클라이언트가 연결을 종료하겠다는 FIN플래그를 전송합니다.<br>

[STEP 2]<br>
서버는 일단 확인메시지를 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 CLOSE_WAIT상태입니다.<br>

[STEP 3]<br>
서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송합니다.<br>

[STEP 4]<br>
클라이언트는 확인했다는 메시지를 보냅니다.<br>
TIME_WAIT Client는 Server로부터 FIN을 수신하더라도 일정시간(디폴트 240초) 동안 세션을 남겨놓고<br>
잉여 패킷을 기다리는 과정을 거치게 되는데 이 과정을 “TIME_WAIT” 라고 합니다. <br>
Server에서 FIN을 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 <br>
FIN패킷보다 늦게 도착하는 상황이 발생한다면 Client가 이미 세션을 종료한 후라서 이 패킷들이 Drop되거나 데이터는 유실되지 않도록 합니다.

</div>
</details>



<details>
<summary> HTTP와 HTTPS의 차이점에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
HTTP는 따로 암호화 과정을 거치지 않기 때문에 중간에 외부에서 패킷을 가로채거나 수정할 수 있어 보안에 취약합니다. <br>
이를 보완하기 위해 나온 것이 HTTPS입니다. 중간에 암호화 계층을 거쳐서 패킷을 암호화합니다.
</div>
</details>



<details>
<summary> HTTP의 동작 과정에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 서버 접속 -> 클라이언트 -> 요청 -> 서버 -> 응답 -> 클라이언트 -> 연결 종료

1. AOP 주요 용어 <br>
2. DNS 서버에 웹 서버의 호스트 이름을 IP 주소로 변경 요청 <br>
3. 웹 서버와 TCP 연결 시도 <br> - 3way-handshaking <br>
4. 클라이언트가 서버에게 요청 <br> 
- HTTP Request Message = Request Header + 빈 줄 + Request Body <br> 
- Request Header  <br> 
  - 요청 메소드 + 요청 URI + HTTP 프로토콜 버전 <br> 
    - GET /background.png HTTP/1.0 POST / HTTP 1.1 <br> 
    - Header 정보(key-value 구조) <br>
5. 서버가 클라이언트에게 데이터 응답 <br>
- HTTP Response Message = Response Header + 빈 줄 + Response Body <br> 
- Response Header <br> 
    - HTTP 프로토콜 버전 + 응답 코드 + 응답 메시지 <br> 
      - ex. HTTP/1.1 404 Not Found. <br> 
    - Header 정보(key-value 구조) <br> 
- 빈 줄 <br> 
  -  요청에 대한 모든 메타 정보가 전송되었음을 알리는 용도 <br> 
- Response Body <br> 
  - 응답 리소스 데이터 <br> 
    - 201, 204 상태 코드는 바디 미포함 <br> 
6. 서버 클라이언트 간 연결 종료 <br> 
  - 4way-handshaking <br> 
7. 웹 브라우저가 웹 문서 출력 <br> 
</div>
</details>



<details>
<summary> TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
Client가 데이터 전송을 마쳤다고 하더라도 Server는 아직 보낼 데이터가 남아있을 수 있기 때문에 <br> 
일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문입니다. 
</div>
</details>

--------------------------------------------------------------------------------------------------------


## [ 데이터 베이스 관련 내용 ]  

<details>
<summary> RDBMS vs NOSQL에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

DBMS는 데이터베이스를 이루는 객체들의 릴레이션을 통해서 데이터를 저장하는 데이터베이스입니다. <br>
SQL을 사용해 데이터의 저장, 질의, 수정, 삭제를 할 수 있으며 데이터를 효율적으로 보관하는 것을 목적으로 하고 구조화가 굉장히 중요합니다. <br>
장점으로는 명확한 데이터 구조를 보장하고, 중복을 피할 수 있습니다. <br>

NOSQL은 RDBMS에 비해 자유로운 형태로 데이터를 저장합니다. <br>
또한 수평확장을 할 수 있고 분산처리를 지원합니다. <br>
다양한 형태의 NOSQL 데이터베이스가 있고, 대표적으로 key-value store, bigtable, dynamo, document db, graph db 등이 있습니다. <br>

둘은 대체될 수 있는 것이 아니고, 각각 필요한 시점에 적절히 선택해서 사용해야 합니다. 둘 다 같이쓰는 상호보완적인 존재가 될 수도 있습니다.

</div>
</details>


<details>
<summary> 트랜잭션에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
트랜잭션이란 데이터베이스의 상태를 변화시키는 하나의 논리적인 작업 단위를 구성하는 연산들의 집합입니다.<br>
트랜잭션은 수행중에 한 작업이라도 실패하면 전부 실패하고, 모두 성공해야 성공이라고 할 수 있습니다.

</div>
</details>


<details>
<summary> ACID에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

ACID는 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질입니다. <br><br> 
- Atomicity(원자성): 트랜잭션의 연산은 모든 연산이 완벽히 수행되어야 하며, 한 연산이라도 실패하면 트랜잭션은 실패해야 합니다.<br>
- Consistency(일관성): 트랜잭션은 유효한 상태로만 변경될 수 있습니다.<br>
- Isolation(고립성): 트랜잭션은 동시에 실행될 경우 다른 트랜잭션에 의해 영향을 받지 않고 독립적으로 실행되어야 합니다.<br>
- Durability(내구성): 트랜잭션이 커밋된 이후에는 시스템 오류가 발생하더라도 커밋된 상태로 유지되는 것을 보장해야 합니다. <br>

</div>
</details>


<details>
<summary> Redis에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- Redis는 key-value store NOSQL DB입니다. <br>
- 싱글스레드로 동작하며 자료구조를 지원합니다. 그리고 다양한 용도로 사용될 수 있도록 다양한 기능을 지원합니다. <br>
- 데이터의 스냅샷 혹은 AOF 로그를 통해 복구가 가능해서 어느정도 영속성도 보장됩니다. <br>
</div>
</details>



--------------------------------------------------------------------------------------------------------

## [ 보안, 암호학 ] 


<details>
<summary> 단방향 암호화에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

단방향 암호화는 복호화 불가능한 암호화라고 합니다. <br> 
대부분 해시 알고리즘을 이용해서 구현하며, 민감정보를 데이터베이스에 저장할 때 해당 방식을 사용합니다.<br>

보통의 단방향 암호화는  무차별 대입 공격에 취약합니다. <br> 
따라서 이런 정보를 저장하기 위해 bcrypt와 같은 방식을 사용합니다. <br>

해시란 말에서 알 수 있듯이 충돌가능성이 있습니다. <br>
이렇게 복호화 불가능한 암호화 방식이 위험하다는 것은 해시 충돌을 일으켰다는 말로 이해해도 됩니다.
</div>
</details>


--------------------------------------------------------------------------------------------------------


## [ Java 관련 내용 ]  

<details>
<summary> JVM의 구조와 Java의 실행방식을 설명해주세요. </summary>
<div markdown="1">  
<br>

자바 가상 머신의 약자를 따서 줄여 부르는 용어로 JVM의 역할은 자바 애플리케이션을 클래스 로더를 통해 읽어 자바 API와 함께 실행하는 것입니다. 메모리 관리(GC)을 수행하며 스택기반의 가상머신입니다.

JVM의 구조는 Class Loader, Execution engine, Runtime Data Area, JNI, Native Method Library로 이루어져 있습니다.

- 클래스 로더: JVM내로 클래스를 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈
- 실행 엔진: 바이트 코드를 실행시키는 역할
  - 인터프리터: 바이트 코드를 한줄 씩 실행합니다.
  - JIT 컴파일러: 인터피르터 효율을 높이기 위한 컴파일러로 인터프리터가 반복되는 코드를 발견하면 JIT 컴파일러가 반복되는 코드를 네이티브 코드로 바꿔줍니다. 그 다음부터 인터프리터는 네이티브 코드로 컴파일된 코드를 바로 사용합니다.
  - GC(Garbage Collector): 가비지 컬렉터로 힙 영역에서 사용되지 않는 객체들을 제거하는 작업을 의미합니다.
- Runtime Data Areas: 프로그램 실행 중에 사용되는 다양한 영역입니다.
  - PC Register: Thread가 시작될 때 생성되며 현재 수행 중인 JVM 명령의 주소를 갖고 있습니다.
  - Stack Area: 지역 변수, 파라미터 등이 생성되는 영역. 실제 객체는 Heap에 할당되고 해당 레퍼런스만 Stack에 저장됩니다.
  - Heap Area: 동적으로 생성된 오브젝트와 배열이 저장되는 곳으로 GC의 대상 영역입니다.
  - Method Area: 클래스 멤버 변수, 메소드 정보, Type 정보, Constant Pool, static, final 변수 등이 생성됩니다. 상수 풀(Constant Pool)은 모든 Symbolic Reference를 포함하고 있습니다.

- JNI(Java Native Interface): 자바 애플리케이션에서 C, C++, 어셈블리어로 작성된 함수를 사용할 수 있는 방법을 제공해줍니다. Native 키워드를 사용하여 메서드를 호출합니다. 대표적인 메서드는 Thread의 currentThread()입니다.
Native Method Library: C, C++로 작성된 라이브러리 입니다. <br> <br>

Java의 실행방식

- 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어 자바 바이트코드(.class)로 변환시킵니다.
- Class Loader를 통해 class 파일들을 JVM으로 로딩합니다.
- 로딩된 class파일들은 Execution engine을 통해 해석됩니다.
- 해석된 바이트코드는 Runtime Data Areas 에 배치되어 실질적인 수행이 이루어집니다.

</div>
</details>


<details>
<summary> 컬렉션 프레임워크에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

![image](https://user-images.githubusercontent.com/67456294/200197961-c54dc32f-7108-41e8-80c1-470c3cc36623.png)


<br>

객체, 데이터들을 효율적으로 관리 할 수 있는 자료구조들이 있는 라이브러리를 컬렉션 프레임워크라고 합니다. <br> <br>

- Map <br>
  - 검색할 수 있는 인터페이스 <br>
  - 데이터를 삽입할 때 Key와 Value의 형태로 삽입되며, Key를 이용해서 Value를 얻을 수 있다. <br>
- Collection <br>
  - List <br>
    - 순서가 있는 Collection <br>
    - 데이터를 중복해서 포함할 수 있다. <br>
  - Set <br>
    - 집합적인 개념의 Collection <br>
    - 순서의 의미가 없다. <br>
    - 데이터를 중복해서 포함할 수 없다. <br>
    
</div>
</details>




<details>
<summary> java Map 인터페이스 구현체의 종류에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- HashMap <br>
  - Entry<K,V>의 배열로 저장되며, 배열의 index는 내부 해쉬 함수를 통해 계산된다. <br>
  - 내부 hash값에 따라서 키순서가 정해지므로 특정 규칙없이 출력된다. <br>
  - key와 value에 null값을 허용한다. <br>
  - 비동기 처리 <br>
  -  시간복잡도: O(1) <br>

- LinkedHashMap <br>
  - HashMap을 상속받으며, Linked List로 저장된다. <br>
  - 입력 순서대로 출력된다. <br>
  - 비동기 처리 <br>
  - 시간복잡도: O(n) <br>
- TreeMap <br>
  - 내부적으로 레드-블랙 트리(Red-Black tree)로 저장된다. <br>
  - 키값이 기본적으로 오름차순 정렬되어 출력된다. <br>
  - 키값에 대한 Compartor 구현으로 정렬 방법을 지정할 수 있다. <br>
  - 시간복잡도: O(logn) <br>
- ConCurrentHashMap <br>
  - multiple lock <br>
  - update할 때만 동기 처리 <br>
  - key와 value에 null값을 허용하지 않는다. <br>
- HashTable <br>
  - single lock <br>
  - 모든 메서드에 대해 동기 처리 <br>
  - key와 value에 null값을 허용하지 않는다. <br>
</div>
</details>



<details>
<summary> 제네릭에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
제네릭은 자바의 타입 안정성을 맡고 있습니다. <br>
컴파일 과정에서 타입체크를 해주는 기능으로 객체의 타입을 컴파일 시에 체크하기 때문에 <br> 
객체의 타입 안정성을 높이고 형변환의 번거로움을 줄여줍니다. 
</div>
</details>



<details>
<summary> java의 데이터 타입에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
1. 기본 데이터 타입(Primitive Data Type) <br>
- 기본 타입의 종류는 byte, short, char, int, float, double, boolean이 있다. <br>
  -- 정수형 : byte, short, int, long <br>
  -- 실수형 : float, double <br>
  -- 논리형 : boolean(ture/false) <br>
  -- 문자형 : char <br>
- 기본 타입의 크기가 작고 고정적이기 때문에 메모리의 Stack 영역에 저장된다. <br><br>
2. 참조 타입(Reference Data Type) <br>
- 참조 타입의 종류는 class, array, interface, Enumeration이 있다. <br>
    -- 기본형을 제외하고는 모두 참조형이다. <br>
    -- new 키워드를 이용하여 객체를 생성하여 데이터가 생성된 주소를 참조하는 타입이다. <br>
    -- String, StringBuffer, List, 개인이 만든 클래스 등 <br>
    -- String과 배열은 참조 타입과 달리 new 없이 생성이 가능하지만 기본 타입이 아닌 참조 타입이다. <br>
- 참조 타입의 데이터의 크기가 가변적, 동적이기 때문에 동적으로 관리되는 Heap 영역에 저장된다. <br>
- 더 이상 참조하는 변수가 없을 때 가비지 컬렉션에 의해 파괴된다. <br>
- 참조 타입은 값이 저장된 곳의 주소를 저장하는 공간으로 객체의 주소를 저장한다. (Call-By-Value) <br>
</div>
</details>



<details>
<summary> 동기화와 비동기화의 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
동기화(Syncronous) <br>
    - 한 자원에 동시에 접근하는 것 제한 <br>
  - 순차적으로 진행 <br> 
  - 다음에 실행될 명령은 현재 실행 중인 명령 종료 시까지 대기 (대기시간 버퍼링 발생) <br>
  - 서버와 클라이언트가 주고 받는 것이 동시에 이루어지는 형태 <br>
  - 시간적인 동기화가 필요한 곳에 많이 사용 <br>
  - ex. 현금인출기 <br>
  - Java에서 synchronized 키워드 사용 <br> 
    --- 자바에서 멀티 스레드 접근 제한 키워드 <br>
    --- 메소드 단위, 블록 단위 적용 가능 <br>
    --- 단, 메소드 단위로 지정할 경우 메소드 전체에 lock이 걸리기 때문에 가능하면 블록 활용 (임계 영역은 작을 수록 좋음) <br>
<br>
비동기화(Asyncronous) <br>
  - 현재 실행 중인 명령이 종료되지 않아도 다음 명령 실행 가능 <br>
  - Callback 함수를 통해 결과 확인 <br>
  - ex. Ajax, Thread <br>
</div>
</details>



<details>
<summary> 객체지향에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 객체(Object) <br>
  - 현실세계의 실체 및 개념을 반영하는 상태(Status)와 행위(Behavior)를 정의한 데이터의 집합 <br> <br> 
- 객체지향(Object-Oriented) 프로그래밍 <br>
  - 각자의 역할을 지닌 객체들끼리 서로 메시지를 주고받으며 동작할 수 있도록 프로그래밍 하는 것 <br><br>
- 객체 지향 모델링은 기능이 아닌 객체가 중심이 되며 "누가 어떤 일을 할 것인가?"가 핵심이 된다. <br>
즉, 객체를 도출하고 각각의 역할을 정의해 나가는 것에 초점을 맞춘다.
</div>
</details>



<details>
<summary> 객체지향의 장점에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

객체를 중심으로 프로그래밍하기 때문에, <br>
- 사람의 관점에서 프로그램을 이해하고 파악하기 쉽다.<br>
- 클래스 단위로 모듈화시켜서 개발할 수 있으므로 대형 프로젝트처럼 여러 명, 여러 회사에서 개발이 필요할 시 업무 분담이 쉽다. <br>
- 재사용성, 확장성, 융통성이 높다.<br>

이러한 장점 때문에 디버깅과 유지보수가 용이하고 설계과 분석이 비교적 쉽다.<br>
</div>
</details>



<details>
<summary> 객체지향의 단점에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 설계 시 많은 시간과 노력이 필요하다. <br>
- 사람이 이해하고 작성하기 편한 방식으로 코드를 나누기 때문에, 컴퓨터가 이해하는데 시간이 걸려 실행하는 속도가 느려지거나 저장 공간을 많이 차지한다. <br>


</div>
</details>



<details>
<summary> OOP의 4가지 특징에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
1. 추상화(Abstraction) <br>
  - 구체적인 사물들의 공통적인 특징을 파악해서 이를 하나의 개념(집합)으로 다루는 것 <br> <br>
2.캡슐화(Encapsulation) <br>
- 정보 은닉(information hiding): 필요가 없는 정보는 외부에서 접근하지 못하도록 제한하는 것 <br> 
- 높은 응집도, 낮은 결합도를 유지하여 유연함과 유지보수성 증가 <br> <br>
3. 일반화 관계(Inheritance, 상속) <br>
- 여러 개체들이 가진 공통된 특성을 부각시켜 하나의 개념이나 법칙으로 성립시키는 과정 <br> <br>
4. 다형성(Polymorphism) <br>
- 서로 다른 클래스의 객체가 같은 메시지를 받았을 때 각자의 방식으로 동작하는 능력 <br>
- 오버라이딩(Overriding), 오버로딩(Overloading) <br>
</div>
</details>



<details>
<summary> 인터페이스와 추상클래스의 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
추상 클래스(Abstract Class) <br>
&nbsp; * 개념: abstract 키워드로 선언된 클래스 <br>
&nbsp; &nbsp; a. 추상 메서드를 최소 한 개 이상 가지고 abstract로 선언된 클래스 <br>
&nbsp; &nbsp; &nbsp; -- 최소 한 개의 추상 메서드를 포함하는 경우 반드시 추상 클래스로 선언하여야 한다. <br>
&nbsp; &nbsp; b. 추상 메서드가 없어도 abstract로 선언한 클래스 <br>
&nbsp; &nbsp; &nbsp; -- 그러나 추상 메서드가 하나도 없는 경우라도 추상 클래스로 선언할 수 있다. <br> <br>
&nbsp; * 추상 클래스의 구현 <br>
&nbsp; &nbsp; -- 서브 클래스에서 슈퍼 클래스의 모든 추상 메서드를 오버라이딩하여 실행가능한 코드로 구현한다. <br> <br>
&nbsp; * 추상 클래스의 목적 <br>
&nbsp; &nbsp; -- 객체(인스턴스)를 생성하기 위함이 아니며, 상속을 위한 부모 클래스로 활용하기 위한 것이다. <br>
&nbsp; &nbsp; -- 여러 클래스들의 공통된 부분을 추상화(추상 메서드) 하여 상속받는 클래스에게 구현을 강제화하기 위한 것이다. <br>
&nbsp; &nbsp; -- 즉, 추상 클래스의 추상 메서드를 자식 클래스가 구체화하여 그 기능을 확장하는 데 목적이 있다. <br> <br>

```java
abstract class Shape { // 추상 클래스
  Shape() {...}
  void edit() {...}
  abstract public void draw(); // 추상 메서드
}
```
<br> 

```java
/* 추상 클래스의 구현 */
class Circle extends Shape {
  public void draw() { System.out.println("Circle"); } // 추상 메서드 (오버라이딩)
  void show() { System.out.println("동그라미 모양"); }
}
```

<br>
인터페이스(Interface) <br>
&nbsp; * 개념: 추상 메서드와 상수만을 포함하며, interface 키워드를 사용하여 선언한다. <br>
&nbsp; &nbsp; - 인터페이스의 구현 <br>
&nbsp; &nbsp; &nbsp; -- 인터페이스를 상속받고, 추상 메서드를 모두 구현한 클래스를 작성한다. <br>
&nbsp; &nbsp; &nbsp; -- implements 키워드를 사용하여 구현한다. <br> <br>
&nbsp; &nbsp; - 인터페이스의 목적 <br>
&nbsp; &nbsp; &nbsp; -- 상속받을 서브 클래스에게 구현할 메서드들의 원형을 모두 알려주어, 클래스가 자신의 목적에 맞게 메서드를 구현하도록 하는 것이다. <br>
&nbsp; &nbsp; &nbsp; -- 구현 객체의 같은 동작을 보장하기 위한 목적이 있다. <br>
&nbsp; &nbsp; &nbsp; -- 즉, 서로 관련이 없는 클래스에서 공통적으로 사용하는 방식이 필요하지만 기능을 각각 구현할 필요가 있는 경우에 사용한다. <br> <br>
&nbsp; &nbsp; - 인터페이스의 특징 <br>
&nbsp; &nbsp; &nbsp; a. 인터페이스는 상수 필드와 추상 메서드만으로 구성된다. <br>
&nbsp; &nbsp; &nbsp; b. 모든 메서드는 추상 메서드로서, abstract public 속성이며 생략 가능하다. <br>
&nbsp; &nbsp; &nbsp; c. 상수는 public static final 속성이며, 생략하여 선언할 수 있다. <br>
&nbsp; &nbsp; &nbsp; d. 인터페이스를 상속받아 새로운 인터페이스를 만들 수 있다. <br>


```java
/* 인터페이스의 개념 */
interface Phone { // 인터페이스
  int BUTTONS = 20; // 상수 필드 (public static final int BUTTONS = 20;과 동일)
  void sendCall(); // 추상 메서드 (abstract public void sendCall();과 동일)
  abstract public void receiveCall(); // 추상 메서드
}
```


```java
/* 인터페이스의 구현 */
class FeaturePhone implements Phone {
  // Phone의 모든 추상 메서드를 구현한다.
  public void sendCall() {...}
  public void receiveCall() {...}

  // 추가적으로 다른 메서드를 작성할 수 있다.
  public int getButtons() {...}
}
```

</div>
</details>


<details>
<summary> 클래스, 객체, 인스턴스에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 클래스
  - 객체를 만들어 내기 위한 설계도 혹은 
  - 연관되어 있는 변수와 메서드의 집합
  
- 객체(Object)
  - 소프트웨어 세계에 구현할 대상
  - 클래스에 선언된 모양 그대로 생성된 실체
  - '클래스의 인스턴스(instance)' 라고도 부른다.
  - 객체는 모든 인스턴스를 대표하는 포괄적인 의미를 갖는다.
  - oop의 관점에서 클래스의 타입으로 선언되었을 때 '객체'라고 부른다.

- 인스턴스(Instance)
  - 설계도를 바탕으로 소프트웨어 세계에 구현된 구체적인 실체
    - 즉, 객체를 소프트웨어에 실체화 하면 그것을 '인스턴스'라고 부른다.
    - 실체화된 인스턴스는 메모리에 할당된다.
  - 인스턴스는 객체에 포함된다고 볼 수 있다.
  - oop의 관점에서 객체가 메모리에 할당되어 실제 사용될 때 '인스턴스'라고 부른다.
  - 추상적인 개념(또는 명세)과 구체적인 객체 사이의 관계 에 초점을 맞출 경우에 사용한다.
    - '~의 인스턴스' 의 형태로 사용된다.
    - 객체는 클래스의 인스턴스다.
    - 객체 간의 링크는 클래스 간의 연관 관계의 인스턴스다.
    - 실행 프로세스는 프로그램의 인스턴스다.
  - 즉, 인스턴스라는 용어는 반드시 클래스와 객체 사이의 관계로 한정지어서 사용할 필요는 없다.
  - 인스턴스는 어떤 원본(추상적인 개념)으로부터 '생성된 복제본'을 의미한다.


```java
/* 클래스 */
public class Animal {
  ...
}
/* 객체와 인스턴스 */
public class Main {
  public static void main(String[] args) {
    Animal cat, dog; // '객체'

    // 인스턴스화
    cat = new Animal(); // cat은 Animal 클래스의 '인스턴스'(객체를 메모리에 할당)
    dog = new Animal(); // dog은 Animal 클래스의 '인스턴스'(객체를 메모리에 할당)
  }
}
```
<br><br>
- Q. 클래스 VS 객체 <br>
  - 클래스는 '설계도', 객체는 '설계도로 구현한 모든 대상'을 의미한다. <br><br>
- Q. 객체 VS 인스턴스 <br>
  - 클래스의 타입으로 선언되었을 때 객체라고 부르고, 그 객체가 메모리에 할당되어 실제 사용될 때 인스턴스라고 부른다. <br>
  - 객체는 현실 세계에 가깝고, 인스턴스는 소프트웨어 세계에 가깝다. <br>
  - 객체는 '실체', 인스턴스는 '관계'에 초점을 맞춘다. <br>
  - 객체를 '클래스의 인스턴스'라고도 부른다. <br>
  - '방금 인스턴스화하여 레퍼런스를 할당한' 객체를 인스턴스라고 말하지만, 이는 원본(추상적인 개념)으로부터 생성되었다는 것에 의미를 부여하는 것일 뿐 엄격하게 객체와 인스턴스를 나누긴 어렵다. <br><br>
- 추상화 기법 <br>
1. 분류(Classification) <br>
   - 객체 -> 클래스 <br>
   - 실재하는 객체들을 공통적인 속성을 공유하는 범부 또는 추상적인 개념으로 묶는 것 <br>
2. 인스턴스화(Instantiation) <br>
   - 클래스 -> 인스턴스 <br>
    - 분류의 반대 개념. 범주나 개념으로부터 실재하는 객체를 만드는 과정 <br>
    - 구체적으로 클래스 내의 객체에 대해 특정한 변형을 정의하고, 이름을 붙인 다음, 그것을 물리적인 어떤 장소에 위치시키는 등의 작업을 통해 인스턴스를 만드는 것을 말한다. 
<br>
</div>
</details>


<details>
<summary> java의 main 메서드가 static인 이유에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- static 키워드 <br>
  - static 멤버는 클래스 로딩(프로그램 시작) 시 메모리에 로드되어 인스턴스를 생성하지 않아도 호출이 가능하다. <br>
- main 메서드가 static인 이유 <br>
  - public static void main(String[] args){...} <br>
  - 위와 같은 형식은 java에서의 main() 관례이다. 위와 같은 시그니처를 가진 메소드가 없으면 실행되지 않는다. <br>
  - JVM은 인스턴스가 없는 클래스의 main()을 호출해야하기 때문에 static이어야 한다. <br>
- JVM과 static <br>
  - 코드를 실행하면 컴파일러가 .java 코드를 .class(byte code)로 변환한다. <br>
  - 클래스 로더가 .class파일을 메모리 영역(Runtime Data Area)에 로드한다. <br>
  - Runtime Data Area 중 Meathod Area(= Class area = Static area)라고 불리는 영역에 Class Variable이 저장되는데, static 변수 또한 여기에 포함된다. <br>
  - JVM은 Meathod Area에 로드된 main()을 실행한다. <br> <br>
  ![image](https://user-images.githubusercontent.com/67456294/200429668-8e46e3b1-b53b-4780-8e50-2dc84f4fd698.png)

</div>
</details>


--------------------------------------------------------------------------------------------------------

## [ Spring ] 


<details>
<summary> Bean에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
- 컨테이너 안에 들어있는 객체 <br>
- 컨테이너에 담겨있으며, 필요할 때 컨테이너에서 가져와서 사용 <br>
- @Bean 을 사용하거나 xml 설정을 통해 일반 객체를 Bean으로 등록할 수 있고, Bean으로 등록된 객체는 쉽게 주입하여 사용 가능 <br>
</div>
</details>


<details>
<summary> Bean 생명주기에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
- 객체 생성 -> 의존 설정 -> 초기화 -> 사용 -> 소멸 <br>
- 스프링 컨테이너에 의해 생명주기 관리 <br>
- 스프링 컨테이너 초기화 시 빈 객체 생성, 의존 객체 주입 및 초기화 <br>
- 스프링 컨테이너 종료 시 빈 객체 소멸 <br>
</div>
</details>


<details>
<summary> Bean 컨테이너에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
- 컨테이너(Container)는 보통 인스턴스의 생명주기를 관리하며, 개발자가 작성한 코드의 처리과정을 위임받은 독립적인 존재입니다. <br>
- 컨테이너는 적절한 설정만 되어있다면 개발자가 작성한 코드를 스스로 참조한 뒤 알아서 객체의 생성과 소멸을 컨트롤합니다. <br>
- Spring 프레임워크는 다른 프레임워크들과 달리 컨테이너 기능을 제공하고 있습니다. <br> 
- 이와 같은 컨테이너 기능을 제공하는 것이 가능하도록 하는 것이 IoC 패턴입니다.
</div>
</details>


<details>
<summary> IoC에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
IoC(Inversion of Control, 제어의 역전)란 <br>
- 객체의 생성에서부터 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐 것을 의미하며, <br>
제어 권한을 자신이 아닌 다른 대상에게 위임하는 것입니다. <br>
- 이 방식은 대부분의 프레임워크에서 사용하는 방법으로, 개발자는 필요한 부분을 개발해서 끼워 넣기의 형태로 개발하고 실행합니다. <br> <br>
- 프레임워크가 이러한 구조를 가지기 때문에 개발자는 프레임워크에 필요한 부품을 개발하고 조립하는 방식의 개발을 하게 됩니다. <br>
- 이렇게 조립된 코드의 최종 호출은 개발자에 의해서 제어되는 것이 아니라 <br>
프레임워크의 내부에서 결정된 대로 이뤄지게 되는데, 이러한 현상을 "제어의 역전"이라고 표현합니다. <br><br><br>

Spring에서의 IoC <br>
Spring 프레임워크에서 지원하는 Ioc Container는 우리들이 흔히 개발하고 사용해왔던 <br>
일반 POJO(Plain Old Java Object)의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능들을 제공합니다. <br><br>

라이브러리와 프레임워크의 차이 <br>
IoC의 개념이 적용되었나의 차이르 의미합니다. <br>
라이브러리를 사용하는 애플리케이션 코드는 애플리케이션 흐름을 직접 제어합니다. <br>
단지 동작하는 중에 필요한 기능이 있을 때 능동적으로 라이브러리를 시용할 뿐입니다. <br>
반면에 프레임워크는 거꾸로 애플리케이션 코드가 프레임워크에 의해 사용됩니다. <br>
보통 프레임워크 위에 개발한 클래스를 등록해두고, <br> 
프레임워크가 흐름을 주도히는 중에 개발자가 만든 애플리케이션 코드를 시용하도록 만드는 방식입니다.
</div>
</details>



<details>
<summary> DI에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- DI란 <br>
  - Dependency Injection, 의존성 주입 <br>
  - Dependency Injection은 Spring 프레임워크에서 지원하는 IoC의 형태이다. <br>
  - DI는 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동적으로 연결해주는 것을 말한다. <br> 
  - 개발자들은 제어를 담당할 필요없이 빈 설정 파일에 의존관계가 필요하다는 정보만 추가해주면 된다. <br>
    - 컨테이너가 실행 흐름의 주체가 되어 애플리케이션 코드에 의존관계를 주입해주는 것. <br><br>
    
- 의존성(Dependency) <br>
  - Dependency Injection, 의존성 주입  <br>
  - 현재 객체가 다른 객체와 상호작용(참조)하고 있다면 다른 객체들을 현재 객체의 의존이라 한다. <br><br>
      
- 의존성이 위험한 이유 <br>
  - 하나의 모듈이 바뀌면 의존한 다른 모듈까지 변경되야 한다. <br>
  - 테스트 가능한 어플을 만들 때 의존성이 있으면 유닛테스트 작성이 어렵다. <br>
  - 유닛테스트의 목적 자체가 다른 모듈로부터 독립적으로 테스트하는 것을 요구한다. <br><br>

- DI의 특징 <br>
  - ‘new’를 사용해 모듈 내에서 다른 모듈을 초기화하지 않으려면 객체 생성은 다른 곳에서 하고, 생성된 객체를 참조하면 된다.<br>
  - 의존성 주입은 Inversion of Control 개념을 바탕으로 한다. 클래스가 외부로부터 의존성을 가져야한다. <br><br>
 
- DIDI가 필요한 이유(DI의 장점) <br>
  - 클래스를 재사용 할 가능성을 높이고, 다른 클래스와 독립적으로 클래스를 테스트 할 수 있다. <br>
  - 비즈니스 로직의 특정 구현이 아닌 클래스를 생성하는데 매우 효과적이다. <br><br>

- DI의 세가지 방법 <br>
  - Contructor Injection : 생성자 삽입
  - Method(Setter) Injection : 메소드 매개 변수 삽입
  - Field Injection : 멤버 변수 삽입
</div>
</details>


<details>
<summary> AOP에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- AOP(Aspect Oriented Programming)란 <br>
  - Aspect Oriented Programming, 관점 지향 프로그래밍 <br>
  - 어떤 로직을 기준으로 핵심 관점과 부가 관점을 나누고, 관점을 기준으로 모듈화하는 것 <br>
  - 핵심 관점은 주로 핵심 비즈니스 로직 <br> 
  - 부가 관점은 핵심 로직을 실행하기 위한 데이터베이스 연결, 로깅, 파일 입출력 등 <br><br>

- AOP 목적 <br>
  - 소스 코드에서 여러 번 반복해서 쓰는 코드(= 흩어진 관심사, Concern)를 Aspect로 모듈화하여 핵심 로직에서 분리 및 재사용  <br>
  - 개발자가 핵심 로직에 집중할 수 있게 하기 위함 <br>
  - 주로 부가 기능을 모듈화 <br><br>
      
- AOP 주요 용어 <br>
  - Aspec <br>
    - 흩어진 관심사를 모듈화 한 것 <br>
    - Advice + PointCut <br>
  - Target <br>
    - Aspect를 적용하는 곳(클래스, 메소드 등) <br>
  - Advice <br>
    - 실질적으로 수행해야 하는 기능을 담은 구현체 <br>
    - Advice + PointCut <br>
  - JoinPoint <br>
    - Advice가 적용될 위치 <br>
    - 끼어들 수 있는 지점 <br>
    - ex. 메소드 진입 시, 생성자 호출 시, 필드에서 값 꺼낼 때 등 <br>
  - PointCut <br>
    - JoinPoint의 상세 스펙 정의 <br>
    - 더욱 구체적으로 Advice가 실행될 지점 지정 <br>
  - Weaving <br>
    - PointCut에 의해 결정된 Target의 JoinPoint에 Advice를 삽입하는 과정 <br>
    
</div>
</details>


