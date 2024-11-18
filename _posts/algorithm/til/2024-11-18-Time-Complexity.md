---
layout: post
title: "[TIL]시간 복잡도"
date: 2024-11-18 13:25 +09:00
categories: algorithm til
tags:
    [
        algorithm,
        til,
        time_complexity,
        시간복잡도
    ]
---
> **3줄 요약**
<br>연산횟수로 **알고리즘 선택의 기준**
<br>상수는 계산에서 제외하고 **가장 많이 중첩**된 반복문이 기준
<br>알맞은 알고리즘을 선택했다면 **내가 짠 코드가 효율적**으로 짜져있는지 확인
{: .prompt-tip }

# 시간 복잡도(Time Complexity)

## 1. 시간 복잡도 이해하기
### 1-1 시간 복잡도
- 알고리즘이 수행될 때 필요한 **“데이터 개수”**와 **“알고리즘 시간 복잡도”**에 따라 **“효율적인 알고리즘”**을 나타내는 척도
  - 쉽게 말해 **“연산횟수”**로 볼 수 있다.
  - 알고리즘 선택의  기준이 된다.
- 자바에서 약 1억번 연산할 때 1초가 걸린다고 간주
  - 예를 들어 시간 제한이 2초인 문제가 있을때 2억번 연산 안에 답이 도출되어야 한다.
### 1-2 유형
- 빅-오메가(𝛺(n)) : 알고리즘이 최선일 때
- 빅-세타(𝜃(n)) : 알고리즘이 보통일 때
- 빅-오(𝛰(n)) : 알고리즘이 최악일 때
![time_complexity_sheet](assets/img/til/time-complexity-sheet.jpg)
  출처 : [Big-O Algorithm Complexity Cheat Sheet \(Know Thy Complexities!\) @ericdrowell](https://www.bigocheatsheet.com/)

## 2. 시간 복잡도 계산하기
- 연산횟수 = 알고리즘 시간 복잡도 x 데이터 크기
  - e.g) 버블정렬(O(n^2)), 데이터크기 = 1000000(백만)
    - (1000000)^2 = 1경

## 3. 코딩테스트에서 시간 복잡도
### 3-1 내가 작성한 코드
- 상수는 시간 복잡도 계산에서 제외
  - e.g) O(n) == O(3n)
- **가장 많이 중첩된 반복문**의 수행 횟수가 시간 복잡도의 기준
### 3-2 코딩테스트에서 유의할 점
- 알맞은 알고리즘을 선택
- 내가 짠 코드에서 비효율적인 부분을 찾아서 효율적으로 수정
  - 알고리즘은 잘 선택했는데 내가 짠 코드를 놓치는 경우가 많다.


<br> 알고리즘을 계속 공부하면서 내용을 추가할 계획

<br><br><br><br>
참고자료<br>
[시간 복잡도, 공간 복잡도, 빅오 표기법 이해하기](https://adjh54.tistory.com/186#3)<br>
[Big-O Complexity Chart](https://www.bigocheatsheet.com/)