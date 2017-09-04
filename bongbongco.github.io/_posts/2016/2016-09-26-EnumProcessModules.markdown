---
layout: post
title: EnumProcessModules 기본 활용.
categories: [Development]
tags: [Development, Tip]
fullview: false
comments: true
published: true
---

'EnumProcessModules' 함수는 NtQueryInformationProcess를 이용하여 PEB에 InInitializationOrderModuleList 를 참조 후 LIST를 구해주고, 그외 잘 알려진 Tool인 ProcessExplorer나 Process Hacker같은 경우에는 PEB의 'InLoadOrderModuleList'에 직접 접근해서  DLL의 List를 뽑아 온다. 만약 DLL을 Hide 시킬 때   'InInitializationOrderModuleList '나 ''InLoadOrderModuleList' 중 어느 하나만 링크를 끊는 경우에는 다른 프로세스 관리 프로그램에서는 나타나는 문제가 있을수 있다.
