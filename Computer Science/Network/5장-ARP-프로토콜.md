# 05 통신하기 전 반드시 필요한 ARP 프로토콜

## ARP 프로토콜

### ARP가 하는일

- ARP 프로토콜은 같은 네트워크 대역에서 통신을 하기 위해 MAC주소를 IP 주소를 이용해서 알아오는 프로토콜
- 같은 네트워크 대역에서 통신을 한다고 하더라도 데이터를 보내기 위해서는 7계층 부터 캡슐화를 통해 데이터를 보내기 때문에 IP주소와 MAC주소가 모두 필요하다
- 이 때 IP주소는 알고 MAC주소는 모르더라도 ARP를 통해 통신이 가능하다

### ARP 프로토콜의 구조

- IP 주소를 이용해 MAC주소를 알아온다

![Alt text](<../../resources/Computer Science/Network/ARP프로토콜/01.png>)

Source Hardware Address ⇒ 출발지 MAC 주소

Source Protocol Address ⇒ 출발지 IP 주소

Destination Hardware Address ⇒ 목적지 MAC 주소

Destination Protocol Address ⇒ 목적지 IP 주소

Hardware type ⇒ 0001(이더넷을 뜻하는 값)

Protocol type ⇒ protocol Adress의 타입(0800) ip4를 뜻하는 값

Hardware Address Length ⇒ 길이 06 (6비트)

Protocol Adrress Length ⇒ 길이 04 (4비트)

Opcode ⇒ 요청하고 있는지(1) 응답하고 있는지(2) 구별

- **이더넷 프로토콜(2계층)만 목적지가 먼저 온다.**

## ARP 프로토콜의 통신 과정

### IP 주소로 MAC 주소를 알아오는 과정

- IP주소만 알고 있을 때 ARP로 MAC 주소를 알아오기

![Alt text](<../../resources/Computer Science/Network/ARP프로토콜/02.png>)


- 일단 MAC 주소는 빈칸으로 두고

![Alt text](<../../resources/Computer Science/Network/ARP프로토콜/03.png>)

- 이더넷에서도 F로 꽉 채움

![Alt text](<../../resources/Computer Science/Network/ARP프로토콜/04.png>)

- 가운데 스위치 에다가 일단 보냄
- 스위치는 2계층 장비라서 2계층만 디캡슐화 함

![Alt text](<../../resources/Computer Science/Network/ARP프로토콜/05.png>)


- 모두 보내서 3계층을 확인함

![Alt text](<../../resources/Computer Science/Network/ARP프로토콜/06.png>)


- 목적지 IP 주소랑 같은거만 두고 나머지는 버림

![Alt text](<../../resources/Computer Science/Network/ARP프로토콜/07.png>)


- 같은애가 응답 주소에 MAC주소를 넘겨줌

![Alt text](<../../resources/Computer Science/Network/ARP프로토콜/08.png>)


- ARP 캐시테이블에 30이라는 애의 MAC 주소를 저장

## ARP 테이블

### 나와 통신했던 컴퓨터들

- 통신 했던 컴퓨터들의 주소는 ARP 테이블에 남는다. ⇒ 캐시 테이블

![Alt text](<../../resources/Computer Science/Network/ARP프로토콜/09.png>)