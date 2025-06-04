---
layout: post
title: "[Network] HTTP 헤더의 구조와 주요 기능"
date: 2025-06-04 17:00 +09:00
categories: cs network
tags: [github, tech, blog, network, http, header, 네트워크]
---

> **3줄 요약**
<br>HTTP 헤더는 **요청과 응답에 부가정보**를 담아 통신 제어
<br>**Host, User-Agent, Authorization** 등 요청 헤더로 자원 접근 및 인증 수행
<br>**Server, Cookie, Cache 등 응답·공통 헤더**로 상태 관리·최적화 가능
{: .prompt-tip }

# 💻 컴퓨터 네트워크 시리즈  

> 이 시리즈는 『혼자 공부하는 네트워크』 (강민철 저)
> <br> + 인프런 강의를 기반으로 **개인적으로 복습 및 정리한 기록**입니다.

---

## 📨 HTTP 헤더란?

- HTTP 메시지는 **헤더 필드**를 통해 다양한 부가 정보를 전달
- `헤더이름: 값` 형태로 구성되며, **요청 헤더 / 응답 헤더 / 공통 헤더**로 구분

---

## 📤 요청 헤더 (Request Header)

서버에 요청을 보낼 때 함께 전달되는 헤더

### 🏠 Host  
- 요청 대상 호스트(도메인/포트)를 명시  
- 하나의 IP에 여러 도메인이 연결된 경우 식별

### 🧭 User-Agent  
- 요청을 생성한 **클라이언트 프로그램 정보**  
- 브라우저, OS 등 클라이언트 정보 포함  
<div style="text-align: center;">
  <img src="assets/img/cs/user_agent.png" alt="user-agent">
  <sub>출처: 『혼자 공부하는 네트워크』 (강민철 저)</sub>
</div>

### 🌍 Referer  
- 현재 요청의 유입 경로(직전 페이지) 명시  
- 유입 분석, 마케팅 등에 활용  
<div style="text-align: center;">
  <img src="assets/img/cs/referer_example.jpg" alt="referer">
  <sub>출처: 『혼자 공부하는 네트워크』 (강민철 저)</sub>
</div>

> 위키피디아에 있다가 내 페이지에 들어왔구나

### 🔐 Authorization  
- 인증 정보 포함 헤더 (ex. `Basic`, `Bearer`)  
- 기본 방식: `Basic base64(username:password)`  
<div style="text-align: center;">
  <img src="assets/img/cs/authorization.png" alt="authorization">
  <sub>출처: 『혼자 공부하는 네트워크』 (강민철 저)</sub>
</div>

---

## 📥 응답 헤더 (Response Header)

서버가 클라이언트에 응답할 때 제공하는 부가 정보

### 🛠️ Server  
- 서버 측 소프트웨어 정보 명시  
<div style="text-align: center;">
  <img src="assets/img/cs/server.png" alt="server">
  <sub>출처: 『혼자 공부하는 네트워크』 (강민철 저)</sub>
</div>

### 🚫 Allow  
- 허용된 HTTP 메서드 명시  
- `405 Method Not Allowed` 응답 시 포함

### ⏳ Retry-After  
- `503 Service Unavailable` 응답 시 재요청 가능 시간 명시  
<div style="text-align: center;">
  <img src="assets/img/cs/retry_after.png" alt="retry-after">
  <sub>출처: 『혼자 공부하는 네트워크』 (강민철 저)</sub>
</div>

> 2024년 8월 23일 금요일 9시 이후로 사용 가능, 120초 이후 사용 가능

### 📍 Location  
- 자원의 새로운 위치 명시 (리다이렉션, 생성된 자원 등)

### 🧾 WWW-Authenticate  
- `401 Unauthorized` 응답 시 사용  
- 인증 방식(Basic 등)을 설명  
<div style="text-align: center;">
  <img src="assets/img/cs/authenticate.png" alt="www-authenticate">
  <sub>출처: 『혼자 공부하는 네트워크』 (강민철 저)</sub>
