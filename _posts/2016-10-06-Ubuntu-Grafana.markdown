---
layout: post
title: Grafana 설치 및 TLS v1.0 제거.
---

Influxdb 설치
------

~~~
wget https://dl.influxdata.com/influxdb/releases/influxdb_1.0.1_amd64.deb
sudo dpkg -i influxdb_1.0.1_amd64.deb
sudo /etc/init.d/influxdb start
http://{ip}:8083
CREATE DATABASE "cubrid"
http://influxdb.com/docs/v0.8/introduction/getting_started.html(설정 참고)
- sudo vi /opt/influxdb/shared/config.toml
~~~

Grafana 설치
------

~~~
wget http://grafanarel.s3.amazonaws.com/builds/grafana-3.1.1-1470047149.deb
dpkg -i grafana-3.1.1-1470047149.deb
service grafana-server start
cd /etc/grafana
sudo openssl genrsa -out grafana.key 2048
sudo openssl req -new -key grafana.key -out grafana.csr
sudo openssl x509 -req -days 365 -in grafana.csr -signkey grafana.key -out grafana.crt
vi /etc/grafana/grafana.ini

cert_file=/etc/grafana/grafana.crt
cert-Key=/etc/grafana/grafana.key
protocol=https

https://{ip}:3000
~~~

Grafana TLS v1.0 제거
------

+ 소스 파일 수정
/pkg/cmd/grafana-server/server.go  
/pkg/cmd/grafana-server/web.go  

~~~
import (
	"crypto/tls"
	"net/http"
)

err := http.ListenAndServeTLS(addr, "crtfile", "keyfile", handler)

config := &tls.Config{MinVersion: tls.VersionTLS11}
server := &http.Server{Addr: addr, Handler: handler, TLSConfig: config}
err := server.ListenAndServeTLS("crtfile", "keyfile")
~~~
