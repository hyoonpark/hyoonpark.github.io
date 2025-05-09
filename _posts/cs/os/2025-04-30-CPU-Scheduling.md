---
layout: post
title: "[OS] CPU 스케줄링"
date: 2025-04-30 18:36 +09:00
categories: cs os
tags:
    [
        github,
        tech,
        blog,
        operating,
        system,
        os,
        scheduling,
        cpu
    ]
---

> **3줄 요약**
<br>운영체제는 여러 프로세스가 CPU를 효율적으로 사용할 수 있도록 스케줄링을 수행
<br>비선점형과 선점형 방식으로 나뉘며 다양한 알고리즘이 존재
<br>라운드 로빈, 우선순위, 다단계 피드백 큐 등 상황에 따라 선택적 적용 필요
{: .prompt-tip }

# 💻 컴퓨터 구조 & 운영체제 시리즈

> 이 시리즈는 『혼자 공부하는 컴퓨터 구조+운영체제』 (강민철 저)
> <br> + 인프런 강의를 기반으로 **개인적으로 복습 및 정리한 기록**입니다.

---

## 🎯 CPU 스케줄링이란?

운영체제가 프로세스들에게 공정하고 합리적으로 **CPU 자원을 배분하는 작업**  
프로세스들은 각자의 우선순위와 상태에 따라 준비큐나 대기큐에 존재하며 CPU 할당을 기다림

---

## 🧾 스케줄링 기본 개념

### 🔹 프로세스 우선순위
- 프로세스마다 우선순위 값 존재 (PCB에 저장)
- 입출력 집중 프로세스의 우선순위는 CPU 집중 프로세스보다 높게 설정

### 🔹 스케줄링 큐
- 큐(Queue)이지만 선입선출일 필요는 없음
- 준비 큐(Ready Queue) : CPU 할당을 기다리는 프로세스 집합  
- 대기 큐(Waiting Queue) : 입출력 장치를 기다리는 프로세스 집합  
  → 장치별로 개별 대기 큐 존재 (프린터, 디스크 등)

---

## 🔁 스케줄링 방식

### ✅ 비선점형 스케줄링 (Non-Preemptive)
- CPU를 할당받은 프로세스가 작업을 끝낼 때까지 CPU를 점유
- 문맥 교환 오버헤드 적음
- 자원 독점 가능성 존재

### ✅ 선점형 스케줄링 (Preemptive)
- 운영체제가 CPU를 강제로 회수하고 다른 프로세스에 할당
- 골고루 자원을 분배 가능
- 문맥 교환 시 오버헤드 발생 가능

---

## ⚙️ 주요 CPU 스케줄링 알고리즘

### 1. 선입 선처리 (FCFS, First Come First Served)
- **비선점형 스케줄링**
- 준비 큐에 들어온 순서대로 CPU 할당
- 단점: **호위 효과(convoy effect)** 발생  
  → 긴 작업 하나 때문에 짧은 작업들이 오래 대기

---

### 2. 최단 작업 우선 (SJF, Shortest Job First)
- **비선점형 방식**
- CPU 사용 시간이 가장 짧은 프로세스부터 처리
- 실행 시간이 예측 가능한 경우에 유리
- 호위 효과 방지 가능

---

### 3. 라운드 로빈 (Round Robin)
- **선점형 스케줄링**
- 프로세스마다 일정 시간(time slice)만큼 CPU 사용
- 시간이 끝나면 문맥 교환 후 다시 큐 끝에 삽입
- time slice 크기가 중요  
  → 너무 크면 FCFS와 유사, 너무 작으면 오버헤드 증가

---

### 4. 최소 잔여 시간 우선 (SRT, Shortest Remaining Time)
- **선점형 SJF**
- 최단 작업 우선 스케줄링 + 라운드 로빈 스케줄링
- 남은 작업 시간이 가장 적은 프로세스가 CPU 선점
- 응답 시간이 중요한 시스템에서 유리

---

### 5. 우선순위 스케줄링
- 프로세스에 우선순위를 부여하고 높은 순서대로 CPU 할당
- 선점형, 비선점형 모두 가능
- **기아현상(starvation)** 발생 가능  
  → 우선순위 낮은 프로세스는 계속 CPU를 못 받는 상황  
- 해결 방법: **에이징(aging)**  
  → 오래 대기한 프로세스의 우선순위를 점차 상승

---

### 6. 다단계 큐 스케줄링 (Multilevel Queue)
- 우선순위별로 여러 개의 준비 큐 구성
- 각 큐는 고정된 우선순위를 가짐
- 큐 간 이동 불가
- 큐마다 스케줄링 방식 독립 적용 가능  
  → 예: 상위 큐는 RR, 하위 큐는 FCFS

---

### 7. 다단계 피드백 큐 스케줄링 (Multilevel Feedback Queue)
- 다단계 큐에서 큐 간 **이동 가능**
- 오랫동안 대기한 프로세스의 우선순위를 자동 조정 (**에이징 적용**)
- 다양한 스케줄링 방식을 혼합 적용 가능
- **CPU 스케줄링의 가장 일반적인 형태**

---

## ✅ 마무리 정리

CPU 스케줄링은 시스템의 자원을 효율적으로 분배하고 사용자 응답성을 높이기 위한 핵심 메커니즘  
운영체제는 다양한 스케줄링 알고리즘을 통해 프로세스의 우선순위와 특성을 고려해 CPU를 배분함  
시스템의 성격에 따라 적절한 스케줄링 전략을 선택하는 것이 중요

---

## 📚 참고 자료

- 『혼자 공부하는 컴퓨터 구조+운영체제』 - 강민철 저  
- [인프런 강의 - 혼자 공부하는 컴퓨터 구조+운영체제 기반 강의](https://www.inflearn.com/course/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C)  
{: target="_blank"}

---

읽어주셔서 감사합니다 🙌  
내용이 도움이 되었거나, 틀린 부분이 있다면 댓글이나 GitHub Issue로 알려주세요 😊
