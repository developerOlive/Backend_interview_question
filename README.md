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
  ㄲ
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
<br>

HTTP는 Hyper Text Transfer Protocol의 줄임말으로써 서버와 클라이언트간에 데이터를 주고 받는 프로토콜입니다.<br>
HTTP는 텍스트, 이미지,영상, JSON 등등 거의 모든 형태의 데이터를 전송할수 있습니다.<br>

<br>

- HTTP HTTPS 차이점<br>
  - HTTPS(https://)는 SSL(Secure Socket Layer) 인증서를 사용하는 HTTP(http://)입니다.<br>
  - SSL(또는 TLS) 인증서는 일반 HTTP 요청 및 응답을 암호화합니다.<br>
  - 따라서 HTTPS는 HTTP보다 더 안전한 보안용 프로토콜이라고 할 수 있습니다.<br>
  - HTTP와 HTTPS의 유일한 차이점은 HTTPS를 사용한 웹 페이지를 통해 전송되는 모든 데이터는 추가적인 보안 계층이 있습니다.<br>
  - 이를 TLS(전송 계층 보안) 프로토콜이라고 합니다.<br>
  - 모든 유형의 데이터는 변경되거나 손상될 수 없는 HTTPS 사이트를 통해 전달되며 제3자로부터 보호됩니다.<br>

<br><br>

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



<details>
<summary> 쿠키와 세션의 차이점에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- HTTP 프로토콜의 특징<br>
  - 비연결 지향(Connectionless)<br>
    - 클라이언트가 request를 서버에 보내고, 서버가 클라이언트에 요청에 맞는 response를 보내면 바로 연결을 끊는다.<br>
  - 상태정보 유지 안 함(Stateless)<br>
    - 연결을 끊는 순간 클라이언트와 서버의 통신은 끝나며 상태 정보를 유지하지 않는다.<br>
- 쿠키와 세션의 필요성<br>
  - HTTP 프로토콜은 위와 같은 특징으로 모든 요청 간 의존관계가 없다.<br>
  - 즉, 현재 접속한 사용자가 이전에 접속했던 사용자와 같은 사용자인지 아닌지 알 수 있는 방법이 없다.<br>
  - 계속해서 연결을 유지하지 않기 때문에 리소스 낭비가 줄어드는 것이 큰 장점이지만, 통신할 때마다 새로 연결하기 때문에 클라이언트는 매 요청마다 인증을 해야 한다는 단점이 있다.<br>
  - 이전 요청과 현재 요청이 같은 사용자의 요청인지 알기 위해서는 상태를 유지해야 한다.<br>
  - HTTP 프로토콜에서 상태를 유지하기 위한 기술로 쿠키와 세션이 있다.<br>
- 쿠키(Cookie)란?<br>
  - 개념<br>
    - 클라이언트 로컬에 저장되는 키와 값이 들어있는 파일이다.<br>
    - 이름, 값, 유효 시간, 경로 등을 포함하고 있다.<br>
    - 클라이언트의 상태 정보를 브라우저에 저장하여 참조한다.<br>
  - 구성 요소<br>
    - 쿠키의 이름(name)<br>
    - 쿠키의 값(value)<br>
    - 쿠키의 만료시간(Expires)<br>
    - 쿠키를 전송할 도메인 이름(Domain)<br>
    - 쿠키를 전송할 경로(Path)<br>
    - 보안 연결 여부(Secure)<br>
    - HttpOnly 여부(HttpOnly)<br>
  - 동작방식<br>
    1. 웹브라우저가 서버에 요청<br>
    2. 상태를 유지하고 싶은 값을 쿠키(cookie)로 생성<br>
    3. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 쿠키를 포함해서 전송<br>
      - Set−Cookie: id=doy<br>
    4. 전달받은 쿠키는 웹브라우저에서 관리하고 있다가, 다음 요청 때 쿠키를 HTTP 헤더에 넣어서 전송<br>
      - cookie: id=doy<br>
    5. 서버에서는 쿠키 정보를 읽어 이전 상태 정보를 확인한 후 응답<br>
  - 쿠키 사용 예<br>
    - 아이디, 비밀번호 저장<br>
  - 쇼핑몰 장바구니<br>
  <br><br>
  
- 세션(Session)이란?<br>
  - 개념<br>
    - 일정 시간 동안 같은 브라우저로부터 들어오는 요청을 하나의 상태로 보고 그 상태를 유지하는 기술이다.<br>
    - 즉, 웹 브라우저를 통해 서버에 접속한 이후부터 브라우저를 종료할 때까지 유지되는 상태이다.<br>
  - 동작 방식<br>
    1. 웹브라우저가 서버에 요청<br>
    2. 서버가 해당 웹브라우저(클라이언트)에 유일한 ID(Session ID)를 부여함<br>
    3. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 Session ID를 포함해서 전송<br>
    쿠키에 Session ID를 JSESSIONID 라는 이름으로 저장<br>
      - Set−Cookie: JSESSIONID=xslei13f<br>
    4. 웹브라우저는 이후 웹브라우저를 닫기까지 다음 요청 때 부여된 Session ID가 담겨있는 쿠키를 HTTP 헤더에 넣어서 전송<br>
      - Cookie: JSESSIONID=xslei13f<br>
    5. 서버는 세션 ID를 확인하고, 해당 세션에 관련된 정보를 확인한 후 응답<br>
    - 세션 사용 예<br>
      - 로그인<br>
<br><br>

- 쿠키와 세션의 차이점<br>
  - 저장 위치<br>
    - 쿠키 : 클라이언트<br>
    - 세션 : 서버<br>
  - 보안<br>
    - 쿠키 : 클라이언트에 저장되므로 보안에 취약하다.<br>
    - 세션 : 쿠키를 이용해 Session ID만 저장하고 이 값으로 구분해서 서버에서 처리하므로 비교적 보안성이 좋다.<br>
  - 라이프사이클<br>
    - 쿠키 : 만료시간에 따라 브라우저를 종료해도 계속해서 남아 있을 수 있다.<br>
    - 세션 : 만료시간을 정할 수 있지만 브라우저가 종료되면 만료시간에 상관없이 삭제된다.<br>
  - 속도<br>
    - 쿠키 : 클라이언트에 저장되어서 서버에 요청 시 빠르다.<br>
    - 세션 : 실제 저장된 정보가 서버에 있으므로 서버의 처리가 필요해 쿠키보다 느리다.<br>

</div>
</details>



--------------------------------------------------------------------------------------------------------


## [ 데이터 베이스 관련 내용 ]  

<details>
<summary> RDBMS vs NOSQL에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- RDBMS <br>
  - DBMS는 데이터베이스를 이루는 객체들의 릴레이션을 통해서 데이터를 저장하는 데이터베이스입니다. <br>
  - SQL을 사용해 데이터의 저장, 질의, 수정, 삭제를 할 수 있으며 데이터를 효율적으로 보관하는 것을 목적으로 하고 구조화가 굉장히 중요합니다. <br>
  - 장점으로는 명확한 데이터 구조를 보장하고, 중복을 피할 수 있습니다. <br> 
- NOSQL <br>
  - NOSQL은 RDBMS에 비해 자유로운 형태로 데이터를 저장합니다. <br>
  - 또한 수평확장을 할 수 있고 분산처리를 지원합니다. <br>
  - 다양한 형태의 NOSQL 데이터베이스가 있고, 대표적으로 key-value store, bigtable, dynamo, document db, graph db 등이 있습니다. <br>

둘은 대체될 수 있는 것이 아니고, 각각 필요한 시점에 적절히 선택해서 사용해야 합니다. 둘 다 같이쓰는 상호보완적인 존재가 될 수도 있습니다.

</div>
</details>


<details>
<summary> 트랜잭션에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 트랜잭션(Transaction) 이란 <br>
   - 데이터베이스의 상태를 변환시키는 하나의 논리적인 작업 단위를 구성하는 연산들의 집합이다. <br>
    - 예를들어, A계좌에서 B계좌로 일정 금액을 이체한다고 가정하자. <br>
     a. A계좌의 잔액을 확인한다. <br>
     b. A계좌의 금액에서 이체할 금액을 빼고 다시 저장한다. <br>
     c. B계좌의 잔액을 확인한다. <br>
     d. B계좌의 금액에서 이체할 금액을 더하고 다시 저장한다. <br>
    - 이러한 과정들이 모두 합쳐져 계좌이체라는 하나의 작업단위를 구성한다. <br>
  - 하나의 트랜잭션은 Commit 되거나 Rollback 된다. <br>
    - Commit 연산 <br>
      - 한개의 논리적 단위(트랜잭션)에 대한 작업이 성공적으로 끝나 데이터베이스가 다시 일관된 상태에 있을 때, 이 트랜잭션이 행한 갱신 연산이 완료된 것을 트랜잭션 관리자에게 알려주는 연산이다. <br>
    - Rollback 연산 <br>
      - 하나의 트랜잭션 처리가 비정상적으로 종료되어 데이터베이스의 일관성을 깨뜨렸을 때, 이 트랜잭션의 일부가 정상적으로 처리되었더라도 트랜잭션의 원자성을 구현하기 위해 이 트랜잭션이 행한 모든 연산을 취소(Undo)하는 연산이다. <br>
      - Rollback 시에는 해당 트랜잭션을 재시작하거나 폐기한다. <br>
  - 데이터베이스 응용 프로그램은 트랜잭션들의 집합으로 정의 할 수 있다. <br>
- 트랜잭션의 필요성 <br>
  - 현금 인출기를 작동하는 도중에 기계오류나 정전 등과 같은 예기치 않은 상황이 발생하여 카드가 나오지 않거나 기계가 멈추는 경우 <br>
  - 각각 다른 지점의 은행에서 동시에 인출할 때, 하나의 지점이 다른 지점에서 저장한 잔액을 덮어 쓰는 경우 <br>
  - 위와 같은 상황이 발생되지 않도록 방지하기 위해, 즉, 트랜잭션의 성질인 ACID를 제공받기 위해 트랜잭션을 사용한다. <br><br>
  
- 트랜잭션의 상태 <br>
![image](https://user-images.githubusercontent.com/67456294/202310579-76b6d114-b199-433d-b0e9-85a01dcf3449.png)


  - 활동(Active) <br>
    - 트랜잭션이 실행 중에 있는 상태, 연산들이 정상적으로 실행 중인 상태 <br>
  - 장애(Failed) <br>
    - 트랜잭션이 실행에 오류가 발생하여 중단된 상태 <br>
  - 철회(Aborted) <br>
    - 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태 <br>
  - 부분 완료(Partially Committed) <br>
    - 트랜잭션이 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태 <br>
  - 완료(Committed) <br>
    - 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태 <br>

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
<br><br>
  
- REmote DIctionary Server<br>
- 오픈 소스 인 메모리 키 값 데이터 구조 스토어입니다.<br>
- 인메모리 방식이기 때문에 디스크에 데이터를 저장하는 다른 RDBMS보다 훨씬 빠릅니다.<br>
- Redis는 다양한 인 메모리 데이터 구조 집합(문자열, 리스트, 맵, 집합)을 제공합니다.<br>

<br><br>

- 데이터베이스가 있는데도 Redis라는 인메모리 데이터 구조 저장소를 사용하는 이유는 무엇일까? <br>
  - DB는 데이터를 물리 디스크에 직접 쓰기 때문에 서버에 문제가 발생하여 다운되더라도 데이터가 손실되지 않는다. <br>
  - 하지만 매번 디스크에 접근해야하기 때문에 만약 많은 사용자들이 접근하게 된다면 부하가 많아져서 느려질 수 있는 단점이 존재한다. <br>
  - 따라서 일반적으로 서비스 운영 초반을 벗어나 규모가 커지게 되면, 사용자가 늘어나고, 이에 따라 데이터 베이스가 과부하 될 수 있기 때문에 이때 캐시 서버를 도입하여 사용한다.
    - 그리고 이 캐시 서버로 이용할 수 있는 것이 바로 Redis <br>
  - 캐시는 한번 읽어온 데이터를 임의의 공간에 저장하여 다음에 읽을 때는 빠르게 결괏값을 받을 수 있도록 도와주는 공간이다. <br>
  - 같은 요청이 여러 번 들어오는 경우 매번 DB를 거치는 것이 아니라 <br>
    - 캐시 서버에서 첫 번째 요청 이후 저장된 결괏값을 바로 내려주기 때문에 DB의 부하를 줄이고 서버의 속도도 느려지지 않게 된다. <br>

<br><br>

- Redis 특징
  - 보통 데이터베이스는 하드 디스크나 SSD에 저장한다. 하지만 Redis는 메모리(RAM)에 저장해서 디스크 스캐닝이 필요없어 매우 빠르다는 장점이 존재한다. <br>
  - 주요 Redis 사용 사례로는 캐싱, 세션 관리, pub/sub(발행/구독) 및 순위표 등이 존재한다. <br>
  - 데이터 구조는 key/value 값으로 이루어져 있다. → 따라서 Redis는 비정형 데이터를 저장하는 비관계형 데이터베이스 관리 시스템이다. <br>
  - Single Threaded 이기 때문에 한 번에 하나의 명령만 처리할 수 있다. <br>

<br>

어라 근데 RAM은 휘발성이지 않나요…? <br>
→ 이를 막기위한 백업 과정이 존재한다 !! (Redis의 영속성) <br>

<br>

- Redis 영속성<br>
  - Redis는 지속성을 보장하기 위해 데이터를 DISK에 저장할 수 있다.<br>
  - 서버가 내려가더라도 DISK에 저장된 데이터를 읽어서 메모리에 로딩을 한다.<br>
  - RDB (snapshot) 순간적으로 메모리에 있는 내용을 DISK에 전체를 옮겨 담는 방식<br>
  - AOF (Append Only File) 명령(쿼리)들을 저장해두고, 서버가 셧다운되면 재실행해서 다시 만들어 놓는 방식 (Redis의 모든 write/update 연산 자체를 모두 log 파일에 기록하는 형태)<br>

<br><br>

</div>
</details>


<details>
<summary> JDBC에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br><br>


JDBC란?<br>
  - Java Database Connectivity<br>
  - 자바언어와 DB를 연결해주는 통로와 같은 것<br>
  - 자바를 이용한 DB접속과 SQL문장의 실행, 그리고 실행 결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 관한 규약<br>
  - 자바 프로그램내에서 SQL문을 실행하기 위한 자바 API<br>
  - SQL과 프로그래밍 언어의 통합 접근 중 한 형태<br>

  <br><br>

[ JDBC의 동작 흐름 ] <br>

![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/f69f4c79-8171-4a07-9046-217495d635d9)

<br>

- JDBC는 Java 애플리케이션 내에서 JDBC API를 사용하여 데이터베이스에 접근하는 단순한 구조이다. <br>
- JDBC API를 사용하기 위해서는 JDBC 드라이버를 먼저 로딩한 후 데이터베이스와 연결하게 된다. <br>

<br><br>

[ JDBC 드라이버 ] <br>

- 데이터베이스와의 통신을 담당하는 인터페이스 <br>
- Oracle, MS SQL, MySQL 등과 같은 데이터베이스에 알맞은 JDBC 드라이버를 구현하여 제공 <br>
- JDBC 드라이버의 구현체를 이용해서 특정 벤더의 데이터베이스에 접근할 수 있음 <br>

<br><br>

[ JDBC API 사용 흐름] <br>

![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/40b87887-3512-4c41-9367-341b1d633823)

<br>

1. JDBC 드라이버 로딩 <br>
   - 사용하고자 하는 JDBC 드라이버를 로딩한다. JDBC 드라이버는 DriverManager 클래스를 통해 로딩된다. <br>

2. Connection 객체 생성 <br>
   - JDBC 드라이버가 정상적으로 로딩되면 DriverManager를 통해 데이터베이스와 연결되는 세션(Session)인 Connection 객체를 생성한다. <br> 

3. Statement 객체 생성 <br>
   - Statement 객체는 작성된 SQL 쿼리문을 실행하기 위한 객체로 정적 SQL 쿼리 문자열을 입력으로 가진다. <br>

4. Query 실행 <br>
   - 생성된 Statement 객체를 이용하여 입력한 SQL 쿼리를 실행한다. <br>

    
<br><br>

</div>
</details>



<details>
<summary> 데이터베이스 풀에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- Connection Pool <br>
  - 클라이언트의 요청에 따라 각 어플리케이션의 스레드에서 데이터베이스에 접근하기 위해서는 Connection이 필요하다. <br>
  - Connection pool은 이런 Connection을 여러 개 생성해 두어 저장해 놓은 공간(캐시), 또는 이 공간의 Connection을 필요할 때 꺼내 쓰고 반환하는 기법을 말한다. <br>
  ![image](https://user-images.githubusercontent.com/67456294/202581000-e485f7a6-7181-42d9-89fa-d9dc2fed92cc.png)
  
<br>
  
- DB에 접근하는 단계 <br>
  1. 웹 컨테이너가 실행되면서 DB와 연결된 Connection 객체들을 미리 생성하여 pool에 저장한다. <br>
  2. DB에 요청 시, pool에서 Connection 객체를 가져와 DB에 접근한다. <br>
  3. 처리가 끝나면 다시 pool에 반환한다. <br>
  
  ![image](https://user-images.githubusercontent.com/67456294/202581112-0aaea334-acb2-49d1-9f16-6faacefb3287.png)

  <br>
  
- Connction이 부족하면? <br>
  - 모든 요청이 DB에 접근하고 있고 남은 Conncetion이 없다면, 해당 클라이언트는 대기 상태로 전환시키고 Pool에 Connection이 반환되면 대기 상태에 있는 클라이언트에게 순차적으로 제공된다. <br>
- 왜 사용할까? <br>
  - 매 연결마다 Connection 객체를 생성하고 소멸시키는 비용을 줄일 수 있다. <br>
  - 미리 생성된 Connection 객체를 사용하기 때문에, DB 접근 시간이 단축된다. <br>
  - DB에 접근하는 Connection의 수를 제한하여, 메모리와 DB에 걸리는 부하를 조정할 수 있다. <br>
- Thread Pool <br>
  - 비슷한 맥락으로 Thread pool이라는 개념도 있다. <br>
  - 이 역시 매 요청마다 요청을 처리할 Thread를 만드는것이 아닌, 미리 생성한 pool 내의 Thread를 소멸시키지 않고 재사용하여 효율적으로 자원을 활용하는 기법. <br>
- Thread Pool과 Connection pool <br>
  - WAS에서 Thread pool과 Connection pool내의 Thread와 Connection의 수는 직접적으로 메모리와 관련이 있기 때문에, <br>
  많이 사용하면 할 수록 메모리를 많이 점유하게 된다. 그렇다고 반대로 메모리를 위해 적게 지정한다면, 서버에서는 많은 요청을 처리하지 못하고 대기 할 수 밖에 없다. <br>
  - 보통 WAS의 Thread의 수가 Conncetion의 수보다 많은 것이 좋은데, 그 이유는 모든 요청이 DB에 접근하는 작업이 아니기 때문이다. <br>
  
  
</div>
</details>


--------------------------------------------------------------------------------------------------------

## [ 보안, 암호학 ] 

<details>
<summary> CSRF 공격에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 개념<br>
  - Cross-site request forgery, CSRF, XSRF, 사이트 간 요청 위조<br>
  - 사용자가 웹사이트에 로그인한 상태에서 사이트 간 요청 위조 공격 코드가 삽입된 페이지를 열면, 공격 대상이 되는 웹사이트는 위조된 공격 명령이 믿을 수 있는 사용자로부터 발송된 것으로 판단하게 되어 공격에 노출된다.<br>
- 방어 방법<br>
  - XSS와 마찬가지로, 입력 필터링은 중요한 문제이다.<br>
  - 모든 민감한 동작에 필수로 요구되는 확인 절차가 항상 수행되도록 한다.<br>
  - 민감한 동작에 사용되는 쿠키는 짧은 수명만 갖도록 한다.<br>
- [참고] XSS vs CSRF<br>
  - 사이트 간 스크립팅(XSS)을 이용한 공격이 사용자가 특정 웹사이트를 신용하는 점을 노린 것이라면,<br>
  - 사이트간 요청 위조(CSRF)는 특정 웹사이트가 사용자의 웹 브라우저를 신용하는 상태를 노린 것이다.<br>
</div>
</details>


--------------------------------------------------------------------------------------------------------


## [ Java 관련 내용 ]  



<details>
<summary> java 언어의 장단점에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- 장점 <br>
  - 운영체제에 독립적이다. <br>
    - JVM에서 동작하기 때문에, 특정 운영체제에 종속되지 않는다. <br>
  - 객체지향 언어이다. <br>
    - 객체지향적으로 프로그래밍 하기 위해 여러 언어적 지원을 하고있다. (캡슐화, 상속, 추상화, 다형성 등) <br>
    - 객체지향 패러다임의 특성상 비교적 이해하고 배우기 쉽다. <br>
  - 자동으로 메모리 관리를 해준다. <br>
    - JVM에서 Garbage Collector라고 불리는 데몬 쓰레드에 의해 GC(Garbage Collection)가 일어난다. <br>
    GC로 인해 별도의 메모리 관리가 필요 없으며 비지니스 로직에 집중할 수 있다. <br>
  - 오픈소스이다. <br>
    - 정확히 말하면 OpenJDK가 오픈소스이다. OracleJDK는 사용 목적에 따라서 유료가 될 수 있다. <br>
    - 많은 Java 개발자가 존재하고 생태계가 잘 구축되어있다. 덕분에 오픈소스 라이브러리가 풍부하며 잘 활용한다면 짧은 개발 시간 내에 안정적인 애플리케이션을 쉽게 구현할 수 있다. <br>
  - 멀티스레드를 쉽게 구현할 수 있다. <br>
    - 자바는 스레드 생성 및 제어와 관련된 라이브러리 API를 제공하고 있기 때문에 실행되는 운영체제에 상관없이 멀티 스레드를 쉽게 구현할 수 있다. <br>
  - 동적 로딩(Dynamic Loading)을 지원한다. <br>
    - 애플리케이션이 실행될 때 모든 객체가 생성되지 않고, 각 객체가 필요한 시점에 클래스를 동적 로딩해서 생성한다. <br>
    - 또한 유지보수 시 해당 클래스만 수정하면 되기 때문에 전체 애플리케이션을 다시 컴파일할 필요가 없다. 따라서 유지보수가 쉽고 빠르다. <br>
- 단점 <br>
  - 비교적 속도가 느리다. <br>
    - 자바는 한 번의 컴파일링으로 실행 가능한 기계어가 만들어지지 않고 JVM에 의해 기계어로 번역되고 실행하는 과정을 거치기 때문에 <br>
    C나 C++의 컴파일 단계에서 만들어지는 완전한 기계어보다는 속도가 느리다. <br> 
    - 그러나 하드웨어의 성능 향상과 바이트 코드를 기계어로 변환해주는 JIT 컴파일러 같은 기술 적용으로 JVM의 기능이 향상되어 속도의 격차가 많이 줄어들었다.<br>
  - 예외처리가 불편하다. <br>
    - 프로그래머 검사가 필요한 예외가 등장한다면 무조건 프로그래머가 선언을 해줘야 한다. <br> <br>
    
</div>
</details>



<details>
<summary> JVM에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/95de439e-875c-41db-b728-ebc20b0ad355)


- JVM은, 다른 프로그램을 실행시키는 것이 목적이다.<br>
갖춘 기능으로는 크게 2가지로 말할 수 있다.<br>

1. 자바 프로그램이 어느 기기나 운영체제 상에서도 실행될 수 있도록 하는 것
2. 프로그램 메모리를 관리하고 최적화하는 것 <br><br>
  
- 개발자들이 말하는 JVM은 보통 자바 앱에 대한 리소스를 대표하고 통제하는 서버를 지칭한다.<br>

- 자바 애플리케이션을 클래스 로더를 통해 읽어들이고, 자바 API와 함께 실행하는 역할 그리고
  - JAVA와 OS 사이에서 중개자 역할을 수행하여 OS에 구애받지 않고 재사용을 가능하게 해준다.<br><br><br>
  
  
## JVM에서의 메모리 관리
  
- 실행 과정<br>
  1. 프로그램이 실행되면, JVM은 OS로부터 이 프로그램이 필요로하는 메모리를 할당받음. JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리함<br>

  2. 자바 컴파일러(JAVAC)가 자바 소스코드를 읽고, 자바 바이트코드(.class)로 변환시킴<br>
  
  3. 변경된 class 파일들을 클래스 로더를 통해 JVM 메모리 영역으로 로딩함<br>

  4. 로딩된 class파일들은 Execution engine을 통해 해석됨<br>

  5. 해석된 바이트 코드는 메모리 영역에 배치되어 실질적인 수행이 이루어짐. 이러한 실행 과정 속 JVM은 필요에 따라 스레드 동기화나 가비지 컬렉션 같은 메모리 관리 작업을 수행함 <br><br>
  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/21b369b3-7504-48e6-b154-a5dc392fe291)

  - 자바 컴파일러<br>
    - 자바 소스코드(.java)를 바이트 코드(.class)로 변환시켜줌<br><br>
  
  - 클래스 로더<br>
    - JVM은 런타임시에 처음으로 클래스를 참조할 때 해당 클래스를 로드하고 메모리 영역에 배치시킴. 
    - 이 동적 로드를 담당하는 부분이 바로 클래스 로더<br><br>
  
  
  - Runtime Data Areas <br>
    - JVM이 운영체제 위에서 실행되면서 할당받는 메모리 영역
    - 총 5가지 영역으로 나누어짐 : PC 레지스터, JVM 스택, 네이티브 메서드 스택, 힙, 메서드 영역
    - 이 중에 힙과 메서드 영역은 모든 스레드가 공유해서 사용함<br><br>

      - 스택 영역 : 지역변수, 매개변수, 메서드 정보, 임시 데이터 등을 저장<br>
      - 힙 영역 : 런타임에 동적으로 할당되는 데이터가 저장되는 영역. 객체나 배열 생성이 여기에 해당함 <br>
        - 또한 힙에 할당된 데이터들은 가비지컬렉터의 대상이 됨. JVM 성능 이슈에서 가장 많이 언급되는 공간 <br>
      - 메서드 영역 : JVM이 시작될 때 생성됨. <br>
        - JVM이 읽은 각각의 클래스와 인터페이스에 대한 런타임 상수 풀, 필드, 메서드 코드, 정적 변수, 메서드의 바이트 코드 등을 보관함<br>
  
  <br><br>

<br><br>
</div>
</details>



<details>
<summary> 가비지 컬렉션에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br><br>
  
- Garbage Collection<br>
  - C/C++ 언어와 달리 자바는 개발자가 명시적으로 객체를 해제할 필요가 없음<br>
  - 사용하지 않는 객체는 메모리에서 삭제하는 작업을 GC라고 부르며 JVM에서 GC를 수행함<br>
  - 기본적으로 JVM의 메모리는 총 5가지 영역(class, stack, heap, native method, PC)으로 나뉘는데, GC는 힙 메모리만 다룸<br>
  - 일반적으로 다음과 같은 경우에 GC의 대상이 됨 <br>
    - 객체가 NULL인 경우 (ex. String str = null) <br>
    - 블럭 실행 종료 후, 블럭 안에서 생성된 객체 <br><br><br>
  
 
[ GC의 메모리 해제 과정 ]
  
1. Marking <br>
  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/347ddcb0-fb9e-4dbb-908e-b98f4a1a3a01)

  <br>
  - 프로세스는 마킹을 호출합니다. <br>
  - 이것은 GC가 메모리가 사용되는지 아닌지를 찾아냅니다. <br>
  - 참조되는 객체는 파란색으로, 참조되지 않는 객체는 주황색으로 보여집니다. <br>
  - 모든 오브젝트는 마킹 단계에서 결정을 위해 스캔되어집니다. <br>
  - 모든 오브젝트를 스캔하기 때문에 매우 많은 시간을 소모하게 됩니다. <br><br><br>
  
  
2. Normal Deletion <br>
  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/35dfc113-28b4-4771-9c7e-447730cb922f)

  - 참조되지 않는 객체를 제거하고, 메모리를 반환합니다. <br>
  - 메모리 Allocator는 반환되어 비어진 블럭의 참조 위치를 저장해 두었다가 <br>
    - 새로운 오브젝트가 선언되면 할당되도록 합니다. <br><br><br>
  
