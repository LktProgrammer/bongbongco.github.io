---
layout: post
title: 안드로이드 USIM.
---

Android API를 이용하여 얻을 수 있는 USIM 데이터 정보는 USIM serial number와 USIM state가 있습니다.

1. USIM serial number
 USIM serial number는 19자리로 구성되어 있으며 4가지 정보를 지니고 있습니다.
예) 89 82 05 1200 00 320451 0

+ 통신사 ID(2자리)
+ 국가 코드(2자리)
+ 네트워크 코드(2자리)
+ USIM 번호(13자리)

2. USIM state

+ SIM_STATE_ABSENT : SIM 카드가 더이상 장치에서 사용할 수 없습니다.
+ SIM_STATE_NETWORK_LOCKED : 잠금해제를 위해 네트워크 PIN이 필요합니다.
+ SIM_STATE_PIN_REQUIRED : 잠금해제를 위해 SIM PIN이 필요합니다.
+ SIM_STATE_PUK_REQUIRED : 잠금해제를 위해 SIM PUK가 필요합니다.
+ SIM_STATE_READY : 준비상태
+ SIM_STATE_UNKNOWN : 알수없음 상태

~~~
활용 코드 예제
//TelephonyManager 객체를 얻기 위해서는 Context 객체에서 제공하는 getSystemService() 메서드를 이용한다.
TelephonyManager tm = (TelephonyManager) getSystemService(TELEPHONY_SERVICE);

//SIM카드 Serial Number 조회
Log.d("PHONE", "getSimSerialNumber :" + tm.getSimSerialNumber());

//SIM카드 상태 조회 SIM_STATE_UNKNOWN/SIM_STATE_ABSENT/SIM_STATE_PIN_REQUIRED/SIM_STATE_PUK_REQUIRED/
//SIM_STATE_NETWORK_LOCKED/SIM_STATE_READY 등의 값을 반환
Log.d("PHONE", "getSimState :" + tm.getSimState());
~~~