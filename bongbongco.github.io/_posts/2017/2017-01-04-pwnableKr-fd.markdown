---
layout: post
title: pwnable.kr - fd.
categories: [CTF]
tags: [Exploit, CTF, pwnable.kr]
fullview: false
comments: true
published: true
---

pwnable.kr 의 첫 번째 문제인 'fd' 입니다. 해당 문제는 파일 디스크립터를 정확히 알고있는 지를 묻고 있습니다.  

#### 1. 문제가 저장된 서버로 접속할 수 있는 접속 정보를 보여주고 있습니다.
![solve-1](https://bongbongco.github.io/images/2017/2017-01-04-pwnableKr-fd-1.png)  <br/><br/>

#### 2. 문제 풀이를 위해서 ssh 연결을 하였습니다.
![solve-2](https://bongbongco.github.io/images/2017/2017-01-04-pwnableKr-fd-2.png)  
파일이 3개 존재하는 것을 확인할 수 있습니다. 그 중에서 'fd.c' 파일을 열어 내용을 확인해 보겠습니다. <br/><br/>

#### 3. 인자가 존재하는 지 확인 후 'buf'에 'LETMEWIN' 문자열이 있다면 flag 값을 출력합니다. 
![solve-3](https://bongbongco.github.io/images/2017/2017-01-04-pwnableKr-fd-3.png)  
이미지에서 확인할 수 있듯이 특정 문자열이 존재하는 지 확인하는 형태의 문제입니다. 특이사항이라면 파일 디스크립터 값을 처리하는 방식입니다. 입력 받은 인자 값에서 0x1234를 뺀 값을 파일 디스크립터로 사용하고 있습니다.

| 파일 디스크립터  | 대상                       |
| :-------------: | :------------------------ |
| 0               | 표준입력 : Standard Input  |
| 1               | 표준출력 : Standard Output |
| 2               | 표준에러 : Standard Error  |

'buf'에 'LETMEWIN'을 입력하여 flag 값을 확인하기 위해서는 'fd' 값을 0(표준입력)으로 만들어야하므로 0x1234의 10진수인 4660을 인자 값으로 넣어줍니다.  <br/><br/>

#### 4. 'fd' 파일의 인자 값으로 4660을 전달 후 'LETMEWIN' 을 입력하여 flag 값을 확인하였습니다.
![solve-4](https://bongbongco.github.io/images/2017/2017-01-04-pwnableKr-fd-4.png) <br/><br/>
 
#### 5. 해당 flag 값을 입력하여 문제 풀이에 성공하였습니다.
![solve-5](https://bongbongco.github.io/images/2017/2017-01-04-pwnableKr-fd-5.png)