3. Compacting <br>
  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/4adbcf66-6767-4b97-8b7e-43fe11b9c57e)

- 퍼포먼스를 향상시키기 위해, 참조되지 않는 객체를 제거하고 또한 남은 참조되어지는 객체들을 묶습니다. <br>
- 이들을 묶음으로서 공간이 생기므로 새로운 메모리 할당 시에 더 쉽고 빠르게 진행 할 수 있습니다.<br><br><br><br>


 [ Generational Gabage Collection ] <br><br>
  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/c371347f-2fe3-497a-b860-d13e903f9c5d)
  
  <br>
  1. Young 영역(Yong Generation 영역) <br>
  
    - 새롭게 생성한 객체의 대부분이 여기에 위치합니다. 
    - 대부분의 객체가 금방 접근 불가능 상태가 되기 때문에 매우 많은 객체가 Young 영역에 생성되었다가 사라집니다. 
    - 이 영역에서 객체가 사라질때 Minor GC 가 발생한다고 말합니다.
  
   <br>
  
  2. Old 영역(Old Generation 영역) <br>
  
    - 접근 불가능 상태로 되지 않아 Young 영역에서 살아남은 객체가 여기로 복사됩니다. 
    - 대부분 Young 영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생합니다. 
    - 이 영역에서 객체가 사라질 때 Major GC(혹은 Full GC) 가 발생한다고 말합니다.

  3. Permanet 영역<br>
    
    - Method Area라고도 합니다.
    - JVM이 클래스들과 메소드들을 설명하기 위해 필요한 메타데이터들을 포함하고 있습니다. 
    - JDK8부터는 PermGen은 Metaspace로 교체됩니다.
  
