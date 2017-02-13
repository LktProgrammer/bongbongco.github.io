---
layout: post
title: Git Error-Please, commit your changes or stash them before you can merge.
---

* 에러 구문

~~~
error: Your local changes to the following files would be overwritten by merge:

        Makefile

Please, commit your changes or stash them before you can merge.

Aborting
~~~

Commit 시도 시 위와 같은 에러가 발생한다면 다음과 같이 입력하여 해결할 수 있다.

~~~
1. git stash
2. git pull
3. git stash pop (pull을 하고 난 이후에는 git stash pop 명령으로 상태를 HEAD로 변경)
~~~
