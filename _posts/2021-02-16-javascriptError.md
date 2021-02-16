---
layout: post
title:  "Uncaught TypeError:.... 스크립트 문제해결"
categories: web view
tags: web, html, jsp, javascrirpt, funciton, overlap
author: mmmjj
description: javascript, function, html
---

 목적:<br>
&nbsp;&nbsp;기존 소스 수정작업하면서 종종 생기던 문제...<br>
    함수 호출이 안된다!!!!!

* 고쳐 볼 소스
![DebTools_1]({{ site.baseurl }}/assets/images/20200216/Image_1.png)
 
 환경: tomcat, spring framework, jsp, javascript, jstl, expression Language...
 
 Progress: 
 
 
* 평소 즐기는 문법(직관적이라 넘넘 맘에 든다.♥)
      
    $("#id").click(function(){
        console.log("hi");
    });
 
 
 * 구글링 시작
 ![search_1]({{ site.baseurl }}/assets/images/20200216/Image_2.png)

구글링 하다 보면 알고있는 내용들이 나온다.<br>
jquery cdn 선언 위치 조정, 캐싱문제, 오타, 포스트 작성중인 html 렌더링순서로 인한...<br>

하지만 그중에서 함수명과 태그아이디의 중복이 되면 안되다는 내용이 있어서...<br>
is not a function 도 신경쓰이고...<br>
해당요소의 id와 상이한 function 명을 지정해주었더니 바로 실행되었다..<br>

![DevTools_2]({{ site.baseurl }}/assets/images/20200216/Image_3.png)
![DevTools_3]({{ site.baseurl }}/assets/images/20200216/Image_4.png)


 result : 기존 소스를 수정하는데 상위버전의 스크립트로 인해 발생 된것으로.<br>
          같은 요소가 아니더라도 고유이름을 중복시키지 말자....