---
layout: post
title: pwnable.kr - bof.
categories: [CTF]
tags: [Exploit, CTF, pwnable.kr]
fullview: false
comments: true
published: true
---

pwnable.kr 의 세 번째 문제인 ‘bof’ 입니다. 해당 문제는 buffer overflow에 대한 기본적인 이해가 있다면 풀 수 있습니다.  
  
    
#### 1. 내려받을 수 있는 파일과 소스코드가 제공되고 'nc'를 이용하여 접속 가능한 연결정보가 명시되어 있습니다. 
![solve-1](https://bongbongco.github.io/images/2017/2017-01-23-pwnableKr-bof-1.png)  

#### 2. 'bof', 'bof.c' 파일을 내려 받은 후, file 명령어를 이용하여 'bof' 파일 정보를 확인합니다.
![solve-1](https://bongbongco.github.io/images/2017/2017-01-23-pwnableKr-bof-2.png)  

'file' 명령어는 파일의 종류를 확인하는 명령어입니다. Windows 환경에서는 확장자나 아이콘 등 파일 종류를 쉽게 확인할 수 있지만 리눅스 환경에서는 파일 명만 보고는 파일 종류를 파악하기 힘든 경우가 많습니다. 이때, 'file' 명령어를 사용하여 파일 종류를 알 수 있습니다.  


#### 3. 리눅스 환경으로 이동하여 gdb를 실행하고 'key' 값 비교 기능이 존재하는 'func'함수에 브레이크 포인트를 설정하여 프로그램을 실행합니다.
![solve-1](https://bongbongco.github.io/images/2017/2017-01-23-pwnableKr-bof-3.png)  

#### 4. 
![solve-1](https://bongbongco.github.io/images/2017/2017-01-23-pwnableKr-bof-4.png)  

#### 5. 
![solve-1](https://bongbongco.github.io/images/2017/2017-01-23-pwnableKr-bof-5.png)  

#### 6. 
![solve-1](https://bongbongco.github.io/images/2017/2017-01-23-pwnableKr-bof-6.png)  

#### 7. 
![solve-1](https://bongbongco.github.io/images/2017/2017-01-23-pwnableKr-bof-7.png)  

#### 8. 
![solve-1](https://bongbongco.github.io/images/2017/2017-01-23-pwnableKr-bof-8.png)  

#### 9. 
![solve-1](https://bongbongco.github.io/images/2017/2017-01-23-pwnableKr-bof-9.png)  