<br><br><br>
  
[ Generational Garbage Collection 과정 ] <br><br>
  
  1. 어떠한 새로운 객체가 들어오면 Eden Space에 할당합니다.<br>
  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/1c4c5362-28ec-4651-b1ba-01b42c9a4f9d)
  
  <br><br>
  
  2. Eden space가 가득차게 되면, minor garbage collection이 시작됩니다. <br><br>
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/36adf24f-c1c9-4888-a280-302a4c859a97)

  <br><br>
  
  3. 참조되는 객체들은 첫 번째 survivor(S0)로 이동되어지고, 비 참조 객체는 Eden space가 clear 될 때 반환됩니다. <br><br>
![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/8a011997-97c4-47f3-adfd-6cc0dd74c658)

 <br><br>
  
  4. 다음 minor GC 때, Eden space에서는 같은 일이 일어납니다.<br>
  비 참조 객체는 삭제되고 참조 객체는 survivor space로 이동하는 것 입니다.<br>
  그러나 이 케이스에서 참조 객체는 두 번째 survivor space로 이동하게 됩니다. <br>
  최근 minor GC에서 첫 번째 survivor space로 이동된 객체들도 age가 증가하고 S1 공간으로 이동하게 됩니다.<br>
  한번 모든 surviving 객체들이 S1으로 이동하게 되면 S0와 Eden 공간은 Clear 됩니다. <br>
  주의해야할 점은 이제 우리는 다른 aged 객체들을 서바이버 공간에 가지게 되었다는 것입니다.<br>
  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/69740f02-500f-4a78-9a9f-eaca24701926)
  
   <br><br>
  
  5. 다음 minor GC 때, 같은 과정이 반복 됩니다. <br>
  그러나 이 번엔 survivor space들은 switch 됩니다. <br> 
  참조되는 객체들은 S0로 이동합니다. <br>
  살아남은 객체들은 aged 되고 Eden과 S1 공간은 Clear 됩니다. <br>
  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/c3e4b065-3991-49fb-8e44-da625e560e0c)

   <br><br>

   6. 아래 그림은 promotion을 보여줍니다. <br> 
      minor GC 후 aged 오브젝트들이 일정한 age threshold(문지방)을 넘게 되면 그들은 young generation에서 old로 promotion 되어집니다. <br> 
      여기서는 8을 예로 들었습니다. <br> 

  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/a80c89ab-e9cf-4027-8b26-30eba2db0ba4)

  <br><br>


  7. minor GC가 계속되고 계속해서 객체들이 Old Generation으로 이동됩니다. <br>

  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/3ff2a8ab-67a7-4004-b700-b8dcc1531e3e)

  <br><br>

  8. 아래 그림은 전 과정을 보여주고 있습니다.<br>
     결국 major GC가 old Generation에 시행되고, old Generation은 Clear 되고, 공간이 Compact 되어집니다.<br>

  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/f443a389-ba1d-41bb-8c98-8096a7601236)




<br><br><br>
  
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
<summary> 자바 컴파일 순서에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br><br> 

  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/0bf7a8ee-d166-44f4-9afe-ad1ddc115163)

  <br><br>
1. 개발자가 자바 소스코드(.java)를 작성합니다. <br><br>

2. 자바 컴파일러(Java Compiler)가 자바 소스파일을 컴파일합니다. <br>
이 때 나오는 파일이 자바 바이트 코드(.class)파일이고  <br>
아직 컴퓨터가 읽을 수 없는 상태이며,  <br>
자바 가상 머신이 이해할 수 있는 코드입니다. <br><br>

3. 컴파일된 바이트 코드를 JVM의 클래스로더(Class Loader)에게 전달합니다.<br><br>

4. 클래스 로더는 동적로딩(Dynamic Loading)을 통해 필요한 클래스들을 로딩 및 링크하여 런타임 데이터 영역(Runtime Data area), <br>
  즉 JVM의 메모리에 올립니다.<br>

  - 클래스 로더 세부 동작.<br>
    - 로드 : 클래스 파일을 가져와서 JVM의 메모리에 로드합니다.<br>
    - 검증 : 자바 언어 명세(Java Language Specification) 및 JVM 명세에 명시된 대로 구성되어 있는지 검사합니다.<br>
    - 준비 : 클래스가 필요로 하는 메모리를 할당합니다. (필드, 메서드, 인터페이스 등등).<br>
    - 분석 : 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경합니다.<br>
    - 초기화 : 클래스 변수들을 적절한 값으로 초기화합니다. (static 필드).<br><br>
 
 5. 실행엔진(Execution Engine)은 JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행합니다. <br>
  이때, 실행 엔진은 두가지 방식으로 변경합니다. <br>

   - 인터프리터 : 
    - 바이트 코드 명령어를 하나씩 읽어서 해석하고 실행합니다.<br>
    - 하나하나의 실행은 빠르나, 전체적인 실행 속도가 느리다는 단점을 가집니다.<br>
  
   - JIT 컴파일러(Just-In-Time Compiler) : <br>
    - 인터프리터의 단점을 보완하기 위해 도입된 방식으로 <br>
      - 바이트 코드 전체를 컴파일하여 바이너리 코드로 변경하고 이후에는 해당 메서드를 더이상 인터프리팅 하지 않고, 바이너리 코드로 직접 실행하는 방식입니다. <br>
    - 하나씩 인터프리팅하여 실행하는 것이 아니라 바이트 코드 전체가 컴파일된 바이너리 코드를 실행하는 것이기 때문에 전체적인 실행속도는 인터프리팅 방식보다 빠릅니다. <br><br>

  
  ![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/152de882-bf58-4b83-b4f4-8210f3a41d16)

<br><br>
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
<summary> java Set 인터페이스 구현체의 종류에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- HashSet <br>
   - 저장 순서를 유지하지 않는 데이터의 집합이다. <br>
   - 해시 알고리즘(hash algorithm)을 사용하여 검색 속도가 매우 빠르다. <br>
   - 내부적으로 HashMap 인스턴스를 이용하여 요소를 저장한다. <br>
- LinkedHashSet <br>
   - 저장 순서를 유지하는 HashSet <br>
- TreeSet <br>
  - 데이터가 정렬된 상태로 저장되는 이진 탐색 트리(binary search tree)의 형태로 요소를 저장한다. <br>
   - 이진 탐색 트리 중에 성능을 향상시킨 레드-블랙 트리(Red-Black tree)로 구현되어 있다. <br>
   - Compartor 구현으로 정렬 방법을 지정할 수 있다. <br>
</div>
</details>



<details>
<summary> java List 인터페이스 구현체의 종류에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- ArrayList <br>
   - 단방향 포인터 구조로 각 데이터에 대한 인덱스를 가지고 있어 데이터 검색에 적합하다. <br>
   - 데이터의 삽입, 삭제 시 해당 데이터 이후 모든 데이터가 복사되므로 삽입, 삭제가 빈번한 데이터에는 부적합하다. <br>
- LinkedList <br>
   - 양방향 포인터 구조로 데이터의 삽입, 삭제 시 해당 노드의 주소지만 바꾸면 되므로 삽입, 삭제가 빈번한 데이터에 적합하다. <br>
   - 데이터의 검색 시 처음부터 노드를 순회하므로 검색에는 부적합하다. <br>
   - 스택, 큐, 양방향 큐 등을 만들기 위한 용도로 쓰인다. <br>
- Vector <br>
   - 내부에서 자동으로 동기화 처리가 일어난다. <br>
   - 성능이 좋지 않고 무거워 잘 쓰이지 않는다. <br>
</div>
</details>

  

<details>
<summary> 제네릭에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

 <br> <br>

- 제네릭이란 <br>
  - JDK1.5 에 처음 도입되었다. <br>
  - Generics add stability to your code by making more of your bugs detectable at compile time. – Oracle Javadoc <br>
  - 제네릭은 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법을 의미한다. – 생활코딩 <br>
  - 제네릭은 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입체크를 해주는 기능이다. – 자바의 정석 <br>

 <br> <br>
 
- 제네릭이 왜 좋을까? <br>
  - 우선 컴파일 타임에 타입을 체크하기 때문에 객체 자체의 타입 안전성을 높일 수 있다.
    개발자가 의도하지 않은 타입의 객체가 저장되는 것을 방지할 수 있고 
    저장한 객체를 다시 가져올 때 기존 타입과 다른 타입으로 캐스팅되어 발생하는 오류(ClassCastException)를 줄일 수 있다.
  - 형 변환(Type Casting)의 번거로움을 줄일 수 있다.
  - 제네릭없이 최상위 객체 Object를 사용한다면 아래와 같이 코드를 작성할 수 있다.

 <br>
 
```java
class MadPlay {
    private Object obj;

    public MadPlay(Object obj) { this.obj = obj; }
    public Object getObj() { return obj; }
}

class GenericTester {
    public void executeMethod() {
        MadPlay instance1 = new MadPlay(new String("Hello"));
        MadPlay instance2 = new MadPlay(new Integer(123));
        MadPlay instance3 = new MadPlay(new Character('a'));

        String obj1 = (String) instance1.getObj();
        Integer obj2 = (Integer) instance2.getObj();
        Character obj3 = (Character) instance3.getObj();
    }
}
```

 <br> <br>
 
