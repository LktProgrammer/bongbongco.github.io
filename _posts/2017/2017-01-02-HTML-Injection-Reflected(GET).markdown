---
layout: post
title: HTML Injection - Reflected (GET)
categories: [bWAPP]
tags: [Pentest, bWAPP, BeeBox]
fullview: false
comments: true
published: true
---

bWAPP 을 이용한 웹 취약점 진단 학습. HTML Injection 취약점은 사용자의 입력 값을 검증 절차 없이 그대로 본문 내 포함하여 사용자에게 반환함으로써 발생하는 취약점이다. 이를 막기 위해서는 사용자에게서 전달 받은 인자 값에서 HTML 태그 혹은 자바스크립트에서 사용되는 특수문자가 존재하는 지 확인하는 절차를 추가해야 한다.

## 1. LOW

### 1.1. Summary
사용자에게 전달 받은 데이터를 그대로 본문 내 삽입하는 형태로 HTMl 구문 삽입 시 해당 구문이 동작하게 된다.

### 1.2. Bypass
인자 값에 대한 검증 절차가 존재하지 않으므로 우회 없이 코드 삽입이 가능하다. 


## 2. Medium

### 2.1. Summary
사용자에게 전달 받은 데이터 중에서 HTML 태그 작성 시 사용되는 '<', '>' 기호를 HTML 인코딩 처리하는 필터가 적용되어 있다. 

```php
function xss_check_1($data)

{

    // Converts only "<" and ">" to HTLM entities    
    $input = str_replace("<", "&lt;", $data);
    $input = str_replace(">", "&gt;", $input);

    // Failure is an option
    // Bypasses double encoding attacks   
    // <script>alert(0)</script>
    // %3Cscript%3Ealert%280%29%3C%2Fscript%3E
    // %253Cscript%253Ealert%25280%2529%253C%252Fscript%253E

    $input = urldecode($input);

    return $input;

}
```

### 2.2. Bypass
필터는 평문 '<', '>' 가 입력되었을 시에만 HTML 인코딩을 적용하고 있으며, 검증 완료 후 URL 디코딩을 수행하여 사용자에게 값을 반환하고 있다. 이를 이용하여 HTML 코드를 URL 인코딩하여 전달하면 성공적으로 코드를 삽입할 수 있다.

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

