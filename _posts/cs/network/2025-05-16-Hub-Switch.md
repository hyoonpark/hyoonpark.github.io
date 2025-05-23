---
layout: post
title: "[Network] 허브와 스위치"
date: 2025-05-16 14:22 +09:00
categories: cs network
tags: [github, tech, blog, network, hub, switch, 스위치, 허브, 이더넷]
---

> **3줄 요약**
<br>허브는 물리 계층 장비로 단순히 수신된 데이터를 **모든 포트에 전송**함
<br>스위치는 데이터 링크 계층 장비로 MAC 주소 기반으로 **포트 지정 전송** 가능
<br>스위치는 충돌 방지와 VLAN 등 고급 기능을 제공하며 효율적인 통신을 가능하게 함
{: .prompt-tip }

# 💻 컴퓨터 네트워크 시리즈

> 이 시리즈는 『혼자 공부하는 네트워크』 (강민철 저)
> <br> + 인프런 강의를 기반으로 **개인적으로 복습 및 정리한 기록**입니다.

---

## 📌 허브 (Hub)

![hub](assets/img/cs/hub.png)
<sub>출처: [Chapter 02 물리계층 (2)](https://amy-ming.tistory.com/158)</sub>

### 📎 정의

- **물리 계층**의 대표적인 장비 (Layer 1)
- 여러 대의 호스트를 연결하는 장치 (리피터 허브, 이더넷 허브 등)

### 📎 특징

1. **모든 포트로 정보 전송**
   - MAC 주소 개념 없음 → 받은 정보는 판단 없이 전 포트로 전송  
   → 데이터 링크 계층에서 패킷의 MAC 주소를 확인하고 관련이 없다면 폐기
   - 불필요한 트래픽 증가

2. **반이중 통신 (Half-Duplex)**
   - 송수신을 번갈아 수행 (무전기처럼)
    - 1차선 도로처럼 송수신 중 하나만 가능
   - cf) 전이중 통신(Full-Duplex: 전화기처럼)과 대비됨

### 🔃 충돌(Collision)

- 허브에 연결된 호스트가 동시에 송신 → 충돌 발생
- **콜리전 도메인**: 충돌이 발생할 수 있는 영역
- 콜리전 도메인이 크면 충돌 확률 증가 → 성능 저하

### 🔧 해결책

- **CSMA/CD**: 충돌 감지 후 재전송을 위한 이더넷 프로토콜
- **스위치 등 상위 계층 장비 사용** → 충돌 방지

### 💡 참고: 리피터(Repeater)

![repeater](assets/img/cs/repeater.png)
<sub>출처: [Chapter 02 물리계층 (2)](https://amy-ming.tistory.com/158)</sub>

- 허브와 유사한 물리 계층 장비
- **신호 증폭**을 통해 거리 확장 가능

---

## 📌 스위치 (Switch)

<div style="text-align: center;">
  <img src="assets/img/cs/switch.png" alt="switch"/>
  <br/>
  <sub>
    출처: 
    <a href="https://amy-ming.tistory.com/158" target="_blank" rel="noopener">
      Chapter 03 데이터 링크 계층의 역할과 기능 (2)
    </a>
  </sub>
</div>

### 📎 정의

- **데이터 링크 계층** 장비 (Layer 2) → L2 스위치
- **MAC 주소 기반**으로 프레임을 **목적지 포트에만 전송**
- 전이중 통신 지원 → 충돌 방지

### 📎 주요 기능

1. **MAC 주소 학습 (Learning)**
   - 프레임 내 송신 MAC 주소와 포트를 기억
   - 목적지 MAC 주소가 등록된 포트로만 전송 (필터링 & 포워딩)

2. **에이징 (Aging)**
   - 일정 시간 동안 활동 없는 MAC 주소는 테이블에서 삭제

3. **VLAN (Virtual LAN)**
   - 가상의 LAN을 구성하여 **트래픽 분리** 및 보안 강화
   - 브로드캐스트 도메인을 논리적으로 분할

### 🔍 MAC 주소 테이블

- **포트 ↔ MAC 주소** 간의 연관 정보를 저장
- **플러딩**: 목적지 주소 미확인 시 모든 포트로 전송
- 학습된 후에는 특정 포트로만 전달 → 효율 향상

### 🌐 VLAN 유형

- **포트 기반 VLAN**: 포트 번호로 VLAN 구분
- **MAC 기반 VLAN**: MAC 주소로 VLAN 구분

### 💡 참고: 브리지(Bridge)

- 스위치와 유사한 데이터 링크 계층 장비
- 네트워크 세그먼트 구분, 충돌 도메인 분리
- 최근에는 스위치가 주로 사용됨

---

## ✅ 마무리 정리

- **허브**: 단순 전기적 중계 장비, 반이중, 충돌 발생률 높음
- **스위치**: 지능형 장비, 전이중 통신, 충돌 도메인 분리, VLAN 등 고급 기능 탑재  

네트워크 환경에서는 허브보다 스위치가 훨씬 더 효율적이며 안정적인 구조를 제공

---

## 📚 참고 자료

- 『혼자 공부하는 네트워크』 - 강민철 저  
- [인프런 강의 - 혼자 공부하는 네트워크 기반 강의](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B3%B5%ED%95%99-%ED%98%BC%EC%9E%90%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC){: target="_blank"}

---

읽어주셔서 감사합니다 🙌  
내용이 도움이 되었거나, 틀린 부분이 있다면 댓글이나 GitHub Issue로 알려주세요 😊
