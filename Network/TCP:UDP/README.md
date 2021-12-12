# TCP / UDP

# Transport Layer

: End-Point간 신뢰성있는 데이터 전송을 담당하는 계층

## 신뢰성

⇒ 데이터를 **순차적**, 안정적인 전달.

## 전송

⇒ **포트 번호에 해당하는 프로세스**에 데이터를 전달.

## 전송 계층이 없다면?

- 데이터의 **순차 전송** 원활히 X

![TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled.png](TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled.png)

- **Flow (흐름 문제)**
⇒ 원인 : 송수신자 간의 데이터 처리 속도 차이
수신자가 처리할 수 있는 데이터량 초과.
- **Congestion (혼잡 문제)**
⇒ 원인 : 네트워크의 데이터 처리 속도(ex.라우터) 
Network가 혼잡.

결과 : 데이터의 손실 발생.

```java
Hello
Nice to meet you
```

해결 : TCP

```java
Hell
     to      you
```

# TCP

## 특징

- **신뢰성**있는 데이터 통신을 가능하게 해주는 프로토콜
- 특징 : Connection 연결 (**3 way-handshake**) - 양방향 통신
          연결 해제시 (**4 way-handshake**)
- 데이터의 **순차 전송**을 보장
- **Flow Control (흐름 제어)**
- **Congestion Control (혼잡 제어)**
- **Error Detection (오류 감지)**

## 세그먼트(Segment)

 : TCP 프로토콜의 PDU (Protocol Distribution Unit)

![TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%201.png](TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%201.png)

- ACK : 응답에 관한 Flag
- SYN : 연결을 위한 Flag
- FIN : 연결 해제를 위한 Flag

## 3-way handshake

![TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%202.png](TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%202.png)

1. SYN 비트를 1로 설정해 패킷 송신
2. SYN, ACK  비트를 1로 설정해 패킷 송신
3. ACK 비트를 1로 설정해 패킷 송신

## 전송

![TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%203.png](TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%203.png)

1. Client가 패킷 송신
2. Server에서 ACK 송신
3. ACK를 수신하지 못하면 재전송

## 4 way handshake

![TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%204.png](TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%204.png)

1. 데이터를 전부 송신한 client가 FIN 송신
2. Server가 ACK 송신
3. Server에서 남은 패킷 송시 (일정 시간 대기)
4. Server가 FIN 송신
5. Client가 ACK 송신

## 문제점

- 느리다!
매번 connection  필요.
손실이 있으면 재전송.

# UDP

## 특징

- 신뢰성은 떨어지지만, 전송속도가 빠른 프로토콜
- 순차 X, 흐름 X, 혼잡 X
- Connectionless
- Error Detection
- 비교적 데이터의 신뢰성이 중요하지 않을 때 사용 (ex. 영상 스트리밍)
TCP는 조금만 손실이 있어도 재전송 하기 때문.

## User Datagram

: UDP 프로토콜의 PDU

![TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%205.png](TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%205.png)

16bit checksum으로 Error Detection

## 전송

![TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%206.png](TCP%20UDP%2058fcebc634474d39b3bce4f69e47e175/Untitled%206.png)

일방적임.