---
layout: post
title: Git Please tell me who you are Error.
---

* 에러 구문

~~~
*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'root@raspberrypi.(none)')
~~~

Commit 시도 시 위와 같은 에러가 발생한다면 다음과 같이 입력하여 해결할 수 있다.

~~~
1.git init
2.git config user.name "someone"
3.git config user.email "someone@someplace.com"
4.git add *
5.git commit -m "some init msg"
~~~