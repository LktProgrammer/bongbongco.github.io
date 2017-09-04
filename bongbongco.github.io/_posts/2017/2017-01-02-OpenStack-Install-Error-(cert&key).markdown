---
layout: post
title: 오픈스택 Answer 파일 이용하여 설치 중 인증서 오류
categories: [Trubleshooting]
tags: [Trubleshooting, Error, OpenStack]
fullview: false
comments: true
published: true
use_math: false
---

오픈스택 설치를 마무리하기 위해서는 인증서가 필요하다.

### 필요 인증서 
+ certs @/etc/pki/tls/certs/ 
++ selfcert.crt
++ ssl_vnc.crt
++ ssl_dashboard.crt
+ private key @ /etc/pki/tls/private/
++ selfcert.key
++ ssl_vnc.key
++ ssl_dashboard.key

생성된 answer 파일을 이용하여 설치 시 인증서 오류로 인하여 오류가 발생하는 것을 확인할 수 있다. 이 경우 answer 파일에서 해당 항목을 검색하여 경로를 수정해주고 해당 경로에 인증서를 넣어주면 정상적으로 설치에 성공할 수 있다.

```
CONFIG_SSL_CACERT_FILE=/etc/pki/tls/certs/selfcert.crt

CONFIG_SSL_CACERT_KEY_FILE=/etc/pki/tls/private/selfkey.key

CONFIG_VNC_SSL_CERT=/etc/pki/tls/certs/ssl_vnc.crt

CONFIG_VNC_SSL_KEY=/etc/pki/tls/private/ssl_vnc.key

CONFIG_HORIZON_SSL_CERT=/etc/pki/tls/certs/ssl_dashboard.crt

CONFIG_HORIZON_SSL_KEY=/etc/pki/tls/private/ssl_dashboard.key

CONFIG_HORIZON_SSL_CACERT=/etc/pki/tls/certs/selfcert.crt
```

아래 명령어를 사용하여 위에서 언급된 인증서 및 인증 키를 생성한다.

**openssl req -x509 -sha256 -newkey rsa:2048 -keyout /etc/pki/tls/private/selfkey.key -out /etc/pki/tls/certs/selfcert.crt -days 365 -nodes**

#### 참고
> [Error while installing openstack 'newton' using rdo packstack](https://ask.openstack.org/en/question/97645/error-while-installing-openstack-newton-using-rdo-packstack/)
>[How to Install Your Own Cloud Platform with OpenStack in RHEL/CentOS 7](http://www.tecmint.com/openstack-installation-guide-rhel-centos/)
