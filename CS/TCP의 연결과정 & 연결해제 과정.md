### Tcp의 연결과정 연결해제과정
TCP는 네트워크 계층 중 전송 계층에서 사용하는 프로토콜 로서, 장치들 사이에 논리적인 접속을 성립(Establish) 하기 위하여 연결을 설정하여 신뢰성을 보장하는 연결형 서비스이다.
#### TCP 3-way HandkShake란?
TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 연결을 설정(Connection Establish)하는 과정이다.

#### TCP 3-way HandkShake 역할 및 과정
 3-way HandkShake
[STEP1]
Client는 Server에 접속을 요청하는 SYN 패킷을 보낸다. 이때 Client는 SYN을 보내고 SYN/ACK 응답을 기다리는 SYN_SENT 상태가 된다.
[STEP2]
Server는 Client의 SYN 요청을 받고 Client에게 요청을 수락한다는 ACK와 SYN 가 설정된 패킷을 발송하고 A가 다시 ACK로 응답
[STEP3]
Client가 Server에게 SYN+ACK를 받게되면 Server에게 응답을 확인했다는 ACK을 보낸다.
그 이후부터는 연결이 이루어지게되고 데이터가 오가게 된다.
위의 3단계를 거쳐 통신하는 것이 신뢰성 있는 연결을 맺어준다는 TCP의 3-Way HandShake방식이다. 
#### TCP 4-way HandkShake란?
TCP 통신 연결을 해제(Connection Termination)하는 과정이다.<br>
[STEP 1]<br>
App으로부터 close 신호를 받은 Client가 Server에게 연결을 종료하겠다는 FIN 플래그를 전송하게된다.<br>
[STEP 2]<br>
Server는 FIN 플래그를 받고 응답을 받았다는 의미로 ACK를 보낸다.<br>
그리고 Server는 자신이 하던 데이터 통신이 끝날 때 까지 기다린다.(이 상태가 Time_Wait 상태)<br>
[STEP 3]<br>
Server가 통신이 끝났으면 연결이 종료되었다고 해당 Client한테 FIN 플래그를 전송한다.<br>
[STEP 4]<br>
Client는 응답을 받았다는 의미로 ACK를 보낸다.<br>
이 때 Client는 패킷 유실이나 Routing 지연으로 인해 FIN패킷보다 늦게 도착하는 상황을 방지하기 위해 FIN 플래그를 받게되어도 일정시간동안 세션을 남겨두고 잉여 패킷을 기다린다.<br>
