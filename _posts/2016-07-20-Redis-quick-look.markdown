---
layout: post
title: 레디스 훑어보기.
---

Redis
=====

+ 목적 : 보안 가이드 작성
+ 조사 내용
	+ 운영 환경(설치 및 간단한 운용 방법)  

Windows
------
	+ Visual studio 2013(최신 버전 redis)을 이용하여 직접 소스 컴파일 (소스 경로 : https://github.com/MSOpenTech/redis)
	+ 생성된 실행 파일 복사 
	+ 환경설정파일 복사 (\redis-3.0\msvs\setups\documentation\redis.windows.conf -> 실행 파일이 존재하는 디렉터리에 redis.conf 파일로 복사)
	+ 환경설정파일 수정 (bind 127.0.0.1, port 6379, logfile "C:\Temp\Redis.log")
	+ 서비스 등록 : \redis-server.exe --service-install redis.conf --loglevel verbose
	+ 서비스 실행 : \redis-server.exe --service-start
	+ 클라이언트 접속 테스트 : redis-cli.exe -h 127.0.0.1 -p 6379
~~~
127.0.0.1:6379> set id lsy
OK
127.0.0.1:6379> get id
"lsy"
~~~
	+ 서비스 중지 : \redis-server.exe --service-stop
	+ 서비스 제거 : \redis-server.exe --service-uninstall
	+ 비밀번호 인증 시 : auth [password]

Linux
------
	+ Redis 최신 버전 소스 다운로드 (소스 경로 : wget http://download.redis.io/releases/redis-3.0.1.tar.gz)
	+ 다운받은 소스 빌드
~~~
$ tar xzf redis-3.0.1.tar.gz
$ cd redis-3.0.1
$ sudo make
$ sudo make install
~~~
	+ utils 디렉터리 안에 설치 파일 실행 ($ sudo ./install_server.sh)
	+ /usr/local/bin/ 디렉터리로 이동하여 서버 실행 (On / Off → $ sudo /etc/init.d/redis_6379 start / $ sudo /etc/init.d/redis_6379 stop)

+ 사용 용도
: Redis 는 Key/Value Store로 데이터베이스 캐시 혹은 메시지 서버로 활용된다. (넓은 의미에서 NoSQL로 분류할 수 도 있고 In memory 솔루션으로 분류도 가능하다.) 그 밖에 서버 간에 공유 메모리를 넣어서 서버간에 상태 정보 유지를 위해 사용할 수 있다.  
  
+ 특징
	* 데이터 저장소로 가장 I/O 속도가 빠른 장치인 메모리를 사용
	* 단순한 Key/Value 방식으로 빠른 속도 보장
	* 캐시 및 데이터 스토어 구축에 유리
	* 다양한 API 지원
  
+ 보안 가이드 필수 작성 항목
	+ 디렉터리 쓰기 권한 제거
	+ 설정 파일 쓰기 권한 제거
	+ 비밀번호 설정
		requirepass [password]  
		: client에게 다른 command들을 수행하기 전에 password를 요구하도록 설정한다. 주의: Redis는 매우 빠르기 때문에 1초 당 15만개의 password를 시도할 수 있다. 따라서 매우 강력한 password를 설정해야 한다.  

+ 최신 보안 패치 적용
: 최근 발견된 취약점으로 인해 2.8.24 미만 버전, 3.0.6 미만 버전의 사용을 금한다.
~~~
CVE-2015-4335 Redis before 2.8.1 and 3.x before 3.0.2 allows remote attackers to execute arbitrary Lua bytecode via the eval command.
CVE-2015-8080 Redis 2.8.x before 2.8.24 and 3.0.x before 3.0.6
~~~

+ 기타 특이사항
	+ Redis 는 SSL 통신을 지원하지 않음. 따라서 암호화 통신이 필요한 경우 stunnel의 이용을 권장하고 있다. 
	+ 특정 command 변경. 운영에 영향을 미칠 수 있는 특정 command 들을 변경하여 운영       
		rename-command [target-command] [new-command]  
		: 공유되는 환경에서는 위험한 command들의 이름을 변경할 수 있다. 예를 들어서 CONFIG command를 추측하기 어려운 다른 값으로 변경할 수 있다. 물론 internal-use tool로는 해당 명령어가 사용하지만, 일반적인 외부 client들에 대해서는 불가능하다.
~~~
예) rename-command CONFIG b840fc02d524045429941cc15f59e41cb7be6c52
또한 command를 공백으로 rename해서 완전히 사용 불가능하게 할 수도 있다.
예) rename-command CONFIG ""
~~~
+ 참고 URL : http://redis.io/topics/security