- 하지만 여기서 제네릭을 사용하면 타입 캐스팅을 하지 않아도 된다.
- 변환하여 사용할 객체의 타입을 사전에 명시하므로서 타입 캐스팅의 수고를 줄일 수 있다.

 <br>
 
```java
class GenericMadPlay<T> {
    private T obj;

    public GenericMadPlay(T obj) { this.obj = obj; }
    public T getObj() { return obj; }
}

class GenericTester {
    public void executeMethod() {
        GenericMadPlay<String> genericInstance1 = new GenericMadPlay<>("Hello");
        GenericMadPlay<Integer> genericInstance2 = new GenericMadPlay<>(123);
        GenericMadPlay<Character> genericInstance3 = new GenericMadPlay<>('a');

        String genericObj1 = genericInstance1.getObj();
        Integer genericObj2 = genericInstance2.getObj();
        Character genericObj3 = genericInstance3.getObj();
    }
}
```
<br><br>

- 제네릭 사용시 주의할 점은? <br>

 1. 제네릭은 클래스와 인터페이스만 적용되기 때문에 자바 기본 타입(Primitive Type)은 사용할 수 없다.

<br>

```java
public void someMethod() {
    List<int> intList = new List<>(); // 기본 타입 int는 사용 불가
    List<Integer> integerList = new List<>(); // Okay!
}
```

<br><br>

 2. 제네릭 타입을 사용하여 객체를 생성하는 것은 불가능하다. 즉, 제네릭 타입의 객체는 생성이 불가능하다. 

 <br>

```java
public void someMethod() {
    // Type parameter 'T' cannot be instantiated directly
    T t = new T();
    return t;
}
```

<br><br>

3. 제네릭에서는 배열에 대한 제한을 두고 있다. 제네릭 클래스 또는 인터페이스 타입의 배열을 선언할 수 없다. 하지만 제네릭 타입의 배열 선언은 허용된다.

<br>

```java
public void someMethod() {
    // generic array creation
    // (자바 8이전) Cannot create a generic array of MadPlay<Integer>
    MadPlay<Integer>[] arr1 = new MadPlay<>[10];
    
    MadPlay<Integer>[] arr2 = new MadPlay[10]; // Okay!
}
```

 <br> <br>

</div>
</details>



<details>
<summary> java의 데이터 타입에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/5b94c67b-5095-4b37-a525-e54ab726bbc4)

<br><br>


  
1. 기본 데이터 타입(Primitive Data Type) <br>
- JAVA에서는 총 8가지의 Primitive type을 미리 정의하고 제공합니다.
- 자바에서 기본 자료형은 반드시 사용하기 전에 선언(Declared)되어야 합니다.
- OS에 따라 자료형의 길이가 변하지 않습니다.
- 비객체 타입입니다. 따라서 null 값을 가질 수 없습니다. 만약 Primitive type에 Null을 넣고 싶다면 Wrapper Class를 활용합니다.
- 스택(Stack) 메모리에 저장됩니다.  <br> <br>

![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/13873db3-e780-4f76-8584-8453e5832447)

 <br>

- boolean  <br>
  - 논리형인 boolean의 기본값은 false이며 참과 거짓을 저장하는 타입입니다.  <br>
  - 주로 yes/no, on/off 등의 논리 구현에 주로 사용되며 두가지 값만 표현하므로 가장 크기가 작습니다.  <br>
  - boolean은 실제로 1bit면 충분하지만, 데이터를 다루는 최소 단위가 1byte이므로 메모리 크기가 1byte입니다.  <br>
  
 <br>
 
- int  <br>
  - int 형은 자바에서 정수 연산을 하기 위한 기본 타입입니다. 
  - byte 혹은 short 의 변수가 연산을 하면 연산의 결과는 int형이 됩니다. <br>
  
 <br>
 
- long <br>
  - 수치가 큰 데이터를 다루는 프로그램(은행 및 우주와 관련된 프로그램)에서 주로 사용합니다. <br>
  - long 타입의 변수를 초기화 할 떄에는 정수값 뒤에 알파벳 L을 붙여서 long 타입(즉, 8byte)의 정수 데이터임을 알려주어야 합니다. <br> 
  - 만일 정수값이 int의 값의 저장 범위를 넘는 정수에서 L을 붙이지 않는다면 컴파일 에러가 발생합니다. <br>

<br>

- float, double
  - 실수를 가수와 지수 형식으로 저장하는 부동소수점 방식으로 저장됩니다.
  - 가수를 표현하는데 있어 double형이 float형보다 표현 가능 범위가 더 크므로 double형이 보다 정밀하게 표현할 수 있습니다.
  - 자바에서 실수의 기본 타입은 double형이므로 float형에는 알파벳 F를 붙여서 float 형임을 명시해주어야 합니다.

 <br> <br>

 

2. 참조 타입(Reference Data Type) <br>
- JAVA에서 Primitive type을 제외한 타입들이 모두 Reference type 입니다.
- 클래스 타입(class type) , 인터페이스 타입(interface type) , 배열 타입(array type) , 열거 타입(enum type) 이 있습니다. <br>
- String과 배열은 참조 타입과 달리 new 없이 생성이 가능하지만 기본 타입이 아닌 참조 타입입니다. <br>
- new 키워드를 이용하여 객체를 생성하여 데이터가 생성된 주소를 참조하는 타입입니다.<br>
- Reference type은 JAVA에서 최상인 java.lang.Object클래스를 상속하는 모든 클래스들을 말합니다.<br>
  -  new를 통하여 생성하는 객체는 메모리 영역인 Heap 영역에 생성을 하게되고, Garbage Collector가 돌면서 메모리를 해제합니다.<br>
- 참조 타입은 값이 저장된 곳의 주소를 저장하는 공간으로 객체의 주소를 저장합니다. (Call-By-Value)<br>
- 빈 객체를 의미하는 Null이 존재합니다.<br>
- 문법상으로는 에러가 없지만 실행시켰을 때 에러가 나는 런타임 에러가 발생합니다. 예를 들어 객체나 배열을 Null 값으로 받으면 NullPointException이 발생하므로 변수 값을 넣어야 합니다.
- Heap 메모리에 생성된 인스턴스는 메소드나 각종 인터페이스에서 접근하기 위해 JVM의 Stack 영역에 존재하는 Frame에 일종의 포인터(C의 포인터와는 다릅니다.)인 참조값을 가지고 있어 이를 통해 인스턴스를 핸들링합니다.

<br>
  
![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/ff43abd4-12fc-44eb-80ba-32354b9f0e1e)


<br> <br>

</div>
</details>



<details>
<summary> 동기화와 비동기화의 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 동기화(Syncronous) <br>
  - 한 자원에 동시에 접근하는 것 제한 <br>
  - 순차적으로 진행 <br> 
  - 다음에 실행될 명령은 현재 실행 중인 명령 종료 시까지 대기 (대기시간 버퍼링 발생) <br>
  - 서버와 클라이언트가 주고 받는 것이 동시에 이루어지는 형태 <br>
  - 시간적인 동기화가 필요한 곳에 많이 사용 <br>
  - ex. 현금인출기 <br>
  - Java에서 synchronized 키워드 사용 <br> 
    - 자바에서 멀티 스레드 접근 제한 키워드 <br>
    - 메소드 단위, 블록 단위 적용 가능 <br>
    - 단, 메소드 단위로 지정할 경우 메소드 전체에 lock이 걸리기 때문에 가능하면 블록 활용 (임계 영역은 작을 수록 좋음) <br>
<br>

- 비동기화(Asyncronous) <br>
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



<details>
<summary> java에서 ==와 equals()의 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- "==" <br>
  - 항등 연산자(Operator) 이다. <br>
    - <--> != <br>
  - 참조 비교(Reference Comparison) ; (주소 비교, Address Comparison) <br>
    - 두 객체가 같은 메모리 공간을 가리키는지 확인한다. <br>
  - 반환 형태: boolean type <br>
    - 같은 주소면 return true, 다른 주소면 return false <br>
  - 모든 기본 유형(Primitive Types)에 대해 적용할 수 있다. <br>
    - byte, short, char, int, float, double, boolean <br><br>
- "equals()" <br>
  - 객체 비교 메서드(Method) 이다. <br>
  - <--> !(s1.equals(s2)); <br>
  - 내용 비교(Content Comparison) <br>
    - 두 객체의 값이 같은지 확인한다. <br>
    - 즉, 문자열의 데이터/내용을 기반으로 비교한다. <br>
  - 기본 유형(Primitive Types)에 대해서는 적용할 수 없다. <br>
  - 반환 형태: boolean type <br>
    - 같은 내용이면 return true, 다른 내용이면 return false <br><br>
    
- "==" VS "equals()" 예시
```java
public class Test {
    public static void main(String[] args) {
        // Thread 객체
        Thread t1 = new Thread();
        Thread t2 = new Thread(); // 새로운 객체 생성. 즉, s1과 다른 객체.
        Thread t3 = t1; // 같은 대상을 가리킨다.
        // String 객체
        String s1 = new String("WORLD");
        String s2 = new String("WORLD");
        /* --print-- */
        System.out.println(t1 == t3); // true
        System.out.println(t1 == t2); // false(서로 다른 객체이므로 별도의 주소를 갖는다.)
        System.out.println(t1.equals(t2)); // false
        System.out.println(s1.equals(s2)); // true(모두 "WORLD"라는 동일한 내용을 갖는다.)
    }
```

</div>
</details>



