---
layout: post
title: "[Computer Architecture] RAM"
date: 2025-04-15 13:36 +09:00
categories: cs computerarchitecture
tags:
    [
        github,
        tech,
        blog,
        memory,
        ram,
        computer,
        architecture
    ]
---

> **3줄 요약**
<br>RAM은 데이터를 임시로 저장하는 휘발성 메모리
<br>DRAM은 주 메모리, SRAM은 캐시에 사용됨
<br>논리 주소와 물리 주소는 MMU에 의해 변환됨
{: .prompt-tip }

# 💻 컴퓨터 구조 & 운영체제 시리즈

> 이 시리즈는 『혼자 공부하는 컴퓨터 구조+운영체제』 (강민철 저)  
> <br> + 인프런 강의를 기반으로 **개인적으로 복습 및 정리한 기록**입니다.

---

## 💾 RAM

- 휘발성 저장 장치  
  - RAM은 전원이 꺼지면 데이터가 사라지는 **휘발성 메모리**로, CPU가 빠르게 접근할 수 있는 작업 공간 역할
- 우리가 흔히 말하는 메모리
  - ~~"이거 메모리 얼마짜리야?"~~
- 종류  
  - DRAM  
  - SRAM  
  - SDRAM  
  - DDR SDRAM

<div style="text-align: center;">
  <img src="assets/img/cs/ram-types.png" alt="DRAM vs SRAM" width="500"/>
  <br/>
  <sub>출처: 『혼자 공부하는 컴퓨터 구조+운영체제』 - 강민철 저</sub>
</div>

### 🔸 DRAM (Dynamic RAM)

- 저장된 데이터가 **동적으로 사라지는** RAM  
- 데이터 유지를 위해 주기적인 재충전(재활성) 필요  
- 주 메모리로 사용됨  
  - 소비 전력 낮음  
  - 저렴함  
  - 집적도 높아 대용량 설계 용이



### 🔸 SRAM (Static RAM)

- 저장된 데이터가 **사라지지 않는(정적인)** RAM  
- DRAM보다 빠름  
- **캐시 메모리**로 사용됨  
  - 소비 전력 높음  
  - 비쌈  
  - 집적도 낮음  
  - 소량, 고속이 필요한 영역에 사용

### 🔸 SDRAM (Synchronous DRAM, Single Data Rate SDRAM(SDR SDRAM))

- **클럭 신호에 동기화된** DRAM  
- 기존 DRAM보다 효율적  
- SDR(Single Data Rate) 방식



### 🔸 DDR SDRAM (Double Data Rate SDRAM)

- SDRAM의 발전된 형태  
- **한 번의 클럭 사이클에서 두 번 데이터 전송**  
  > 일반 SDRAM은 클럭의 상승(edge)에서만 데이터를 전송하지만,  
> DDR은 상승과 하강(edge) 모두에서 데이터를 전송하여 **2배의 속도**를 구현
- 대역폭을 넓혀 더 빠른 속도 제공  
  - 대역폭은 데이터를 주고 받는 길의 너비
- DDR2, DDR3, DDR4 등 세대별 발전

---

## 🧭 주소 공간 (Address Space)

![주소 공간 개념도](assets/img/cs/address-space.png)  
<sub>출처: 『혼자 공부하는 컴퓨터 구조+운영체제』 - 강민철 저</sub>



### 🔹 물리 주소 (Physical Address)

- 메모리 입장에서의 실제 주소  
- 정보가 저장된 **하드웨어 상의 위치**

### 🔹 논리 주소 (Logical Address)

- CPU와 프로그램 입장에서의 주소  
- 각 프로그램 입장에서 0번지부터 시작

### 🔸 주소 변환

- **MMU (메모리 관리 장치, Memory Management Unit)** 를 통해 논리 → 물리 주소로 변환  
- 계산: `물리 주소 = 베이스 레지스터 값 + 논리 주소`  
  🧮 예시)  
  논리 주소: `100`  
  베이스 레지스터: `15000`  
  → 물리 주소 = 15000 + 100 = `15100`

#### 🔸 레지스터 설명

- **베이스 레지스터**: 프로그램의 가장 작은 물리 주소(**프로그램의 첫 물리 주소**)  
- **논리 주소**: 프로그램 기준 시작점으로부터의 거리(프로그램의 **시작점으로부터 떨어진 거리**)

### 🔒 메모리 보호

- **한계 레지스터 (Limit Register)** 를 통해 다른 프로그램 침범 방지
- 베이스 레지스터가 실행 중인 프로그램의 가장 작은 물리 주소를 저장한다면,
- 한계 레지스터는 **논리 주소의 최대 크기를 저장**  
- 범위 조건  
  ```
  베이스 레지스터 값 ≤ 주소 < 베이스 레지스터 값 + 한계 레지스터 값
  ```

---

## ✅ 마무리 정리

RAM은 CPU가 데이터를 빠르게 읽고 쓸 수 있게 해주는 **핵심 기억 장치**  
DRAM은 주 메모리, SRAM은 캐시에 사용  
주소 공간과 MMU, 보호 메커니즘까지 이해하면 운영체제와의 연결성까지 보임

---

## 📚 참고 자료

- 『혼자 공부하는 컴퓨터 구조+운영체제』 - 강민철 저  
- [인프런 강의 - 혼자 공부하는 컴퓨터 구조+운영체제 기반 강의](https://www.inflearn.com/course/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C)  
{: target="_blank"}

---

읽어주셔서 감사합니다 🙌  
내용이 도움이 되었거나, 틀린 부분이 있다면 댓글이나 GitHub Issue로 알려주세요 😊
