---
layout: post
title: "[TIL]구간합"
date: 2024-11-28 19:52 +09:00
categories: algorithm til
tags:
    [
        algorithm,
        til,
        prefix_sum,
        구간합
    ]
---
# 구간합(Prefix Sum)
배열을 이용한 알고리즘이다.

## 합배열
배열 A가 있을 때 합배열 S구하기.
S[i]는 A[0]부터 A[i]까지의 합
```java
S[i] = A[0] + A[1] + A[2] + ... + A[i - 1] + A[i]
S[i] = S[i - 1] + A[i]
```

## 구간합
합배열을 이용해 배열 A의 특정 구간의 합을 쉽게 구할 수 있다.
```java
/*
배열 A의 i에서 j까지의 구간합을 구해보자.
*/
S[p] = S[j] - S[i - 1]
```
### 코드 구현(백준 11659)
[구간 합 구하기 4](https://www.acmicpc.net/problem/11659){: target="_blank"}
<details>
<summary>정답 코드</summary>
<div markdown="1">

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {

        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));  // 시간복잡도를 생각해서 Scanner보다 빠른 버퍼리더를 사용해준다.
        StringTokenizer stringTokenizer = new StringTokenizer(bufferedReader.readLine());  // 나열된 숫자를 int로 받게 되면 시간이 많이 걸려 stringtokenizer를 이용해 받아준다.

        int n = Integer.parseInt(stringTokenizer.nextToken());
        int m = Integer.parseInt(stringTokenizer.nextToken());

        long[] S = new long[n + 1];  // i-1 작업 없이 바로 사용하기 위해 n+1을 해준다.

        stringTokenizer = new StringTokenizer(bufferedReader.readLine());

        for (int i = 1; i < n + 1; i++) {
            S[i] = S[i - 1] + Integer.parseInt(stringTokenizer.nextToken());
        }

        for (int q = 0; q < m; q++) {
            stringTokenizer = new StringTokenizer(bufferedReader.readLine());

            int i = Integer.parseInt(stringTokenizer.nextToken());
            int j = Integer.parseInt(stringTokenizer.nextToken());

            long answer = S[j] - S[i - 1];  // 구간합 공식을 사용해준다.

            System.out.println(answer);
        }
    }
}
```

</div>
</details>