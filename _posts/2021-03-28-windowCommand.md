---
layout: post
title:  "window 커맨드창에서 디렉토리 삭제하기"
categories: window
tags: window, cmd, command, ilnux, 명령어
author: mmmjj
description: fix not connected internet.
---

 목적:<br>
&nbsp;&nbsp;주말에 운영서버에 배포할 일이 있어 로컬에 백업을 하는데, 기존 백업본을(약120기가)삭제하는데 시간을 단축하고 싶다.

 환경: WINDOW 10 PRO
 
 Progress:  
 윈도우 키 + R -> 커맨드실행<br>
 폴더 및 하위 내용 모두삭제옵션추가( /s ) 명령어 사용
    ![stepTwo]({{ site.baseurl }}/assets/images/20210328/cmd.png){: width="60%" }
 <br>

 result : 휴지통에 남지 않고 모두삭제 됨( == SHIFT + DEL)
 
 <br>
 ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
          
   * 추가내용1 리눅스/윈도우 기본의기본명령어 비교
   
 |linux|WINDOW|
 |--|--|
 |ls|dir|
 |cd|cd|
 |clear|cls|
 |ifconfig|ipconfig|
 |rm|rmdir|
 |mkdir|mkdir|
 
 <br>
   * 추가내용2 리눅스 명령어 윈도우에서 사용하기
   
         doskey 나의명령어 = 윈도우명령어
         
  ![stepTwo]({{ site.baseurl }}/assets/images/20210328/cmd2.png){: width="100%" }