</div>

### 🔁 Basic 인증 흐름
<div style="text-align: center;">
  <img src="assets/img/cs/basic.png" alt="basic-auth-flow">
  <sub>출처: 『혼자 공부하는 네트워크』 (강민철 저)</sub>
</div>

---

## 🔁 공통 헤더 (요청·응답 모두 사용)

### 📅 Date  
- 메시지가 생성된 날짜와 시각 명시

### 🔗 Connection  
- 연결 방식 명시 (`keep-alive`, `close` 등)

### 📦 Content-Length  
- 본문 데이터의 크기(byte)

### 🏷️ 표현 헤더 (Representation Headers)  
- 본문의 타입·언어·압축방식 명시  
- `Content-Type`, `Content-Language`, `Content-Encoding`

---

## ⚙️ HTTP 기반 기술

### 📄 캐시 (Cache)  
- **사본 데이터를 저장해 재사용**하는 기술  
- 브라우저(Private), 중간 서버(Public)에 저장 가능

#### 🧪 캐시 신선도
- `Expires`, `Cache-Control: max-age`로 유효 기간 설정  
- 신선도 재검사
  - `If-Modified-Since` – 날짜 기준 변경 여부 확인  
  - `If-None-Match` – ETag(버전 식별자) 기준 확인  
  - `Last-Modified` – 최종 수정일 제공  
- 변경 없음 시 → `304 Not Modified` 응답

---

### 🍪 쿠키 (Cookie)

- **클라이언트에 저장된 서버 측 상태 정보**  
- <이름=값> 쌍 구조 + 다양한 속성 포함

#### 🍽️ 인증 흐름
1. 클라이언트가 인증 정보 전송  
2. 서버가 세션 ID 발급 및 `Set-Cookie` 헤더로 전달  
3. 클라이언트는 추후 요청에 `Cookie` 헤더로 세션 ID 포함  
4. 서버는 세션 ID로 클라이언트 식별

#### 🧾 주요 헤더
- `Set-Cookie` – 응답 시 쿠키 설정  
- `Cookie` – 요청 시 쿠키 포함  

#### ⚙️ 쿠키 속성
- `Domain`, `Path` – 적용 범위 제어  
- `Expires`, `Max-Age` – 유효 기간  
- `Secure`, `HttpOnly` – 보안 옵션

---

### 🗄️ 웹 스토리지 (Web Storage)

- 클라이언트에 저장되는 **<키-값> 형태의 데이터**
- 쿠키와 달리 서버로 자동 전송되지 않음
- `localStorage`: 영구 저장  
- `sessionStorage`: 브라우저 종료 시 삭제

---

### 🧪 콘텐츠 협상 (Content Negotiation)

- 클라이언트 선호에 따라 **자원의 표현 방식 결정**

| 헤더 | 설명 |
|------|------|
| `Accept` | 미디어 타입 |
| `Accept-Language` | 자연어 |
| `Accept-Charset` | 문자 인코딩 |
| `Accept-Encoding` | 압축 방식 |

- `q=0~1`로 선호도 우선순위 설정 가능 (기본값: 1)

---

## ✅ 마무리 정리  

HTTP 헤더는 **요청·응답 흐름을 풍부하게 구성하는 핵심 요소**  
- 요청 헤더로 **자원 요청, 인증 정보, 클라이언트 정보** 전달  
- 응답 헤더로 **상태 관리, 인증 안내, 리다이렉션** 등 수행  
- 공통 헤더 및 기반 기술로 **성능 최적화와 사용자 맞춤화** 지원

---

## 📚 참고 자료

- 『혼자 공부하는 네트워크』 – 강민철 저  
- [인프런 강의 – 혼자 공부하는 네트워크](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B3%B5%ED%95%99-%ED%98%BC%EC%9E%90%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC){: target="_blank"}

---

읽어주셔서 감사합니다 🙌  
틀린 부분이 있거나, 도움이 되셨다면 댓글이나 GitHub Issue로 자유롭게 알려주세요 😊
