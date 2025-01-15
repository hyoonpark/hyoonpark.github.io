---
layout: post
title: "[CursorAI]CursorAI를 활용한 웹 포트폴리오 만들기"
date: 2025-01-15 16:40 +09:00
categories: etc
tags:
    [
        github,
        tech,
        blog,
        portfolio,
        cursorai,
        vscode
    ]
---

[완성된 포트폴리오 사이트](https://hyoonpark.github.io/portfolio/){: target="_blank"}

<font color="#cccccc"><i>CursorAI를 모두 설치했다고 가정하고 스따뚜! 설치 방법이 궁금하시다면 이전 포스트를 참고해주세요!</i></font>

# CursorAI로 웹 포트폴리오 제작하기
Mac OS 기준으로 설명합니다.

## 프로젝트 소개

CursorAI의 AI 코딩 지원 기능을 활용하여 개인 웹 포트폴리오를 제작하는 과정을 설명합니다.
이 프로젝트를 통해 CursorAI의 실제 활용 사례를 보여드리고자 합니다.

## 1. 프로젝트 준비

### 프로젝트 목표
- 반응형 웹 포트폴리오 제작
- 개인 프로젝트 및 기술 스택을 효과적으로 전시
- 깔끔하고 모던한 UI/UX 구현
- 직관적인 사용자 경험 제공

### 기술 스택
- **프론트엔드 프레임워크**: React
- **스타일링**: Tailwind CSS
- **개발 언어**: TypeScript
- **버전 관리**: Git/GitHub
- **배포**: GitHub Pages

### 레이아웃 구상
- 단일 페이지 구성(SPA)
- 직관적인 네비게이션
- 반응형 그리드 시스템
- 모던한 애니메이션 효과

## 2. 개발 환경 구성
- Node.js 설치 및 설정
  - <font color="#cccccc"><i>Node.js는 이미 설치되어 있다고 가정하고 진행하겠습니다. 
설치가 필요하신 분들은 <a href="https://nodejs.org" target="_blank">Node.js 공식 웹사이트</a>에서 LTS 버전을 설치해주세요.</i></font>
- 필요한 개발 도구 준비
- CursorAI 환경 설정

## 3. 프로젝트 초기 설정

### React 프로젝트 생성

1. command + j 누르고 터미널 창 열기

2. command + k 눌러서 프롬프트 창 열기

3. 프롬프트 창에 다음 명령어 입력
   
   ![react_project_create](assets/img/etc/react_project_create.jpg)
   
   <font color="#cccccc"><i>주인장의 실수... 하위폴더 없이 프로젝트 생성해달라고 하세요!!</i></font>

4. 알려주는 명령어를 터미널에 입력
   
   ![react_project_create_2](assets/img/etc/react_project_create_2.jpg)

### 프로젝트 구조 설계
- 기본 설정 파일 구성
  - 프로젝트 루트 폴더에 require 폴더를 생성한다.
  - 폴더 내부에 prd.md 파일을 생성한다.

```
# Portfolio Website PRD

## 1. 프로젝트 개요
이 프로젝트는 백엔드 주니어 개발자의 포트폴리오 웹사이트로, 개발자의 소개 및 기술 스택, 프로젝트 경험 등을 효과적으로 전달하는 것을 목표로 합니다.

## 2. 핵심 구성 요소

### Contact Information
- Tech Blog (GitHub Pages)
- Gmail
- LinkedIn

### Experience
- 신세계I&C 스파로스 아카데미 4기 (2024.02 ~ 2024.07)
- 삼성 청년 SW 아카데미 9기 (2023.01 ~ 2023.12)

### Tech Stack
- **Language**: Java, Python, JavaScript
- **Backend**: Spring Boot/Cloud, Django, Flask
- **Database**: MySQL, MariaDB, PostgreSQL, MongoDB
- **Infrastructure**: AWS, Docker, Nginx, Jenkins, Linux
- **Collaboration**: Git, Jira, Gerrit

### GitHub Stats
- GitHub 활동 통계
- 주요 사용 언어 통계
- 방문자 수 카운터

## 3. 기술 명세

### 개발 스택
- **Frontend**: React, TypeScript
- **Styling**: Tailwind CSS
- **Version Control**: Git/GitHub
- **Deployment**: GitHub Pages

### 구현 요구사항
- SPA(Single Page Application) 구조
- 반응형 웹 디자인
- 모바일 최적화
- 부드러운 스크롤 애니메이션
- 프로젝트 카드 형식의 갤러리

## 4. 개발 계획

### Phase 1: 기본 구조 개발
- 컴포넌트 구조 설계
- 라우팅 설정
- 기본 레이아웃 구현

### Phase 2: 주요 기능 구현
- 헤더/네비게이션
- 메인 소개 섹션
- 프로젝트 갤러리
- 기술 스택 표시
- 연락처 섹션

### Phase 3: 스타일링 및 최적화
- 반응형 디자인 적용
- 애니메이션 효과 추가
- 성능 최적화
- 크로스 브라우저 테스트

## 5. 프로젝트 구조
portfolio-website/
├── README.md
├── require/
│ └── prd.md
├── public/
│ └── assets/
│ └── images/
├── src/
│ ├── components/
│ ├── pages/
│ ├── styles/
│ └── utils/
└── package.json
```

아래의 과정들을 cursurAI에게 전적으로 맡겨보겠습니다.
![prd_create](assets/img/etc/prd_create.jpg)
수많은 오류들을 만나고 고쳤습니다. 프론트 지식이 있으면 조금 더 쉽게 할 수 있을 것 같습니다.
물론 이 과정에서도 composer에 물어보면 잘 고쳐줍니다.

## 4. 주요 컴포넌트 개발

오늘은 기본적인 컴포넌트 구조만 만들어보겠습니다.

### 컴포넌트 구조 설계
```
src/
├── components/
│   ├── layout/
│   │   ├── Header.tsx
│   │   ├── Footer.tsx
│   │   └── Navigation.tsx
│   ├── home/
│   │   ├── Hero.tsx
│   │   ├── About.tsx
│   │   ├── Skills.tsx
│   │   ├── Projects.tsx
│   │   └── Contact.tsx
│   └── common/
│       ├── Card.tsx
│       └── Button.tsx
└── pages/
    └── Home.tsx
```

## 5. 마무리

### 오늘 배운 점
- CursorAI를 활용한 프로젝트 구조 설계
- React + TypeScript 프로젝트 생성
- 기본 컴포넌트 구조 설계

## 6. 배포 및 최적화
- GitHub Pages 배포 설정
  참고 : [배포방법](https://codingapple.com/unit/react-build-deploy-github-pages/){: 
  target="_blank"}

  <font color="#cccccc"><i>저 처럼 이미 github.io를 활용해 블로그를 하고 있다면 설정 방법이 있으니 
  참고하여 배포해보세요.</i></font>


<br><br><br><br><font color="#cccccc"><i>포트폴리오는 계속 된다~~</i></font>