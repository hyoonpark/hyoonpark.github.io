---
layout: post
title: "[Network] DNS와 자원"
date: 2025-05-29 12:30 +09:00
categories: cs network
tags: [github, tech, blog, network, dns, uri, url, 네트워크]
---

> **3줄 요약**
<br>DNS는 도메인 네임을 IP 주소로 변환하는 계층적 분산 시스템
<br>도메인을 관리하는 다양한 네임 서버가 질의를 통해 IP 주소를 응답
<br>자원은 URI로 식별되며, URL과 URN은 각각 위치와 이름 기반 식별자
{: .prompt-tip }

# 💻 컴퓨터 네트워크 시리즈

> 이 시리즈는 『혼자 공부하는 네트워크』 (강민철 저)
> <br> + 인프런 강의를 기반으로 **개인적으로 복습 및 정리한 기록**입니다.

---

## 🌐 DNS(Domain Name System)

### 📌 기본 개념

- 계층적, 분산된 도메인 네임 관리 체계
- 도메인 네임: 문자열 형태로 된 호스트 주소
- IP 주소 대신 기억하기 쉬운 이름 사용
- 네임 서버(DNS 서버)에서 관리

### 🏷 도메인 구조

- 점(.) 기준 계층적 분류
  - 루트(root) 도메인 → 최상위도메인(Top-Level Domain, TLD) → 2단계/3단계 도메인 등
- FQDN (Fully-Qualified Domain Name): 전체 계층 포함한 도메인 이름
- **네임 서버는 전 세계에 분산**

### 🧩 계층적 네임 서버 구조

- 로컬 네임 서버 → 루트 네임 서버 → TLD 네임 서버 → 책임 네임 서버

| 네임 서버 | 역할 |
|-----------|------|
| 로컬 네임 서버 | 클라이언트 가장 가까운 DNS, 일반적으로 ISP 제공 |
| 루트 네임 서버 | 루트 도메인 담당, TLD 서버 위치 반환 |
| TLD 네임 서버 | .com, .net 등 TLD 관리, 하위 도메인 네임 서버 반환 |
| 책임 네임 서버 | 도메인 영역(zone) 최종 관리 |

### 🔄 질의 방식

#### 재귀적 질의 (recursive query)

- 클라이언트 → 로컬 DNS가 대신 전체 탐색
- 최종 응답까지 역순으로 결과 반환

![재귀적 질의](assets/img/cs/recursive_query.png)
<sub>출처: 『혼자 공부하는 네트워크』 강민철 저</sub>

#### 반복적 질의 (iterative query)

- 각 네임 서버에 직접 질의-응답 반복

![반복적 질의](assets/img/cs/iterative_query.png)
<sub>출처: 『혼자 공부하는 네트워크』 강민철 저</sub>

> ⚠ 재귀적·반복적 질의는 루트 서버 과부하 및 네트워크 지연 가능성 존재

---

## 📥 DNS 캐시 & hosts 파일

### 📌 DNS 캐시

- 이전 응답 저장하여 재사용
- 응답 속도 향상
- TTL(Time To Live) 만료 시 삭제

### 📁 hosts 파일

- 로컬에서 도메인-IP 직접 매핑
- 위치: `/etc/hosts`

```bash
$ vi /etc/hosts

# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost
255.255.255.255 broadcasthost
::1             localhost
```

---

## 🧾 자원(Resource) 식별

### 📌 URI (Uniform Resource Identifier)

- 자원 식별자
  - URL (Locator): 위치 기반
  - URN (Name): 이름 기반

### 🔗 URL 구조 (RFC 3986 기준)

1. **scheme**: http, https 등 자원 접근 방법  
2. **authority**: 도메인 혹은 IP 주소, 포트  
3. **path**: 자원이 위치한 경로  
4. **query**: 검색/정렬 등의 요청 정보  
5. **fragment**: 자원의 특정 부분 가리킴

> 예시: `https://www.example.com:443/path/resource?query=value#section`

### 🧬 URN

- 위치와 무관한 자원 식별
- 고유 이름으로 자원 추적

---

## 📄 DNS 레코드

### 💡 예시

<div>
  <img src="assets/img/cs/dns_example.png" alt="dns 예시" style="width: 75%;"/>
  <sub>출처: 『혼자 공부하는 네트워크』 강민철 저</sub>
</div>

- `example.com.` → `1.2.3.4` 응답
- TTL: 300초

### 🔠 레코드 유형

![레코드 유형](assets/img/cs/record_type.png)
<sub>출처: 『혼자 공부하는 네트워크』 강민철 저</sub>

---

## ✅ 마무리 정리

DNS는 도메인 네임을 IP로 변환하는 핵심 인프라  
자원 식별은 URI를 통해 수행되며, URL이 가장 널리 사용  
DNS 구조와 질의 방식, 자원 식별자의 이해는 네트워크 설계에 필수  

---

## 📚 참고 자료

- 『혼자 공부하는 네트워크』 - 강민철 저  
- [인프런 강의 - 혼자 공부하는 네트워크 기반 강의](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B3%B5%ED%95%99-%ED%98%BC%EC%9E%90%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC){: target="_blank"}

---

읽어주셔서 감사합니다 🙌  
도움이 되었다면 댓글이나 GitHub Issue로 알려주세요 😊
