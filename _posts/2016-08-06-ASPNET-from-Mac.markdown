---
layout: post
title: 맥에서 ASP.NET 개발하기.
---

맥을 구입하고 JAVA와 Swift를 열심히하려 했으나;; (안드로이드는 하고 있으나, JAVA 웹 프로그래밍이나 Swift는 아직 못하고 있다. 아쉽다. 모바일 프로그래밍이 생각보다 재밌어서 안드로이드를 만지고 있다보면 시간이 어떻게 가는 지 모르겠다.) 얼마 지나지 않아서 업무 상 ASP.NET 지식이 필요하게 되었다. ASP.NET 공부를 위해서는 Windows가 편할텐데, 추가적으로 OS를 설치하고 싶은 생각이 없어서 .NET 개발환경을 구축하여 사용하는 것으로 결정하였고 그 방법을 간략히 정리한다.  

설치가 필요해
------
+ Homebrew

~~~
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
~~~

+ openssl

~~~
brew update
brew install openssl
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/ 
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
~~~

+ .NET Core SDK

~~~
wget -O dotnet.pkg https://go.microsoft.com/fwlink/?LinkID=809124
~~~

여기까지 설치가 완료되면 기본적인 준비를 완료한 것이다. 정상 동작 여부를 확인하자.

~~~
mkdir testapp
cd testapp
dotnet new
~~~

여기까지만 해도 사용은 가능하지만 실제 활용하기에는 너무 불편하기 때문에 YEOMAN을 추가로 설치한다.

+ YEOMAN을 사용하기 위해서는 기본적으로 RUBY와 GIT이 설치되어 있어야 한다.
+ Node Version Manager (node가 설치되어 있지 않다면 설치해! 지금은 2016년이야!)

~~~
curl https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash
source ~/.bash_profile
nvm --version
nvm install stable
~~~

+ YEOMAN

~~~
npm install -g yo grunt-cli bower gulp
npm install -g generator-aspnet
~~~

이제 YEOMAN으로 프로젝트를 구성하여 마음껏 프로그래밍하면 된다.

~~~
yo aspnet

dotnet restore
dotnet bulid
dotnet run
~~~

![run testapp](/_asset/dotnet_testapp.png)
