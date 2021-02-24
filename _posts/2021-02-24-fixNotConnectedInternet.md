---
layout: post
title:  "window7 인터넷 연결안됨 (진단 정책 서비스가 실행되고 있지 않습니다)"
categories: window
tags: window, window7, Diagnostic Policy Service
author: mmmjj
description: fix not connected internet.
---

 목적:<br>
&nbsp;&nbsp;타팀에서 오전회의 끝나고 특정피시 하나가 인터넷이 안된다며 요청이 들어와서
 컴퓨터기사로서 출동... <br>인터넷연결문제를 해결하자!<br>

 환경: window7 pro
 
 Progress:  
1. 포트 꽂혀있는지 확인.


    내근직은 데스크탑을 이용해 딱히 건들이지 않았어도 빠져있을수있으니 확인!
<br><br><br>
2. 컴퓨터 복구.

    모든사용자가 백업을 항상해두진 않지만... 업데이트 직후라면 업데이트 이전으로 돌리는 방법을 하면 된다.!
    ![stepTwo]({{ site.baseurl }}/assets/images/20210224/restore.jpg){: width="60%" }
 <br><br><br>
3. ipconfig로 현재 ip확인 후 대처


    ip주소가 192.168....이아니라 169.254....으로 되어있다면 ip주소가 할당이 안된것.
        이 경우에 문제해결 또는 ip할당을 요청한다.
    cmd 창에서 
        
        ipconfig /release
        ipconfig /renew
        
4. 3번도 했지만 안된다면.. 고정ip를 설정해본다. ip 설정에 앞서 다른 pc가있다면 
ping으로 빈 ip를 먼저 확인하면 좋다.

    ![staticIP]({{ site.baseurl }}/assets/images/20210224/staticIP.png){: width="80%" }
<br><br><br>
5. 위 방법까지 했는데도 안되고.. 문제해결을 통해 나온 [진단 정책 서비스가 실행되고 있지 않습니다] 해결하기
    ![staticIP]({{ site.baseurl }}/assets/images/20210224/dps1.png){: width="60%" }    [사진출처][link1]
<br>microsoft 공식 홈 답변 ([출처][link2])

        작업 방법 1. 진단 정책 서비스 시작
        [제어판-관리 도구-서비스]에서 Diagnostic Policy Service 의 유형이 "자동" 상태가 "시작 됨"으로 되어 있는지 확인 합니다.
        만약 서비스가 시작되지 않고 오류가 발생 된다면 응답해 주시기 바랍니다.

    그런데 Diagnostic Policy Service가 시작이 안된다.....<br>
    그래서 또 한번 검색 하여 ([출처][link3])<br>
    
        Widnows 7 사용 중 Diagnostic Policy Service (진단 정책 서비스)가 정상적으로 시작되지 않는 문제로 문의를 주셨습니다.
        문의주신 내용의 경우, 아래의 작업 방법을 참고하여 점검을 진행해보시기 바랍니다.
        [작업 방법]1.시작 - 프로그램 및 파일 검색 창에서cmd 입력 후 검색이 되면 검색된 cmd.exe에 마우스 오른쪽 클릭하여 관리자 계정으로 실행을 클릭합니다.
        2.사용자 계정 컨트롤 메시지가 나타나면 관리자암호를 입력하거나 또는 예를 클릭합니다.
        3.명령 프롬프트 창이 나타나면 아래와 같이 입력하고 Enter 합니다.
        (한줄씩 입력하고 Enter 합니다.)
            net localgroup Administrators /add networkservice
            net localgroup Administrators /add localservice
        4.완료 메시지가 나타나면 PC 를 재시작하여 증상을 확인합니다.

 result : 전원부터물리적->논리적->세부적으로 다가가기, 윈도우7 말고 10사용하기...
 
[link1]:https://answers.microsoft.com/ko-kr/windows/forum/all/%EC%A7%84%EB%8B%A8-%EC%A0%95%EC%B1%85/8b2d8e9f-fcb1-4a3c-8f6f-25b7cc236395
[link2]:https://answers.microsoft.com/ko-kr/ie/forum/ie10-windows_7/%EC%A7%84%EB%8B%A8%EC%A0%95%EC%B1%85%EC%84%9C/cdb6d324-5c02-43b0-8f03-512509d91772
[link3]:https://answers.microsoft.com/ko-kr/ie/forum/ie11-windows_7/%EC%A7%84%EB%8B%A8-%EC%A0%95%EC%B1%85/d3a9744b-81ca-4e6c-9400-05a6c7b67105