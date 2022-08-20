# Backend_interview_question  

## [ CS 관련 내용 ]  

<details>
<summary>TCP와 UDP의 차이점에 대해서 말해주세요. </summary>
<div markdown="1">  
<br>
  
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


