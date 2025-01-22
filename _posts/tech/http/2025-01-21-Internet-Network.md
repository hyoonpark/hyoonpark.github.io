---
layout: post
title: "[HTTP]인터넷 네트워크 기초"
date: 2025-01-21 16:20 +09:00
categories: tech http
tags:
    [
        github,
        tech,
        blog,
        http,
        network
    ]
---

> **3줄 요약**
<br>**IP : 아파트**
<br>**PORT : 동, 호수**
<br>**DNS : 전화번호부**
{: .prompt-tip }

# 인터넷 네트워크

## 인터넷 통신

### 인터넷 프로토콜(IP)

#### 역할
- 지정한 IP 주소(IP Address)에 데이터 전달
- **패킷(Packet)**이라는 통신단위로 데이터 전달
  - IP 패킷 정보 : 출발 IP, 목적 IP
  - Package + Bucket

#### 한계
- **비연결성**
  - 패킷을 받을 대상이 없거나 서비스 불능(컴퓨터가 꺼져 있음)상태여도 패킷을 전송한다.
- **비신뢰성**
  - 패킷이 중간에 유실될 수 있다.
  - 여러개의 패킷을 보냈을때 순서를 보장할 수 없다.
    - 한 패킷의 최대 용량 약 1500byte
- **프로그램 구분**
  - 같은 IP를 사용하는 서버에서 여러 애플리케이션을 사용할 때 구분하지 못할 수 있다.
이러한 한계를 해결하기 위해 나타난 것이 TCP이다.

### TCP/UDP
**전송 제어 프로토콜(Transmission Control Protocol, TCP)**

#### 프로토콜 계층
- 인터넷 프로토콜 스택의 4계층
  - 애플리케이션 계층 - HTTP, FTP
  - 전송 계층 - TCP, UDP
  - 인터넷 계층 - IP
  - 네트워크 인터페이스 계층
1. 프로그램이 Hello, http! 메시지 생성
2. socket 라이브러리를 통해 전달
3. TCP 정보 생성, 메시지 데이터 포함
4. IP 패킷 생성, TCP 데이터 포함

#### 역할
- **TCP 세그먼트**로 전달
  - TCP 세그먼트 : 출발 PORT, 목적 PORT, 전송 제어, 순서, 검증 정보 등

#### 특징
- 연결지향
  - TCP 3 way handshake
  - SYN : 접속 요청, ACK : 요청 수락
    1. Client -> SYN -> Server
    2. Server -> SYN + ACK -> Client
    3. Client -> ACK -> Server (데이터 함께 전송 가능)
    4. 데이터 전송
- 데이터 전달 보증
  - Client -> 데이터 전송 -> Server
  - Server -> 데이터 잘 받았음 -> Client
- 순서 보장
- 신뢰할 수 있는 프로토콜

#### UDP
**사용자 데이터그램 프로토콜(User Datagram Protocol, UDP)**
특징
- 기능 거의 없음(하얀 도화지)
  - 하지만 사용하는 이유 : 단순하고 빠름
- IP와 거의 유사
- +PORT
  -> 애플리케이션 구분
- +체크섬

### PORT
같은 IP 내에서 프로세스를 구분 하는 것이다.
- 0 ~ 65535 할당 가능
- 0 ~ 1023
  - 잘 알려진 포트로 사용하지 않는 것을 권고한다.
  - HTTP : 80포트
  - HTTPS : 443포트

### DNS
**도메인 네임 시스템(Domain Name System)**

#### IP 문제
- 복잡해서 기억하기 어려움
- 변경될 수 있음
-> DNS 사용해 해결
도메인 명을 IP 주소로 변환해준다.
1. Client -> 도메인 명 -> DNS 서버
2. DNS 서버 -> IP -> Client
3. Client -> IP -> Server