---
layout: post
title: pwnable.kr - collision.
categories: [CTF]
tags: [Exploit, CTF, pwnable.kr]
fullview: false
comments: true
published: true
---

pwnable.kr 의 두 번째 문제인 'collision' 입니다. 해당 문제는 Hex 값 처리에 대한 이해가 있다면 풀 수 있습니다.  
  
    
#### 1. 문제가 저장된 서버로 접속할 수 있는 접속 정보를 보여주고 있습니다.
![solve-1](https://bongbongco.github.io/images/2017/2017-01-20-pwnableKr-collision-1.png)  
  
  
#### 2. 접속 정보를 이용해서 'collision' 문제 서버에 접속했습니다.
![solve-2](https://bongbongco.github.io/images/2017/2017-01-20-pwnableKr-collision-2.png)  
소스파일, 실행파일, 정답파일로 총 3개의 파일이 존재하는 데, 소스 파일을 열어서 내용을 확인해보겠습니다.
  
  
#### 3. 인자가 존재하는 지 확인 후 check_password 함수 수행결과가 '0x21DD09EC'와 일치하면 flag 값을 출력합니다.
![solve-3](https://bongbongco.github.io/images/2017/2017-01-20-pwnableKr-collision-3.png)  
이번 문제의 핵심인 'check_password' 함수를 살펴보겠습니다. 프로그램 실행 시 전달한 인자 값을 정수형 포인터를 이용해서 4바이트 단위로 접근하는 것을 확인할 수 있습니다. 그리고 접근한 값에서 4바이트씩 5번 이동하며 읽어들인 값을 더해주고 그 값을 리턴합니다. 
  
```cpp
unsigned long check_password(const char* p){
  int* ip = (int*)p;
  int i;
  int res=0;
  for(i=0; i<5; i++){
    res += ip[i];
  }
  return res;
}
```
  
  
  
  
#### 4. python을 이용해서 5번 더해서 'hashcode'가 완성되는 계산합니다.
![solve-4](https://bongbongco.github.io/images/2017/2017-01-20-pwnableKr-collision-4.png)  
이미지에서 볼 수 있듯이 'hashcode'를 5로 나누어 반복적으로 더할 값을 구합니다. 나머지 연산을 통해서 나머지 값도 포함하여 값을 구성하여야합니다.
  
```python
hex(0x21DD09EC/5)
hex(0x21DD09EC%5)
```
  
계산 식을 구성하는 방법은 여러가지가 될 수 있습니다. 결과적으로 5번 더해서 'hashcode' 값이 나오면 되므로 단순하게 '\x01\x01\x01\x01\x01\x01\x01\x01\x01\x01\x01\x01\x01\x01\x01\x01\xE8\x05\xD9\x1D' 처럼 '\x01' 16개를 나열하고 'hashcode'에서 '\x04\x04\x04\x04'를 뺀 값을 덧붙여 구성할 수 있습니다.
  
  
  
  
#### 5. python을 이용해서 구한 값을 'col' 프로그램의 인자 값으로 전달하여 flag 값을 획득하였습니다.
![solve-5](https://bongbongco.github.io/images/2017/2017-01-20-pwnableKr-collision-5.png)  
  
  
#### 6. 획득한 flag 값을 pwnable.kr 에 입력한 결과 3포인트를 얻었습니다.
![solve-6](https://bongbongco.github.io/images/2017/2017-01-20-pwnableKr-collision-6.png)  
  
  
#### 7. collision 문제 풀이를 완료하였습니다.
![solve-7](https://bongbongco.github.io/images/2017/2017-01-20-pwnableKr-collision-7.png)  
