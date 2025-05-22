---
layout: post
title: "[Network] 전송 계층"
date: 2025-05-22 14:00 +09:00
categories: cs network
tags: [github, tech, blog, network, 전송계층, transport layer, TCP, UDP, port, 네트워크]
---

> **3줄 요약**
<br>전송 계층은 애플리케이션 프로세스를 식별하고, IP의 신뢰성 부족을 보완하는 역할
<br>TCP는 연결 기반의 신뢰성 있는 전송, UDP는 빠르지만 비연결성
<br>포트 번호를 통해 송수신 애플리케이션을 식별하고 통신함
{: .prompt-tip }

# 💻 컴퓨터 네트워크 시리즈

> 이 시리즈는 『혼자 공부하는 네트워크』 (강민철 저)
> <br> + 인프런 강의를 기반으로 **개인적으로 복습 및 정리한 기록**입니다.

---

## 📦 전송 계층이란?

전송 계층은 네트워크 계층과 응용 계층 사이에서 작동하며,  
IP의 한계를 보완하고 **애플리케이션 간 통신을 가능하게** 함

- 프로세스 간 통신 식별: **포트 번호(port)** 사용
- 대표 프로토콜: **TCP**, **UDP**

---

## 🚫 IP 프로토콜의 한계

### 신뢰할 수 없는 프로토콜 (Unreliable Protocol)

- 전송 성공 여부 확인 X
- 손실/손상된 패킷에 대한 재전송 X
- 수신 순서 보장 X

### 비연결형 프로토콜 (Connectionless Protocol)

- 송수신 간 **사전 연결 없이** 전송
- 빠르지만, 안정성은 떨어짐

→ 이 한계를 보완하는 것이 **전송 계층**의 역할

---

## 🎯 포트 번호 (Port Number)

포트 번호는 **애플리케이션을 식별**하는 주소  
하나의 호스트 내에서 여러 애플리케이션이 네트워크를 사용할 수 있게 해줌

### 포트 번호의 범위 및 분류

| 분류 | 범위 | 설명 |
|------|------|------|
| Well-known Port | 0 ~ 1023 | 시스템에서 예약된 범용 포트 (예: HTTP: 80, HTTPS: 443) |
| Registered Port | 1024 ~ 49151 | 일반 애플리케이션용 |
| Dynamic Port | 49152 ~ 65535 | 클라이언트 측에서 임시로 사용 |

<details>
<summary>
  <h3 style="display:inline; margin:0;">📝 추가 설명</h3>
</summary>
<div markdown="1">

#### 잘 알려진 포트(well-known port)
- 0번 부터 1023번까지
- 시스템 포트(system port)
- 범용적으로 사용되는 애플리케이션 프로토콜이 일반적으로 사용하는 포트 번호를 의미
<div>
  <img src="assets/img/cs/well-known.png" alt="잘 알려진 포트" width="50%">
  <sub>출처: 『혼자 공부하는 네트워크』 - 강민철 저</sub>
</div>

#### 등록된 포트(registered port)
1024번 부터 49151번까지
- 잘 알려진 포트에 비해 덜 범용적
- 흔히 사용되는 애플리케이션 프로토콜에 할당하기 위해 사용
- [Port Number Registry](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml){: target="_blank"}
<div>
  <img src="assets/img/cs/registered.png" alt="등록된 포트" width="50%">
  <sub>출처: 『혼자 공부하는 네트워크』 - 강민철 저</sub>
</div>

#### 동적 포트(dynamic port)
사설 포트(private port), 임시 포트(ephemeral port)
- 특별히 관리되지 않는 포트
- 서버는 대부분 잘 알려진 포트와 등록된 포트 사용
- 클라이언트는 대부분 동적 포트 사용

</div>
</details>

---

## 🔁 포트 포워딩 (Port Forwarding)

- 네트워크 내의 특정 호스트에 **IP + 포트 번호**로 접근 가능하도록 설정
- 외부에서 내부 장치에 접근할 때 유용 (e.g. 192.168.0.10:8080 → 내부 서버로 전달)

---

## 📡 TCP vs UDP

| 항목 | TCP | UDP |
|------|-----|-----|
| 연결 방식 | 연결형 | 비연결형 |
| 신뢰성 | 높음 | 낮음 |
| 순서 보장 | O | X |
| 재전송 | O | X |
| 속도 | 상대적으로 느림 | 빠름 |
| 사용 예시 | 웹, 이메일 | 실시간 스트리밍, VoIP |

---

## 📢 ICMP (Internet Control Message Protocol)

IP의 한계를 보완하는 **오류 보고 및 진단용 프로토콜**

- 전송 실패, 네트워크 문제 상황에 대한 **피드백 제공**
- 라우터 간 연결 문제, 수신 불가 상황 등 알림

### ICMP 메시지 형식

- 타입(Type): 메시지의 유형
- 코드(Code): 상세 정보

| 타입 | 설명 |
|------|------|
| 0 | Echo Reply (Ping 응답) |
| 3 | Destination Unreachable |
| 5 | Redirect |
| 8 | Echo Request (Ping 요청) |
| 11 | Time Exceeded (TTL 초과) |

<div style="text-align: center;">
  <img src="assets/img/cs/icmp_types.png" alt="ICMP 타입">
  <sub>출처: 『혼자 공부하는 네트워크』 - 강민철 저</sub>
</div>

---

## ✅ 마무리 정리

전송 계층은 **신뢰성과 프로세스 식별을 제공하는 핵심 계층**  
TCP/UDP의 특징과 포트 번호의 역할을 잘 이해하면,  
실제 네트워크에서의 데이터 전송 구조를 효율적으로 분석 가능

---

## 📚 참고 자료

- 『혼자 공부하는 네트워크』 - 강민철 저  
- [IANA 포트 번호 공식 문서](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml){: target="_blank"}  
- [인프런 강의 - 혼자 공부하는 네트워크 기반 강의](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B3%B5%ED%95%99-%ED%98%BC%EC%9E%90%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC){: target="_blank"}

---

읽어주셔서 감사합니다 🙌  
내용이 도움이 되었거나, 틀린 부분이 있다면 댓글이나 GitHub Issue로 알려주세요 😊
