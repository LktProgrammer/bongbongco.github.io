---
layout: post
title: SQL Injection (Search)
categories: [bWAPP]
tags: [Pentest, bWAPP, BeeBox]
fullview: false
comments: true
published: true
---

bWAPP 을 이용한 웹 취약점 진단 학습. SQL Injection 취약점은 사용자에게 전달 받은 인자 값을 포함하여 동적으로 쿼리를 완성하는 과정에서 인자 값에 대한 미흡한 검증으로 인해 발생한다. 이를 막기 위해서는 쿼리문 작성 시 사용되는 특수문자를 필터링하는 로직의 추가가 필요하며, Java의 'preparestatement' 와 같이 미리 SQL 문을 정의해두고 인자 값만을 전달받아 쿼리문을 완성하는 식으로 프로그램을 작성하여 의도치 않은 쿼리문이 실행되지 않게 한다.

## 1. LOW

### 1.1. Summary
쿼리 작성 시 사용되는 특수문자를 체크하는 로직 없이 입력 값을 그대로 포함하여 쿼리문을 구성하고 있다. 이로 인하여 악의적인 쿼리 수행이 가능하며 공격자가 데이터베이스를 임의로 조작할 위험이 있다.

### 1.2. Bypass
인자 값에 대한 검증 절차가 존재하지 않으므로 우회 없이 쿼리 삽입이 가능하다. 


## 2. Medium

### 2.1. Summary
addslashes()함수를 이용하여 사용자가 입력한 값에서 홑따옴표('), 겹따옴표("), 백슬래시(\), NULL(NULL 바이트)가 있는 경우 백슬래스를 붙여서 반환합니다.

#### 참고
>[PHP Manual - addslashes](http://php.net/manual/kr/function.addslashes.php)  

```php
function sqli_check_1($data)
{

    return addslashes($data);

}
```

### 2.2. Bypass
필터링되는 특수문자 앞에 '%bf'를 입력하면 addslashes()에 의해서 붙는 백슬래시가 %bf와 연결되어 하나의 문자로 인식되고 백슬래시를 우회할 수 있다.


## 3. High

### 3.1. Summary
mysql_real_escape_string() 함수를 이용하여 사용자가 입력한 값에서  \x00, \n, \r, ', ", \x1a 가 존재하는 경우 백슬래시를 붙여서 반환합니다.

```php
function sqli_check_2($data)
{

    return mysql_real_escape_string($data);

}
```

### 3.2. Bypass
현재 우회를 위해 노력하고 있으나, 성공하지 못하였다. 우회를 위한 추가 테스트가 필요하다.

#### 참고 
>[Stackoverflow - SQL injection that gets around mysql_real_escape_string()](http://stackoverflow.com/questions/5741187/sql-injection-that-gets-around-mysql-real-escape-string)  
