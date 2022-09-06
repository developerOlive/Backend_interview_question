# Backend_interview_question  

## [ CS 관련 내용 ]  

<details>
<summary>TCP와 UDP의 차이점에 대해서 말해주세요. </summary>
<div markdown="1">  
<br>

![image](https://user-images.githubusercontent.com/67456294/185793406-cb3f0b74-5235-4e61-ae1a-9f1e084c8df2.png)

![image](https://user-images.githubusercontent.com/67456294/185793419-df382525-a5d8-4008-a9cb-2b6cf73e36b8.png)

  
TCP와 UDP는 둘 다 전송 계층에서 데이터를 보내기 위해 사용하는 프로토콜 입니다.  
TCP는 연결형 서비스로 가상 회선 방식을 제공하고, 높은 신뢰성을 보장하며 흐름 제어 및 혼잡 제어 기능을 제공합니다.  
UDP는 비연결형 서비스로 데이터그램 방식을 제공하고, 패킷에 순서 부여나 재조립등의 기능을 처리하지 않기 때문에 연속성이 중요한 서비스에 사용됩니다.  

</div>
</details>
  
  
  
<details>
<summary>TCP의 3-way Handshaking 역할과 과정을 말해주세요. </summary>
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
<summary> TCP의 4-way Handshaking의 역할과 과정에 대해서 말해주세요. </summary>
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
<summary> HTTP와 HTTPS의 차이점에 대해서 말해주세요. </summary>
<div markdown="1">  
<br>
  
HTTP는 따로 암호화 과정을 거치지 않기 때문에 중간에 외부에서 패킷을 가로채거나 수정할 수 있어 보안에 취약합니다. <br>
이를 보완하기 위해 나온 것이 HTTPS입니다. 중간에 암호화 계층을 거쳐서 패킷을 암호화합니다.
</div>
</details>


--------------------------------------------------------------------------------------------------------


## [ 데이터 베이스 관련 내용 ]  

<details>
<summary> RDBMS vs NOSQL에 대해서 말해주세요. </summary>
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
트랜잭션이란 데이터베이스의 상태를 변화시키는 하나의 논리적인 작업 단위라고 할 수 있으며, 트랜잭션에는 여러개의 연산이 수행될 수 있습니다. <br>
트랜잭션은 수행중에 한 작업이라도 실패하면 전부 실패하고, 모두 성공해야 성공이라고 할 수 있습니다.

</div>
</details>


<details>
<summary> ACID에 대해서 설명해주세요. </summary>
<div markdown="1">  
<br>
ACID는 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질입니다. <br><br> 
Atomicity(원자성): 트랜잭션의 연산은 모든 연산이 완벽히 수행되어야 하며, 한 연산이라도 실패하면 트랜잭션은 실패해야 합니다.<br>
Consistency(일관성): 트랜잭션은 유효한 상태로만 변경될 수 있습니다.<br>
Isolation(고립성): 트랜잭션은 동시에 실행될 경우 다른 트랜잭션에 의해 영향을 받지 않고 독립적으로 실행되어야 합니다.<br>
Durability(내구성): 트랜잭션이 커밋된 이후에는 시스템 오류가 발생하더라도 커밋된 상태로 유지되는 것을 보장해야 합니다. <br>

</div>
</details>


<details>
<summary> Redis에 대해서 간단히 설명해주세요. </summary>
<div markdown="1">  
<br>
Redis는 key-value store NOSQL DB입니다. <br>
싱글스레드로 동작하며 자료구조를 지원합니다. 그리고 다양한 용도로 사용될 수 있도록 다양한 기능을 지원합니다. <br>
데이터의 스냅샷 혹은 AOF 로그를 통해 복구가 가능해서 어느정도 영속성도 보장됩니다. <br>
</div>
</details>



--------------------------------------------------------------------------------------------------------

## [ 보안, 암호학 ] 


<details>
<summary> 단방향 암호화에 대해서 간단히 설명해주세요. </summary>
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

