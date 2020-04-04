---
layout: post
title:  "Make catalina.out by date"
categories: server
tags: tomcat, catalina, linux
author: mmmjj
description: 날짜별 카탈리나 생성
---

catalina.out 날짜별 생성을 위한 catalina.sh 수정

 목적: catalina.out의 크기가 점점 커져 로그 확인 어려움 해소를 위한 날짜 별 로그생성

 환경: linux의 tomcat 8.0대 설치버전, (tomcat 설치 시 rotatelogs 설치 됨. 위치확인 명령어: find / -name rotatelogs)

 Progress: catalina.sh에서 `touch "$CATALINA_OUT"` 검색 후 해당 쉘 내용 중 글쓴이 기준 461Line, 471Line의 ` >> "$CATALINA_OUT" 2>&1 "&"` 삭제 후 하단 테스트 스크립트 추가

	| /usr/local/tomcat/bin/rotatelogs "$CATALINA_OUT".%Y-%m-%d 86400 540 & 
	
* startup.sh 실행 시 log내용 출력됨.

![catalina_1]({{ site.baseurl }}/assets/images/catalina_1.png)


	"2>&1" \| /usr/local/tomcat/bin/rotatelogs $CATALINA_OUT.%Y-%m-%d.log 86400 540 &

* 2020.04.03 테스트 진행 중

![catalina_2]({{ site.baseurl }}/assets/images/catalina_2.png)


	2>&1 "&" | /usr/local/tomcat/bin/rotatelogs "$CATALINA_OUT"-%Y-%m-%d.log 86400 540 &

![catalina_3]({{ site.baseurl }}/assets/images/catalina_3.png)


	"2>&1" \| "$CATALINA_HOME"/bin/rotatelogs "'$CATALINA_OUT'.'%Y-%m-%d'.'log'" 86400 540 "&" # 540 for JST offset

![catalina_4]({{ site.baseurl }}/assets/images/catalina_4.png)

*result: 테스트 진행 중