<details>
<summary> CheckedException과 UnCheckedException의 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
  ![image](https://user-images.githubusercontent.com/67456294/207458000-74186bea-6238-4187-98ee-3a763844edc1.png)


- Checked Exception
  - 명시적인 예외 처리를 강제하기 때문에 Checked Exception이라 한다.
  - 반드시 try ~ catch로 예외를 잡거나 throw로 호출한 메소드에게 예외를 던져야 한다.
  - Checked Exception은 RuntimeException을 상속하지 않은 클래스이며, 명시적인 예외 처리를 해야 한다. 
  - 컴파일 시점에 확인할 수 있고 트랜잭션 안에서 동작할 때 Checked Exception이 발생하면 롤백되지 않는다는 특징이 있다.
  
- Unchecked Exception
  - 명시적인 예외 처리를 강제하지 않기 때문에 Uncheked Exception이라고 한다. 
  - 명시적인 예외 처리란 try ~ catch로 예외를 잡거나 throw로 호출한 메소드에게 예외를 던지지 않는 행위를 말한다.
  - Unchecked Exception은 RuntimeException을 상속한 클래스이며, 명시적인 예외 처리를 하지 않는다. 
  - 런타임 시점에 확인할 수 있고 트랜잭션 안에서 동작할 때 Unchecked Exception이 발생하면 롤백된다는 특징이 있다.
  
- 올바른 예외처리 방식?
  - 예외 복구 전략이 명확하고 복구가 가능하다면 Checked Excetpion을 try-catch로 잡아서 예외를 복구하는 것이 좋다. 
  - 복구가 불가능한 Checked Exception이 발생하면 더 구체적인 Unchecked Exception을 발생시키고 예외에 대한 메시지를 명확하게 전달하는 것이 좋다. 
  - 무책임하게 상위 메서드에 throw로 예외를 던지는 것은 상위 메서드의 책임이 증가하기 때문에 좋지 않은 방법이다.

</div>
</details>



<details>
<summary> String vs StringBuffer vs StringBuilder 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

![image](https://github.com/developerOlive/Backend_interview_question/assets/67456294/ab31d99a-d21f-4dcc-8c32-698ca934a119)


- String <br>
    - immutable(불변) <br>
    - new 연산을 통해 생성된 인스턴스의 메모리 공간은 변하지 않는다. (Immutable) <br>
      - 할당 시 Heap String Pool영역에 생성되어 그 값을 계속 사용한다. <br>
    - Garbage Collector로 제거되어야 한다. <br>
    - 객체가 불변하므로, Multithread에서 동기화를 신경 쓸 필요가 없음. (조회 연산에 매우 큰 장점)<br>
    - 엄청나게 많은 문자열을 선언 및 연산할 때는 성능저하를 고려해야 한다.<br>
    - 문자열 연산이 적고, 조회가 많은 멀티쓰레드 환경에서 좋다.<br>

- StringBuffer, StringBuilder<br>
  - 공통점<br>
    - new 연산으로 클래스를 한 번만 만듬 (Mutable)<br>
    - 문자열 연산시 새로 객체를 만들지 않고, 크기를 변경시킴<br>
    - StringBuffer와 StringBuilder 클래스의 메서드가 동일함<br>
  - 차이점<br>
    - StringBuffer는 Thread-Safe함 / StringBuilder는 Thread-safe하지 않음 (불가능)<br>
    - StringBuffer 클래스 : 문자열 연산이 많은 Multi-Thread 환경<br>
    - StringBuilder 클래스 : 문자열 연산이 많은 Single-Thread 또는 Thread 신경 안쓰는 환경<br>


<정리><br>
- String은 짧은 문자열을 더할 경우 사용한다.<br>
- StringBuffer는 스레드에 안전한 프로그램이 필요할 때나, 개발 중인 시스템의 부분이 스레드에 안전한지 모를 경우 사용하면 좋다.<br>
- StringBuilder는 스레드에 안전한지 여부가 전혀 관계 없는 프로그램을 개발할 때 사용하면 좋다. <br>
- 멀티스레드 환경이라면 값 동기화 보장을 위해 StringBuffer를 사용하고,<br>
  단일스레드 환경이라면 StringBuilder를 사용하는 것이 좋다.<br>
- 단순히 성능만 놓고 본다면 연산이 많은 경우, StringBuilder > StringBuffer >>> String 이다.<br>

<br><br>

</div>
</details>



<details>
<summary> 자바의 메모리 영역에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 메서드 영역<br>
  - static 변수, 전역 변수, 코드에서 사용되는 Class 정보 등이 할당된다.<br>

- 스택(Stack)<br>
  - 지역 변수, 함수(메서드) 등이 할당되는 LIFO(Last In First Out) 방식의 메모리이다.<br>

- 힙(Heap)<br>
    - new 연산자를 통한 동작할당된 객체들이 저장되며, 가비지 컬렉션에 의해 메모리가 관리된다.<br>

</div>
</details>



<details>
<summary> new String()과 “”의 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- Java에서 문자열은 Heap 영역 내의 String Pool이라는 곳에서 따로 관리하게 된다.
- "" 으로 선언된 String은 String Pool에 추가가 되고 해당 값을 참조 값으로 가지게 된다.
- 반면 new String()으로 생성된 String은 String Pool이 아닌 Heap 영역에 새로운 객체를 등록하게 된다.
- 즉, 위 두 방법으로 객체를 생성하였을 경우 각 객체의 메모리상의 위치가 다르다.

</div>
</details>



<details>
<summary> 접근제어자에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- public : 어디서든 접근이 가능합니다.
- protected : 동일 패키지 혹은 상속받은 외부 패키지 클래스에서 사용 가능합니다.
- (default) : 동일 패키지 내에서만 접근 가능합니다.
- private : 해당 클래스 내에서만 접근 가능합니다.

</div>
</details>



<details>
<summary> 객체 지향적 설계 원칙의 종류에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

1.SRP(Single Responsibility Principle) : 단일 책임 원칙 <br>
클래스는 단 하나의 책임을 가져야 하며 클래스를 변경하는 이유는 단 하나의 이유여야 합니다. <br>
<br>
2. OCP(Open-Closed Principle) : 개방-폐쇄 원칙 <br>
확장에는 열려 있어야 하고 변경에는 닫혀 있어야 합니다.<br>
<br>
3. LSP(Liskov Substitution Principle) : 리스코프 치환 원칙<br>
상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 합니다.<br>
<br>
4. ISP(Interface Segregation Principle) : 인터페이스 분리 원칙 <br>
인터페이스는 그 인터페이스를 사용하는 클라이언트를 기준으로 분리해야 합니다. <br>
<br>
5. DIP(Dependency Inversion Principle) : 의존 역전 원칙<br>
고수준 모듈은 저수준 모듈의 구현에 의존해서는 안됩니다.<br>

</div>
</details>



--------------------------------------------------------------------------------------------------------

## [ Spring ] 

<details>
<summary> Spring Framework에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- 스프링 프레임워크는 자바 개발을 편리하게 해주는 오픈소스 프레임워크다.<br>

  - 경량 컨테이너로서 자바 객체를 직접 관리<br>
    - 각각의 객체 생성, 소멸과 같은 라이프 사이클을 관리하며 스프링으로부터 필요한 객체를 얻어올 수 있다.<br><br>
    
  - 제어의 역전(IoC)이라는 기술을 통해 어플리케이션의 느슨한 결합을 도모<br>
    - 컨트롤의 제어권이 사용자가 아닌 프레임워크에 있어서 필요에 다라 스프링에서 사용자의 코드를 호출한다.<br><br>
    
  - 의존성 주입(DI, Dependency Injection)을 지원<br>
    - 각각의 계층이나 서비스들 간에 의존성이 존재할 경우 프레임워크가 서로 연결시켜준다.<br><br>
    
  - 관점 지향 프로그래밍(AOP, Aspect-Oriented Programming)을 지원<br>
    - 트랜잭션이나 로깅, 보안과 같이 여러 모듈에서 공통적으로 사용하는 기능의 경우 해당 기능을 분리하여 관리할 수 있다.<br>
<br>

</div>
</details>


<details>
<summary> Bean에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- 컨테이너 안에 들어있는 객체 <br>
- 컨테이너에 담겨있으며, 필요할 때 컨테이너에서 가져와서 사용 <br>
- @Bean 을 사용하거나 xml 설정을 통해 일반 객체를 Bean으로 등록할 수 있고, Bean으로 등록된 객체는 쉽게 주입하여 사용 가능 <br><br>

</div>
</details>


<details>
<summary> Bean을 등록하는 방법에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
1. 우선 가장 쉬운 방법으로 @Component 어노테이션을 사용하는 것입니다.<br>
@Controller, @Service, @Repository는 모두 @Component를 포함하고 있습니다.<br>
<br>

2. 설정 클래스를 따로 만들어 @Configuration 어노테이션을 붙이고,<br>
해당 클래스 안에서 빈으로 등록할 메소드를 만들어 @Bean 어노테이션을 붙여주면 자동으로 해당 타입의 빈 객체가 생성됩니다.<br>
<br>

</div>
</details>



<details>
<summary> Bean 생명주기에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- 스프링 IoC 컨테이너 생성 → 스프링 빈 생성 → 의존관계 주입 → 초기화 콜백 메소드 호출 →  사용 → 소멸 전 콜백 메소드 호출 → 스프링 종료  <br>
<br>

- 스프링 컨테이너에 의해 생명주기 관리 <br>
- 스프링 컨테이너 종료 시 빈 객체 소멸 <br> <br>

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
- 컨테이너의 종류로는 BeanFactory, ApplicationContext가 있습니다. 
<br>

</div>
</details>


<details>
<summary> Bean Scope에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

![image](https://user-images.githubusercontent.com/67456294/234728511-f0ef56b3-d312-442d-94dc-f0774795768f.png)


- Bean Scope라는 것은 Bean의 범위
- Bean Scope는 객체를 만들 때 컨테이너가 이 객체를 한 번만 호출하는지, 아니면 호출 할 때마다 여러 번 만드는지에 대한 내용이다. <br>
- 여러 Scope가 있는 걸 볼 수 있고, 대부분 singleton 혹은 prototype이다. <br>
- 스프링은 기본적으로 모든 bean을 singleton으로 생성하여 관리한다. <br>
- 구체적으로는 애플리케이션 구동 시 JVM 안에서 스프링이 bean마다 하나의 객체를 생성하는 것을 의미한다. <br>
- 그래서 우리는 스프링을 통해서 bean을 제공받으면 언제나 주입받은 bean은 동일한 객체라는 가정하에서 개발을 한다. <br><br><br><br>


![image](https://user-images.githubusercontent.com/67456294/234728524-e592dc75-e97e-42a2-980b-8073e27e33d9.png)

1. Singleton <br>
- ‘singleton’ bean은 Spring 컨테이너에서 한 번 생성된다.<br>
  - 컨테이너가 사라질 때 bean도 제거된다.<br>
- 기본적으로 모든 bean은 scope이 명시적으로 지정되지 않으면 singleton이다.<br>
- 생성된 하나의 인스턴스는 single beans cache에 저장되고, 해당 bean에 대한 요청과 참조가 있으면 캐시된 객체를 반환한다.
  - 하나만 생성되기 때문에 동일한 것을 참조한다.<br><br><br><br>

  
  ![image](https://user-images.githubusercontent.com/67456294/234728537-6f049b24-0983-4522-9490-c63835c93aa2.png)

2. Prototype <br>
- ‘prototype’ bean은 모든 요청에서 새로운 객체를 생성하는 것을 의미한다. <br>
  - 즉, prototype bean은 의존성 관계의 bean에 주입 될 때 새로운 객체가 생성되어 주입된다. <br>
- 정상적인 방식으로 gc에 의해 bean이 제거된다. <br><br><br>


- 싱글톤으로 적합한 객체는? <br>
  - (1) 상태가 없는 공유 객체: <br>
    - 상태를 가지고 있지 않은 객체는 동기화 비용이 없다. 따라서 매번 이 객체를 참조하는 곳에서 새로운 객체를 생성할 이유가 없다.<br>
  - (2) 읽기용으로만 상태를 가진 공유 객체: <br>
    - 1번과 유사하게 상태를 가지고 있으나 읽기 전용이므로 여전히 동기화 비용이 들지 않는다. 매 요청마다 새로운 객체 생성할 필요가 없다.<br>
  - (3) 공유가 필요한 상태를 지닌 공유 객체: <br>
    - 객체 간의 반드시 공유해야 할 상태를 지닌 객체가 하나 있다면, 이 경우에는 해당 상태의 쓰기를 가능한 동기화 할 경우 싱글톤도 적합하다.<br>
  - (4) 쓰기가 가능한 상태를 지니면서도 사용빈도가 매우 높은 객체: <br>
    - 애플리케이션 안에서 정말로 사용빈도가 높다면, 쓰기 접근에 대한 동기화 비용을 감안하고서라도 싱글톤을 고려할만하다. <br>
      - 이 방법은 1. 장시간에 걸쳐 매우 많은 객체가 생성될 때, <br>
      - 2. 해당 객체가 매우 작은 양의 쓰기상태를 가지고 있을 때, <br>
      - 3. 객체 생성비용이 매우 클 때에 유용한 선택이 될 수 있다.<br>

- 비싱글톤으로 적합한 객체는? <br>
  - (1) 쓰기가 가능한 상태를 지닌 객체: <br>
    - 쓰기가 가능한 상태가 많아서 동기화 비용이 객체 생성 비용보다 크다면 싱글톤으로 적합하지 않다. <br>
  - (2) 상태가 노출되지 않은 객체: <br>
    - 일부 제한적인 경우, 내부 상태를 외부에 노출하지 않는 빈을 참조하여 다른 의존객체와는 독립적으로 작업을 수행하는 의존 객체가 있다면 <br>
      싱글톤보다 비싱글톤 객체를 사용하는 것이 더 나을 수 있다.<br>




https://gmlwjd9405.github.io/2018/11/10/spring-beans.html

<br>

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
프레임워크의 내부에서 결정된 대로 이뤄지게 되는데, 이러한 현상을 "제어의 역전"이라고 표현합니다. <br><br>

Spring에서의 IoC <br>
- Spring 프레임워크에서 지원하는 Ioc Container는 우리들이 흔히 개발하고 사용해왔던 <br>
일반 POJO(Plain Old Java Object)의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능들을 제공합니다. <br><br> 

라이브러리와 프레임워크의 차이 <br>
- IoC의 개념이 적용되었나의 차이를 의미합니다. <br>
- 라이브러리를 사용하는 애플리케이션 코드는 애플리케이션 흐름을 직접 제어합니다. <br>
- 단지 동작하는 중에 필요한 기능이 있을 때 능동적으로 라이브러리를 시용할 뿐입니다. <br>
- 반면에 프레임워크는 거꾸로 애플리케이션 코드가 프레임워크에 의해 사용됩니다. <br>
- 보통 프레임워크 위에 개발한 클래스를 등록해두고, <br> 
프레임워크가 흐름을 주도히는 중에 개발자가 만든 애플리케이션 코드를 시용하도록 만드는 방식입니다. <br> 

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



<details>
<summary> Filter와 Interceptor 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- Filter, Interceptor <br>
  - 애플리케이션에서 자주 사용되는 기능(공통 부분)을 분리하여 관리할 수 있도록 Spring이 제공하는 기능 <br>

- Filter, Interceptor 흐름 <br> <br> 
![image](https://user-images.githubusercontent.com/67456294/202929031-9a440ce8-01cc-4dfb-aadb-3cf00deadb23.png) <br>

1. 서버 실행 시 Servlet이 올라오는 동안 init 후 doFilter 실행 <br>
2. Dispatcher Servlet을 지나쳐 Interceptor의 preHandler 실행 <br>
3. 컨트롤러를 거쳐 내부 로직 수행 후, Interceptor의 postHandler 실행 <br>
4. doFilter 실행 <br>
5. Servlet 종료 시 destroy <br><br>

Filter 특징 <br>
- Dispatcher Servlet 이전에 수행되고, 응답 처리에 대해서도 변경 및 조작 수행 가능 <br>
- WAS 내의 ApplicationContext에서 등록된 필터가 실행 <br>
- WAS 구동 시 FilterMap이라는 배열에 등록되고, 실행 시 Filter chain을 구성하여 순차적으로 실행 <br>
- Spring Context 외부에 존재하여 Spring과 무관한 자원에 대해 동작 <br>
- 일반적으로 web.xml에 설정 <br>
- 예외 발생 시 Web Application에서 예외 처리 <br>
- ex. 인코딩 변환, XSS 방어 등 <br>
- 실행 메소드 <br>
  - init() : 필터 인스턴스 초기화 <br>
  - doFilter() : 실제 처리 로직 <br>
  - destroy() : 필터 인스턴스 종료 <br>
  
  
Interceptor 특징 <br>
- Dispatcher Servlet 이후 Controller 호출 전, 후에 끼어들어 기능 수행 <br>
- Spring Context 내부에서 Controller의 요청과 응답에 관여하며 모든 Bean에 접근 가능 <br>
- 일반적으로 servlet-context.xml에 설정 <br>
- 예외 발생 시 @ControllerAdvice에서 @ExceptionHandler를 사용해 예외 처리 <br>
- ex. 로그인 체크, 권한 체크, 로그 확인 등 <br>
- 실행 메소드 <br>
  - preHandler() : Controller 실행 전 <br>
  - postHandler() : Controller 실행 후 <br>
  - afterCompletion() : view Rendering 후 <br>
  
  
Filter, Interceptor 차이점 요약 <br>
- Filter는 WAS단에 설정되어 Spring과 무관한 자원에 대해 동작하고, <br>
  - Interceptor는 Spring Context 내부에 설정되어 컨트롤러 접근 전, 후에 가로채서 기능 동작 <br> 
- Filter는 doFilter() 메소드만 있지만, Interceptor는 pre와 post로 명확하게 분리 <br>
- Interceptor의 경우 AOP 흉내 가능 <br>
  - handlerMethod(@RequestMapping을 사용해 매핑 된 @Controller의 메소드)를 파라미터로 제공하여 메소드 시그니처 등 추가 정보를 파악해 로직 실행 여부 판단 가능 <br>

</div>
</details>



<details>
<summary> DAO와 DTO의 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- DAO(Data Access Object) <br>
  - DB의 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 객체를 말한다. <br>
  - DB에 접근을 하기위한 로직과 비즈니스 로직을 분리하기 위해서 사용 한다. <br>
- DTO(Data Transfer Object) <br>
  - 계층간 데이터 교환을 위한 자바빈즈를 말한다. <br>
    - 여기서 말하는 계층은 Controller, View, Business Layer, Persistent Layer 이다. <br>
  - 일반적인 DTO는 로직을 갖고 있지 않는 순수한 데이터 객체이며, 속성과 그 속성에 접근하기 위한 getter, setter 메소드만 가진 클래스이다. <br>
  - VO(Value Object) 라고도 불린다. <br>
    - DTO와 동일한 개념이지만 read only 속성을 가진다. <br>
</div>
</details>



<details>
<summary> @Transactional의 동작 원리에 대해 설명해주세요. </summary>
<div markdown="1">  
<br>
   
- @Transactional이 붙은 메서드를 호출할 경우, 우리 코드에는 어떤 일이 벌어질까? <br>
  - @Transactional이 클래스 내지 메서드게 붙을 때, Spring은 해당 메서드에 대한 프록시를 만든다.<br>
  - 프록시 패턴은 디자인 패턴 중 하나로, 어떤 코드를 감싸면서 추가적인 연산을 수행하도록 강제하는 방법이다.<br>
  - 트랜잭션의 경우, 트랜잭션의 시작과 연산 종료시의 커밋 과정이 필요하므로, 프록시를 생성해 해당 메서드의 앞뒤에 트랜잭션의 시작과 끝을 추가하는 것이다.<br>

- 스프링 컨테이너는 트랜잭션 범위의 영속성 컨텍스트 전략을 기본으로 사용한다.<br>
  - 서비스 클래스에서 @Transactional을 사용할 경우, 해당 코드 내의 메서드를 호출할 때 영속성 컨텍스트가 생긴다는 뜻이다.<br>
  - 영속성 컨텍스트는 트랜잭션 AOP가 트랜잭션을 시작할 때 생겨나고, <br>
  - 메서드가 종료되어 트랜잭션 AOP가 트랜잭션을 커밋할 경우 영속성 컨텍스트가 flush되면서 해당 내용이 반영된다. <br>
  - 이후 영속성 컨텍스트 역시 종료되는 것이다.<br>

</div>
</details>



<details>
<summary> @Transactional에 readOnly 속성을 사용하는 이유에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- 트랜잭션 안에서 수정/삭제 작업이 아닌 ReadOnly 목적인 경우에 주로 사용하며,<br>
영속성 컨텍스트에서 엔티티를 관리 할 필요가 없기 때문에 readOnly를 추가하는 것으로 메모리 성능을 높일 수 있고,<br>
데이터 변경 불가능 로직임을 코드로 표시할 수 있어 가독성이 높아진다는 장점이 있다.<br>
<br>

- readOnly 속성이 없는 보통의 트랜잭션은 데이터 조회 결과 엔티티가 영속성 컨텍스트에 관리되며, <br>
이는 1차 캐싱부터 변경 감지(Dirty Checking)까지 가능하게 된다.<br>
하지만, 조회시 스냅샷 인스턴스를 생성해 보관하기 때문에 메모리 사용량이 증가한다.<br>
  
</div>
</details>


<details>
<summary> @RequestBody, @RequestParam 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- @RequestBody 는 클라이언트가 전송하는 JSON 형태의 HTTP Body 내용을 MessageConverter를 통해 Java Object로 변환시켜주는 역할을 한다. <br>
값을 주입하지 않고 값을 변환 시키므로(Reflection을 사용해 할당), 변수들의 생성자, Getter,Setter가 없어도 정상적으로 할당된다. <br>
하지만, 조회시 스냅샷 인스턴스를 생성해 보관하기 때문에 메모리 사용량이 증가한다. <br>
<br>

- @RequestParam 은 1개의 HTTP 요청 파라미터를 받기 위해 사용한다. <br>
@RequestParam은 필수 여부가 true이기 때문에, 기본적으로 반드시 해당 파라미터가 전송되어야 한다. <br>
전송되지 않으면 400Error를 유발할 수 있으며, 반드시 필요한 변수가 아니라면 required의 값을 false로 설정해줘야 한다. <br>
  
</div>
</details>



<details>
<summary> Spring MVC에 대해 설명해주세요.</summary>
<div markdown="1">  
<br>
  
- MVC는 Model, View, Controller의 약자이며, 각 레이어간 기능을 구분하는데 중점을 둔 디자인 패턴입니다.<br>

- Model은 데이터 관리 및 비즈니스 로직을 처리하는 부분이며, (DAO, DTO, Service 등)<br>

- View는 비즈니스 로직의 처리 결과를 통해 유저 인터페이스가 표현되는 구간입니다. <br>
(html, jsp, tymeleaf, mustache 등 화면을 구성하기도 하고, Rest API로 서버가 구현된다면 json 응답으로 구성되기도 한다.)<br>

- Controller는 사용자의 요청을 처리하고 Model과 View를 중개하는 역할을 합니다. Model과 View는 서로 연결되어 있지 않기 때문에 Controller가 사이에서 통신 매체가 되어줍니다.<br>
  
</div>
</details>



<details>
<summary> MVC는 어떠한 흐름으로 요청을 처리하는지 설명해주세요. </summary>
<div markdown="1">  
<br>
  
  ![image](https://user-images.githubusercontent.com/67456294/212773042-41f7dbdd-9709-4753-a303-a7073fe5f49b.png)

- DispatcherServlet : 클라이언트에게 요청을 받아 응답까지의 MVC 처리과정을 통제한다. <br>
- HandlerMapping : 클라이언트의 요청 URL을 어떤 Controller가 처리할지 결정한다. <br>
 <br>
  
1. 클라이언트는 URL을 통해 요청을 전송한다.
2. 디스패처 서블릿은 핸들러 매핑을 통해 해당 요청이 어느 컨트롤러에게 온 요청인지 찾는다.
3. 디스패처 서블릿은 핸들러 어댑터에게 요청의 전달을 맡긴다.
4. 핸들러 어댑터는 해당 컨트롤러에 요청을 전달한다.
5. 컨트롤러는 비즈니스 로직을 처리한 후에 반환할 뷰의 이름을 반환한다.
6. 디스패처 서블릿은 뷰 리졸버를 통해 반환할 뷰를 찾는다.
7. 디스패처 서블릿은 컨트롤러에서 뷰에 전달할 데이터를 추가한다.
8. 데이터가 추가된 뷰를 반환한다.

</div>
</details>



<details>
<summary> Lombok 및 Lombok이 만드는 메소드들이 실행되는 시점에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- Lombok은 Java 라이브러리이며 반복되는 getter, setter, toString .. 등의 반복 메서드 작성 코드를 줄여주는 코드 다이어트 라이브러리 이다.
  
- Lombok은 메소드를 컴파일 하는 과정에 개입해서 추가적인 코드를 만들어낸다.
  - 이것을 어노테이션 프로세싱이라고 하는데,
  - 어노테이션 프로세싱은 자바 컴파일러가 컴파일 단계에서 어노테이션을 분석하고 처리하는 기법을 말한다.

</div>
</details>


--------------------------------------------------------------------------------------------------------


## [ OS ]  


<details>
<summary> 운영 체제가 무엇인지 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- 운영체제(Operating System)는 컴퓨터 시스템의 하드웨어, 소프트웨어적인 자원들을 효율적으로 운영 및 관리함으로써 <br>
사용자가 컴퓨터를 편리하고 효과적으로 사용할 수 있도록 하는 시스템 소프트웨어입니다. <br>

- 컴퓨터 하드웨어 바로 위에 설치되어 사용자 및 다른 소프트웨어와 하드웨어를 연결하는 소프트웨어 계층 <br>
즉, 중개자 역할을 해주는 프로그램입니다.<br>
<br>

</div>
</details>



<details>
<summary> 운영 체제의 주요 목적이 무엇인지 설명해주세요. </summary>
<div markdown="1">  
<br>
  
1. 자원관리<br>
  - 컴퓨터 시스템 자원 효율적 관리<br>
  - (시스템 자원 - CPU, Memory, I/O장치와 같은 하드웨어 자원과 프로세스, 파일 메시지 등의 소프트웨어 자원)<br>
  
2. 자원 보호<br>
  - 프로그램이나 다른 사용자가 데이터를 삭제하거나 중요 파일에 접근하지 못하게 컴퓨터 자원들 보호<br>
  
3. 인터페이스 제공<br>
  - 하드웨어 인터페이스와 사용자 인터페이스 제공하여 편리하게 사용하도록 지원<br>

<br>

</div>
</details>



<details>
<summary> 프로세스와 스레드의 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 프로세스는 실행 중인 프로그램을 말하며, 
  완벽히 독립적이기 때문에 메모리 영역(Code, Data, Heap, Stack)을 다른 프로세스와 공유하지 않습니다. 
- 프로세스는 최소 1개의 쓰레드(메인 쓰레드)를 가지고 있습니다.
<br>
 
- 쓰레드는 프로세스 내에서 Stack만 따로 할당 받고, 
  그 이외의 메모리 영역(Code, Data, Heap)영역을 공유하기 때문에 다른 쓰레드의 실행 결과를 즉시 확인할 수 있습니다. 
- 쓰레드는 프로세스 내에 존재하며 프로세스가 할당받은 자원을 이용하여 실행됩니다.
<br><br><br>

- 프로그램(Program) 이란<br>
  - 사전적 의미: 어떤 작업을 위해 실행할 수 있는 파일<br>
- 프로세스(Process) 란<br>
  - 사전적 의미: 컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램<br>
    - 메모리에 올라와 실행되고 있는 프로그램의 인스턴스(독립적인 개체)<br>
    - 운영체제로부터 시스템 자원을 할당받는 작업의 단위<br>
    - 즉, 동적인 개념으로는 실행된 프로그램을 의미한다.<br>
  - 할당받는 시스템 자원의 예<br>
    - CPU 시간<br>
    - 운영되기 위해 필요한 주소 공간<br>
    - Code, Data, Stack, Heap의 구조로 되어 있는 독립된 메모리 영역<br>
  - 특징<br>
  ![image](https://user-images.githubusercontent.com/67456294/204920003-0b40e4f5-35e1-439d-a3a4-b13f8fa6b6aa.png)
  
    - 프로세스는 각각 독립된 메모리 영역(Code, Data, Stack, Heap의 구조)을 할당받는다.<br>
    - 기본적으로 프로세스당 최소 1개의 스레드(메인 스레드)를 가지고 있다.<br>
    - 각 프로세스는 별도의 주소 공간에서 실행되며, 한 프로세스는 다른 프로세스의 변수나 자료구조에 접근할 수 없다.<br>
    - 한 프로세스가 다른 프로세스의 자원에 접근하려면 프로세스 간의 통신(IPC, inter-process communication)을 사용해야 한다. <br>
      - (Ex. 파이프, 파일, 소켓 등을 이용한 통신 방법 이용)<br>

- 스레드(Thread) 란<br>
  - 사전적 의미: 프로세스 내에서 실행되는 여러 흐름의 단위<br>
    - 프로세스의 특정한 수행 경로<br>
    - 프로세스가 할당받은 자원을 이용하는 실행의 단위<br>
  - 특징<br>
  ![image](https://user-images.githubusercontent.com/67456294/205172930-1ec43a48-00e1-4517-b3d2-82fc780190ef.png)
  
    - 스레드는 프로세스 내에서 각각 Stack만 따로 할당받고 Code, Data, Heap 영역은 공유한다.<br>
    - 스레드는 한 프로세스 내에서 동작되는 여러 실행의 흐름으로, 프로세스 내의 주소 공간이나 자원들(힙 공간 등)을 같은 프로세스 내에 스레드끼리 공유하면서 실행된다.<br>
    - 같은 프로세스 안에 있는 여러 스레드들은 같은 힙 공간을 공유한다. 반면에 프로세스는 다른 프로세스의 메모리에 직접 접근할 수 없다.<br>
    - 각각의 스레드는 별도의 레지스터와 스택을 갖고 있지만, 힙 메모리는 서로 읽고 쓸 수 있다.<br>
    - 한 스레드가 프로세스 자원을 변경하면, 다른 이웃 스레드(sibling thread)도 그 변경 결과를 즉시 볼 수 있다.<br>
    
- 자바 스레드(Java Thread) 란<br>
  - 일반 스레드와 거의 차이가 없으며, JVM가 운영체제의 역할을 한다.<br>
  - 자바에는 프로세스가 존재하지 않고 스레드만 존재하며, 자바 스레드는 JVM에 의해 스케줄되는 실행 단위 코드 블록이다.<br>
  - 자바에서 스레드 스케줄링은 전적으로 JVM에 의해 이루어진다.<br>
  - 아래와 같은 스레드와 관련된 많은 정보들도 JVM이 관리한다.<br>
    - 스레드가 몇 개 존재하는지<br>
    - 스레드로 실행되는 프로그램 코드의 메모리 위치는 어디인지<br>
    - 스레드의 상태는 무엇인지<br>
    - 스레드 우선순위는 얼마인지<br>
  - 즉, 개발자는 자바 스레드로 작동할 스레드 코드를 작성하고, 스레드 코드가 생명을 가지고 실행을 시작하도록 JVM에 요청하는 일 뿐이다.<br>
</div>
</details>




<details>
<summary> 멀티 스레딩(Multi-threading) 의 장점과 단점에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- 멀티 스레딩이란 하나의 프로세스를 다수의 스레드로 만들어 실행하는 것<br>

- 장점) <br>
  - 하나의 프로세스 내에 다수의 실행 단위들이 존재하여 작업의 수행에 필요한 자원들을 공유하기 때문에 자원의 생성과 관리가 중복되는 것을 줄일 수 있다.<br>

- 단점)<br>
  - 교착상태를 발생시킬 수 있다.<br>
  - 동기화에 주의해야한다.<br>
    <br>
    
</div>
</details>



<details>
<summary>멀티 프로세스 대신 멀티 스레드를 사용하는 이유에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
- 쉽게 설명하면, 프로그램을 여러 개 키는 것보다 하나의 프로그램 안에서 여러 작업을 해결하는 것이다. <br>
![image](https://user-images.githubusercontent.com/67456294/205756712-c9f6b69b-8cbf-44b7-a2fe-aa0cb80f6cf7.png)

1. 자원의 효율성 증대<br>
    - 멀티 프로세스로 실행되는 작업을 멀티 스레드로 실행할 경우, 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리할 수 있다.<br>
      - 프로세스 간의 Context Switching시 단순히 CPU 레지스터 교체 뿐만 아니라 RAM과 CPU 사이의 캐시 메모리에 대한 데이터까지 초기화되므로 오버헤드가 크기 때문<br>
      - 스레드는 프로세스 내의 메모리를 공유하기 때문에 독립적인 프로세스와 달리 스레드 간 데이터를 주고 받는 것이 간단해지고 시스템 자원 소모가 줄어들게 된다.<br>
2. 처리 비용 감소 및 응답 시간 단축<br>
    - 또한 프로세스 간의 통신(IPC)보다 스레드 간의 통신의 비용이 적으므로 작업들 간의 통신의 부담이 줄어든다.<br>
      - 스레드는 Stack 영역을 제외한 모든 메모리를 공유하기 때문<br>
    - 프로세스 간의 전환 속도보다 스레드 간의 전환 속도가 빠르다.<br>
    - Context Switching시 스레드는 Stack 영역만 처리하기 때문<br>
- 주의할 점!<br>
    - 동기화 문제<br>
    - 스레드 간의 자원 공유는 전역 변수(데이터 세그먼트)를 이용하므로 함께 상용할 때 충돌이 발생할 수 있다.<br>
</div>
</details>



<details>
<summary> 교착상태의 개념과 조건에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
  ![image](https://user-images.githubusercontent.com/67456294/206035880-812564b7-c4be-4b70-87e5-ee9b478b1b1d.png)

- 프로세스는 실행을 위해 CPU, 메모리, 파일 등 여러 하드웨어 자원이 필요하다. 이를 운영체제에서 프로세스가 요구하는 자원을 적절히 분배해준다.<br>
- 멀티 프로그래밍 환경에서 한정된 자원을 사용하려고 서로 경쟁하는 상황이 발생 할 수 있다.<br>
- 어떤 프로세스가 자원을 요청 했을 때 그 시각에 그 자원을 사용할 수 없는 상황이 발생할 수 있고 그 때는 프로세스가 대기 상태로 들어 간다.<br>
- 대기 상태로 들어간 프로세스들이 실행 상태로 변경 될 수 없을 때 이러한 상황을 교착 상태라 한다.<br>
<br><br>

교착상태 필요 조건(Necessary Conditions)<br>
- 교착상태가 일어나기 위한 필요 조건이 네 가지가 존재한다. <br>
- 이는 필요 조건이므로, 네 가지가 모두 해당된다고 해서 반드시 교착상태가 일어나는 것은 아니고, 일어날 확률이 생기는 것이다.<br><br>

1. 상호 배제(Mutual Exclusion) : <br>
한 자원에 대한 여러 프로세스의 동시 접근은 불가능하다. 즉, 하나의 자원을 특정 시기에 하나의 프로세스나 스레드만 소유할 수 있는 형태.<br>

2. 점유와 대기(Hold and Wait) : <br>
하나의 자원을 소유하고 다른 프로세스 혹은 스레드의 자원을 요청하는 상태이다.<br>

3. 비선점(Non preemptive)  : 하나의 프로세스나 스레드에게 주어진 자원은 해당 프로세스나 스레드가 스스로 놓기 전에는 놓게 만들 수 없는 상태.<br>
즉, 다른 프로세스에서 자원을 사용하는 동안 자원을 강제로 가져올 수 없다.<br>

4. 환형 대기(Circle wait) : <br>
각 프로세스가 다음 프로세스가 요구하는 자원을 가지고 있는 것을 말한다. <br>
두 개의 프로세스나 스레드의 경우, A -> B, B -> C, C -> A 에게 서로 자원을 요청하고 기다리는 상황<br>

<br>

  - 교착상태는 위 네 가지 조건을 모두 만족하더라도 매우 드물게 일어나는 현상이지만, <br>
    한 번 교착상태에 빠지면 프로세스가 무한 루프에 빠져 수행하지 못하고 해당 프로세스가 가지고 있는 자원은 아무도 사용하지 못한다. <br>
  - 이는 전체 컴퓨터 환경에 매우 치명적이다.<br>
<br><br>

교착상태 처리<br>
1. 교착상태 방지 (Deadlock Prevention)<br>
- 교착상태 방지는 위에서 살펴본 교착상태 필요조건 네 가지 중 최소 한 가지를 만족시키지 않도록 만드는 것이다.<br>

    - 상호배타(Mutual exclusion): 상호배타를 없애기 위해서는 자원을 공유 가능하게 만들어야 한다. 
      하지만 현실적으로 이러한 방법이 불가능한 경우가 많다.<br>
    - 보유 및 대기(Hold & Wait): 이 조건을 없애려면 자원을 가지고 있는 상태에서 다른 자원을 기다리지 않도록 만든다.<br>
      만약 여러 개의 자원이 필요하다면 필요한 모든 자원을 얻을 수 있는 경우에만 해당 자원을 요청한다.<br>
      또는 필요한 자원 중 일부만 가지는 경우 할당받은 자원을 모두 운영체제에 반납한다.<br>
      하지만 이와 같은 방법은 자원의 활용률을 저하시키고, starvation 현상이 발생하는 단점이 있다.<br>
    - 비선점(No preemption): 비선점을 없애러면 반대로 선점이 가능하도록 만들어야 한다.<br>
      이 역시 대부분의 자원에게는 불가능한 방법이다. CPU는 강제로 스위칭하는 것이 가능한 경우가 있지만, 대부분의 경우에는 불가능하다.<br>
      가령 프린터를 수행하는 중간에 다른 프로세스가 이를 선점하는 것은 불가능하다고 볼 수 있다.<br>
    - 환형대기(Circular wait): 이 조건을 없애는 것은 위 세 가지 조건보다는 할 수 있는 확률이 높다.<br>
      대표적인 예는 모든 자원에 번호를 부여하여 이 번호에 대한 오름차순으로 자원을 요청하는 것이다. 이 역시 자원의 활용률을 저하시키는 단점이 있다.<br><br>

- 네 가지 방법을 살펴본 결과 가장 현실적인 방법은 hold & wait나 circular wait 조건을 없애는 것이다. <br>
- 하지만 둘 다 자원을 비효율적으로 사용하게 되는 단점을 가지고 있다. <br>
- 그래서 이와 같이 교착상태를 사전에 방지하는 것은 군사, 우주, 의료와 같은 크리티컬한 곳에서 사용하는 것이 좋다.<br>
<br><br>

2. 교착상태 회피 (Deadlock Avoidance)<br>
교착상태 회피와 방지의 차이점은 교착상태를 다르게 접근하는 것이다. <br>
교착상태 회피에서는 교착상태를 자원 요청에 대한 잘못된 승인으로 판단한다.<br>
교착상태 회피 대표 기법은 은행원 알고리즘이 있다.<br>
은행원 알고리즘에서 운영체제는 안전상태를 유지할 수 있는 요구만을 수락하고 불안전 상태를 초래할 사용자의 요구는 나중에 만족될 수 있을 때까지 거절한다.<br>

- 안정 상태 : 시스템이 교착상태를 이루지 않으면서 각 프로세스가 요구한 최대 요구량만큼 필요한 자원을 할당해 줄 수 있는 상태로 안전순서열이 존재하는 상태를 말한다.<br>
- 불안정한 상태 : 안전 순서열이 존재하지 않는 상태를 말한다. 교착상태는 불안전상태에서만 발생한다. 불안정상태라고 무조건 교착상태가 발생하는 것은 아니다.<br>

안전 순서열이란 자원을 순서대로 주고 받을 수 있는 순서를 말한다.<br>
- (보충) 은행원 알고리즘의 단점<br>
    - 할당할 수 있는 자원의 수가 일정해야 한다.<br>
    - 사용자 수가 일정해야 한다.<br>
    - 항상 불안정 상태를 방지해야 하므로 자원 이용도가 낮다.<br>
    - 최대 자원 요구량을 미리 알아야 한다.<br>
    - 프로세스들은 유한한 시간 안에 자원을 반납해야 한다. <br><br>
즉 은행원 알고리즘은 매우 복잡하다. <br>
또한 해당 프로세스가 시작할 때 프로세스가 가지고 있어야 할 자원의 최대 개수를 미리 알아야 하기 때문에 실제 돌아가는 프로그램에 적용하기도 상당히 어렵다. <br>
그래서 현재 채택하고 있는 방식이 아니다.<br>

<br>
</div>
</details>



<details>
<summary> Context Switching에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
  
멀티프로세스 환경에서 CPU가 어떤 하나의 프로세스를 실행하고 있는 상태에서<br>
인터럽트 요청에 의해 다음 우선 순위의 프로세스가 실행되어야 할 때 <br>
기존의 프로세스의 상태 또는 레지스터 값(Context)을 저장하고 <br>
CPU가 다음 프로세스를 수행하도록 새로운 프로세스의 상태 또는 레지스터 값(Context)를 교체하는 작업을 <br>
Context Switch(Context Switching)라고 한다.<br>

<br>
</div>
</details>



<details>
<summary> 커널에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

![image](https://user-images.githubusercontent.com/67456294/217103264-6b356f12-6f31-4de3-9639-45d3d5471505.png)

  
- 커널은 운영체제 중 항상 메모리에 올라가 있는 운영체제의 핵심 부분으로써 <br>
하드웨어와 응용 프로그램 사이에서 인터페이스를 제공하는 역할을 하며 컴퓨터 자원들을 관리하는 역할을 한다. <br>

-  커널은 인터페이스로써 응용 프로그램 수행에 필요한 여러가지 서비스를 제공하고, <br>
  여러가지 하드웨어(CPU, 메모리) 등의 리소스를 관리하는 역할을 한다. <br>
  
- 다만 이러한 커널은 항상 컴퓨터 자원들을 바라만 보고 있기에 사용자와의 상호작용은 지원하지 않는다. <br>
따라서 사용자와의 직접전인 상호작용을 위해 프로그램을 제공하게 되는데, 대표적으로 쉘(Shell)이라는 명령어 해석기등이 있다. <br>

<br>
</div>
</details>



<details>
<summary> 운영체제 메모리에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

![image](https://user-images.githubusercontent.com/67456294/217951566-01bfe95b-db53-4b62-865f-53f0a5373546.png)

프로그램이 실행되기 위해 프로그램이 메모리에 로드가 되어야한다. <br>
따라서 운영체제에서 프로그램의 실행을 위해 다향한 메모리 공간을 제공한다. <br>
코드, 데이터, 스택, 힙 영역이 할당되고 각 역할은 다음과 같다. <br><br>

- 코드 :  실행할 프로그램의 코드가 저장되는 텍스트 영역이다. <br>
CPU는 코드영역에서 저장된 명령어를 하나씩 가져가서 처리한다. <br>

- 데이터 :  전역변수와 정적변수가 이해 해당된다. <br>
프로그램의 시작과 함께 할당되며 프로그램이 종료되면 소멸된다. <br>

- 스택 :  스택영역은 함수의 호출과 관계되는 지역변수와 매개변수가 저장되는 영역이다. <br>
함수의 호출과 함께 할당되며, 함수의 호출이 종료될때 해제된다. <br>

- 힙  :  힙 영역은 사용자가 직접 관리할 수 있는 메모리 영역이다. <br>
힙 영역은 사용자에 의해 메모리공간이 동적으로 할당되고 해제된다. <br>

<br>
</div>
</details>



<details>
<summary> CPU 스케줄링의 종류 중 '비선점 스케쥴링'에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 비선점(Non-preemptive) 스케줄링 <br>

  - 이미 할당된 CPU를 다른 프로세스가 강제로 빼앗아 사용할 수 없는 스케줄링 기법이다. <br>

  - 프로세스가 CPU를 할당받으면 해당 프로세스가 완료될 때까지 CPU를 사용한다. <br>

  - 일괄 처리 방식의 스케줄링(공정하지만 긴급 응답을 요하는 작업에 좋지 않다.)  <br> <br>
  
 (1)  FCFS(FIFO) : 
  - 준비상태 큐에 도착한 순서에 따라 CPU를 할당하는 기법. <br>
  - 공평성은 유지되지만 짧은 작업이 긴 작업을, 중요한 작업이 중요하지 않은 작업을 기다리게 됨.  <br>
    - 장점 : 평균 응답시간이 길다. (대화식 시스템에 부적합) <br>
    - 단점 : 도착 순서에 따라 공평하다. <br> <br>

(2) SJF(Shortest Job First) : 
  - 실행시간이 가장 짧은 프로세스에 먼저 CPU를 할당하는 기법. 
  - 가장 적은 평균 대기 시간을 제공하는 최적 알고리즘.  <br>
    - 장점 : 평균 응답 시간을 최소화 할 수 있다. <br>
    - 단점 : 실행시간이 긴 프로세스는 CPU를 할당받지 못하고 무한히 대기하는 현상 발생(starvation)  <br><br>
  
 (3) HRN(Highest Response ratio) : 
 - 실행 시간이 긴 프로세스에 불리한 SJF 기법을 보완하기 위한 것으로 <br>
 - 우선순위 계산 결과 값이 높은 것부터 우선순위가 부여된다. <br><br>

(4) 기한부(DeadLine) : <br>
- 프로세스에게 일정한 시간을 주어 그 시간 안에 프로세스를 완료하도록 하는 기법<br>

(5) 우선순위(Priority) : <br>
- 준비상태 큐에서 기다리는 각 프로세스마다 우선순위를 부여하여 그 중 가장 높은 프로세스에게 먼저 CPU를 할당하는 기법. <br>

<br>
</div>
</details>



<details>
<summary> CPU 스케줄링의 종류 중 '선점 스케쥴링'에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 하나의 프로세스가 CPU를 할당받아 실행 하고 있을 때 우선순위가 높은 프로세스가 CPU를 강제로 빼앗아 사용할 수 있는 스케줄링 기법 <br>
- 선점으로 인한 많은 오버헤드가 발생한다.<br>
- 시분할 시스템에 사용하는 스케줄링이다. (긴급을 요하는 우선순위를 갖는 시분할 처리, 실시간 처리에 유용) <br>
- 선점을 위해 시간 배당을 위한 인터럽트용 타이머 클럭(Clock)이 필요하다. <br><br><br>

(1) SRT(Shortest Remaining Time) : <br>
- 현재 실행 중인 프로세스의 남은 시간과 대기 큐에 프로세스의 실행시간이 가장 짧은 프로세스에게 CPU를 할당하는 기법 <br>
    - 비선점 기법인 SJF 알고리즘의 선점 형태로 변경한 기법  <br>
    - 단점 : 잦은 선점으로 인한 문맥교환의 부담 <br><br>
    
(2) 선점 우선순위 : <br>
- 준비상태 큐의 프로세스들 중에서 우선순위가 가장 높은 프로세스에게 먼저 CPU를 할당하는 기법 <br><br>

(3) RR(Round Robin) : <br>
- 시분할 시스템을 위해 고안된 방법으로, FCFS 알고리즘을 선점 형태로 변형한 기법. <br>
- 대기 큐를 사용하여 먼저 대기한 작업이 먼저 CPU를 사용한다. <br>
- 단점 <br>
  - CPU를 사용할 수 있는 시간(Quantum)동안 CPU를 사용한 후에 다시 대기 큐의 가장되로 배치된다. <br>
  - 할당되는 시간이 클 경우 FCFS 기법과 같아지고, 시간이 작을 경우 문맥교환 및 오버헤드가 자주 발생된다. <br><br>

(4) MLQ(다단계 큐) : <br>
- 프로세스를 특정 그룹으로 분류할 수 있는 경우 그룹에 따라 각기 다른 준비상태 큐를 사용한다. <br>
- 작업들을 여러 종류의 그룹으로 분할한다. <br>
- 큐들간에 프로세스 이동이 불가능하고, 각 큐는 자신만의 독자적인 스케줄링을 가진다. <br>
- 상위 우선 순위의 큐가 Empty 이면 하위 우선순위의 큐의 프로세스가 수행된다. <br>

(5) MLFQ(다단계 피드백 큐) : <br>
- 특정 그룹의 준비상태 큐에 들어간 프로세스가 다른 준비상태 큐로 이동할 수 없는 다단계 큐 기법을 준비상태 큐 사이를 이동할 수 있도록 개선한 기법이다. <br>
- 우선순위가 높은 단계의 큐일수록 시간 할당량을 작게 설정한다.  <br>
- 현대 OS에서 RR방식과 함께 가장 많이 사용되는 스케줄링 기법이다. <br>

<br>
</div>
</details>


<details>
<summary> 메모리 단편화에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 메모리 단편화란? <br>
  - 메모리의 빈 공간 또는 자료가 여러 개의 조각으로 나뉘는 현상을 말한다. <br>
  - 할당한 메모리를 해제를 하게 되면 그 메모리 공간이 빈 공간(사용하지 않는 공간)이 되고 그 빈공간의 크기보다 큰 메모리는 사용할 수 없다. <br>
  - 그리하여 이 공간들이 하나 둘 쌓이게 되면 수치상으로는 많은 메모리 공간이 남았음에도 불구하고, 실제로 사용할 수 없는 메모리가 발생한다. <br><br>

- 메모리 단편화 해결방법은? <br>
  - 메모리 압축(디스크 조각 모음), 메모리 통합(단편화가 발생된 공간들을 하나로 통합시켜 큰 공간으로 만드는 기법) <br><br>

- 내부단편화와 내부단편화란? <br>
  - 내부단편화<br>
    - 분할된 영역이 할당된 프로그램의 크기보다 커서 사용되지 않고 남아 있는 빈 공간을 말한다.<br>
   

<br>
</div>
</details>

--------------------------------------------------------------------------------------------------------
  
## [ JPA ]  

<details>
<summary> 영속성 컨텍스트 및 속성에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

영속성 컨텍스트는 엔티티를 영구 저장하는 환경입니다.<br>
엔티티 매니저를 생성하면 자동으로 영속성 컨텍스트가 생성되고 엔티티를 관리 혹은 보관할 수 있습니다.<br>

영속성 컨텍스트의 속성<br>

- 비영속 : 영속성 컨텍스트와 전혀 무관한 상태로 순수한 객체의 상태 (처음 객체가 생성되면 비영속 상태)<br>
- 영속 : 영속성 컨텍스트에 저장된 상태<br>
- 준영속 : 영속성 컨텍스트에서 관리하다, 영속성 컨텍스에서 분리된 상태, 준영속 상태는 영속 상태 였던 적이 있기 때문에 @Id 값을 반드시 가지고 있습니다.<br>
- 삭제 : 삭제된 상태<br>

</div>
</details>
  
  

<details>
<summary>영속성 컨텍스트의 특징에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

1. 1차 캐시<br>
   - 영속성 컨택스트 내부에는 1차 캐시라고 불리는 캐시를 가지고 있습니다. <br>
   - 영속상태의 엔티티는 모두 1차 캐시에 저장되고, 1차 캐시는 @Id를 키로 가지고 있는 Map이 존재합니다. <br>
   - 엔티티를 조회할 때 바로 DB에 접근하는 것이 아니고 1차 캐시에 있는 데이터를 먼저 조회한 후 없는 경우에만 DB에 접근하여 조회 후 다시 1차 캐시에 저장 합니다.<br>
   - 즉, 먼저 DB에 접근하는 것이 아닌 1차 캐시에 먼저 접근함으로서 데이터의 결과를 빠르게 가져올 수 있습니다.<br>

2. 동일성 보장<br>
   - 1번 특징과 연관되며 모든 엔티티의 데이터들은 1차 캐시에 저장되어지기 때문에<br>
   - 식별자가 동일한 엔티티의 경우 동일성이 보장됩니다. 여기서 동일성이란 같은 객체를 참조한다는 의미입니다.<br>

3. 트랜잭션을 지연하는 쓰기지연<br>
   - 트랜잭션은 DB에서 하나의 작업 단위를 나타냅니다. <br>
   - 영속성 컨텍스트에서 DML이 발생했을 때 바로 DB에 저장하지 않고, 트랜잭션이 커밋될 때 영속성 컨텍스트의 쓰기지연 SQL 저장소에 모아둔 쿼리들을 한 번에 저장합니다. <br>
   - 이때 쿼리들은 영속성 컨텍스트에 따로 저장이 되며 커밋을 실행하게 되면 flush를 통해 쿼리들을 DB에 저장하게 되고 최종적으로 commit을 하여 DB에 쿼리를 반영합니다.<br>
   - 즉, DB에 접근하는 횟수가 줄어들기 때문에 성능면에서 뛰어납니다.<br>

4. 변경 감지<br>
   - 영속성 컨텍스트의 1차 캐시에는 스냅샷을 통해 엔티티의 변경을 감지합니다. 변경감지는 오직 영속 상태의 엔티티에만 적용이 됩니다. <br>
 순서는 아래와 같습니다.<br>

      (1) 트랜잭션을 커밋하면, flush가 호출되고, 엔티티와 스냅샷을 비교해서 변경된 엔티티를 찾습니다.<br>

      (2) 변경된 엔티티가 존재하면, 쿼리를 생성해서 쓰기지연 SQL 저장소에 저장합니다.<br>

      (3) 쓰기지연SQL 저장소에 생성된 쿼리들을 데이터베이스에 flush하고 commit 합니다.<br>
  
</div>
</details>



<details>
<summary> 즉시 로딩과 지연 로딩의 차이에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>

- 즉시로딩 : 엔티티를 조회할 때, 연관된 엔티티도 함께 조회한다.<br>
(Question을 조회할 때, List 도 조회)<br>


- 지연로딩 : 연관된 엔티티를 실제 사용할 때 조회한다.<br>
(Quesion을 조회할 때, List도 사용한다면 그 때만 조회)<br>

</div>
</details>


  
  
--------------------------------------------------------------------------------------------------------
  
## [ ETC ]  

<details>
<summary> 웹 브라우저에 URL을 입력하면 어떤 일이 일어나는지 설명해주세요. </summary>
<div markdown="1">  
<br>

<br><br>

1. 브라우저 주소창에 maps.google.com을 입력한다. <br>
2. 브라우저가 maps.google.com의 IP 주소를 찾기 위해 캐시에서 DNS 기록을 확인한다.<br>
3. 만약 요청한 URL(maps.google.com)이 캐시에 없다면, ISP의 DNS 서버가 DNS 쿼리로 maps.google.com을 호스팅하는 서버의 IP 주소를 찾는다.<br>
4. 브라우저가 해당 서버와 TCP 연결을 시작한다.<br>
5. 브라우저가 웹서버에 HTTP 요청을 보낸다.<br>
6. 서버가 요청을 처리하고 응답을 보낸다.<br>
7. 서버가 HTTP 응답을 보낸다.<br>
8. 브라우저가 HTML 컨텐츠를 보여준다. <br>

<br><br>

</div>
</details>
