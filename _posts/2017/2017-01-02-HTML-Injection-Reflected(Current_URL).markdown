---
layout: post
title: HTML Injection Reflected (Current URL)
categories: [bWAPP]
tags: [Pentest, bWAPP, BeeBox]
fullview: false
comments: true
published: true
---

bWAPP 을 이용한 웹 취약점 진단 학습. HTML Injection 취약점은 사용자의 입력 값을 검증 절차 없이 그대로 본문 내 포함하여 사용자에게 반환함으로써 발생하는 취약점이다. 이를 막기 위해서는 사용자에게서 전달 받은 인자 값에서 HTML 태그 혹은 자바스크립트에서 사용되는 특수문자가 존재하는 지 확인하는 절차를 추가해야 한다. *부제인 Current URL 에서 확인할 수 있듯이, 사용자가 최근 요청했던 URL을 본문 내 포함하는 과정에서 미흡한 입력 값 검증으로 발생하는 취약점이다.*

## 1. LOW

### 1.1. Summary
사용자가 요청한 URL 값이 그대로 본문 내 포함되어 있다. 이로 인해 URL 에 임의의 인자를 추가하여 인자 값 내 HTML 구문을 삽입할 시 어플리케이션 무단 변경이 가능하다.

### 1.2. Bypass
인자 값에 대한 검증 절차가 존재하지 않으므로 우회 없이 코드 삽입이 가능하다. 


## 2. Medium

### 2.1. Summary
사용자에게 전달 받은 인자 값을 'document.URL()' 함수를 이용하여 본문 내 삽입하고 있다. 이로 인해 인자 값에 HTML 스크립트 구문을 삽입 시에도 URL 인코딩 되어 스크립트 구문이 동작하지 않는다.

```php
    case "1" :

        $url = "<script>document.write(document.URL)</script>";
        break;
```

### 2.2. Bypass
인자 값 삽입 시 '?' 기호 대신 '#' 기호를 사용하면 URL 인코딩 되지 않고 스크립트 구문을 본문 내 삽입할 수 있다.

#### 참고
>[DOM Based Cross-site Scripting Vulnerability](https://www.netsparker.com/blog/web-security/dom-based-cross-site-scripting-vulnerability/)  
>[DOM-based Cross-Site Scripting (XSS) Explained](http://www.acunetix.com/blog/articles/dom-xss-explained/)  


## 3. High

### 3.1. Summary
사용자에게 전달 받은 값을 htmlspecialchar() 함수를 이용하여 HTML 태그 입력 시 사용되는 특수 문자들을 HTML 인코딩하는 필터가 적용되어 있다.

```php
function xss_check_3($data, $encoding = "UTF-8")
{

    // htmlspecialchars - converts special characters to HTML entities    
    // '&' (ampersand) becomes '&amp;' 
    // '"' (double quote) becomes '&quot;' when ENT_NOQUOTES is not set
    // "'" (single quote) becomes '&#039;' (or &apos;) only when ENT_QUOTES is set
    // '<' (less than) becomes '&lt;'
    // '>' (greater than) becomes '&gt;'  

    return htmlspecialchars($data, ENT_QUOTES, $encoding);

}
```

### 3.2. Bypass
현재 우회를 위해 노력하고 있으나, 성공하지 못하였다. 인터넷 검색 시 쉽게 볼 수 있는 UTF-7 을 이용한 우회 방법이나, multi-byte를 이용한 (\xf0 ~ \xfc) 방법을 확인해보았으나 실패하였다. 우회를 위한 추가 테스트가 필요하다.
