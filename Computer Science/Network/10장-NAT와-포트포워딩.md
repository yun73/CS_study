### [NAT란?](https://youtu.be/Qle5cfCcuEY?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- **Network Address Translation**
- **특정 IP주소에 특정 포트번호로 가는 패킷을 다른 IP주소에 다른 포트번호로 바꿔주는 것**
- IP패킷의 TCP/UDP 포트 숫자와 소스 및 목적지의 IP 주소등을 재기록하면서 라우터를 통해 네트워크 트랙픽을 주고 받는 기술
- 패킷에 변화가 생기기 때문에 IP나 TCP/UDP의 체크섬(checksum)도 다시 계산되어 재기록해야 한다.
- NAT를 이용하는 이유는 대개 사설 네트워크에 속한 여러 개의 호스트가 하나의 공인 IP 주소를 사용하여 인터넷에 접속하기 위함이다.
- 하지만 꼭 사설 IP를 공인 IP로 변환 하는 데에만 사용하는 기술은 아니다.
![Alt text](<../../resources/Computer Science/Network/NAT/nat.png>)

### 포트 포워딩

- 포트 포워딩 또는 포트 매핑(port mapping)은 패킷이 라우터나 방화벽과 같은 네트워크 장비를 가로지르는 동안 <span style="color:red">특정 IP 주소와 포트 번호의 통신 요청을 특정 다른 IP와 포트 번호로 넘겨주는</span> 네트워크 주소 변환(NAT)의 응용이다.
- 이 기법은 게이트웨이(외부망)의 반대쪽에 위치한 사설네트워크에 상주하는 호스트에 대한 서비스를 생성하기 위해 흔히 사용된다.
- 일반적으로 **서버가 사설 네트워크 대역에 있을 때, 그 네트워크 대역을 설정하는 3계층 장비(라우터, 공유기 등)에서 제공해주는 기능**
- 사설 IP 대역에서(위 사진 빨간색 위치) 보이지않는 네트워크(위 사진 초록색 위치)대역 컴퓨터로 직접 통신을 하고싶다. (먼저 들어가고싶다.)
- 포트포워딩은 직접 컴퓨터의 IP를 치는게 아니라, 공인 IP 2(아래 사진)로 보낸다. 공인 IP 2 공유기에 포트포워딩 설정을 해놓아야한다.
	
    - 공인 IP 1에서 공인 IP 2의 특정 포트로 전송 - IPv4 목적지 Ip주소가 공인 IP 2
    - 이렇게 보냈을 때, 공인 IP 2 공유기가 특정 포트로 들어온 요청을 내부 네트워크 대역 중에서 특정 ip에 특정 포트로 보내는 것
    - 공인 IP 2 공유기 입장에서는 웹서버가 보임(직접 연결되어 있으니, 사진3) 공유기가 대신 전달해 줌
![Alt text](<../../resources/Computer Science/Network/NAT/port.png>)
![Alt text](<../../resources/Computer Science/Network/NAT/port2.png>)

### [포트 포워딩 설정 실습](https://youtu.be/EvYI14QdM6A?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

