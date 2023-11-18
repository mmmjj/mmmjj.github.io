---
layout: post
title:  "docker 사용하기"
date:   2023-11-18 16:58:00 +0000
categories: msa
tags: docker, msa
author: mmmjj
description: docker 다운로드, 사용하기
---

#### 목적
* 2023.11.08    : docker desktop 로컬에 설치하고 도커이미지를 실행시켜보자
<br><br>

#### 환경
* os: window10
* docker: Docker Desktop Installer.exe(4.25.1)
* ubuntu image: ubuntu:16.04
* mariadb image: mysql:5.7
<br><br>

#### Progress
<br>

##### 1. os에 맞는 인스톨러 다운로드 
<br>

- https://www.docker.com/products/docker-desktop/


![downloadDocker]({{ site.baseurl }}/assets/images/20231118/downloadDocker.png){: width="100%" }

<br><br>
- 1-1. 첫번째 에러

```
error: request returned internal server error for api route and version http://%2f%2f.%2fpipe%2fdocker_engine/v1.24/info,
 check if the server supports the requested api version errors pretty printing info
```
<br>
[에러 참고사이트](https://github.com/docker/for-mac/issues/6956) (_이것저것했는데 안됨..._)

<br><br>

- 1-2. 두번째 에러(첫번째 에러때 재부팅을 많이하다보니.. 다르게 뜬 에러)
<br>
![secondError]({{ site.baseurl }}/assets/images/20231118/secondError.png){: width="80%" }

<br>

- 솔루션
<br>
![secondResolve]({{ site.baseurl }}/assets/images/20231118/secondResolve.png){: width="80%" }

```
파워쉘 관리자모드로 실행

Enable-WindowsOptionalFeature -Online -FeatureName $("Microsoft-Hyper-V","Containers") -All
```

<br>
- docker info cli, docker desktop
![firstDockerExecution]({{ site.baseurl }}/assets/images/20231118/firstDockerExecution.png){: width="100%" }



<br><br><br>

##### 2. 도커 이미지 다운받기,  docker pull image

<br>

- ubuntu:16.04 이미지 pull받기

```
docker pull ubuntu:16.04
```

<br><br>
- 2-1. 첫번째 에러...._(제목을 에러모음집으로 바꿀까..)_

```
C:\Users\owner>docker pull ubuntu:16.04
16.04: Pulling from library/ubuntu
no matching manifest for windows/amd64 10.0.19045 in the manifest list entries
C:\Users\owner>
```

<br>
- 시도1 엔진 설정내용을 true로 바꾸었다 <br><br>
  ![firstImageErr]({{ site.baseurl }}/assets/images/20231118/firstImageErr.png){: width="100%" }

_안됨_

<br><br>
- 솔루션  시스템트레이에서 linux 컨테이너를 사용하도록 변경<br><br>
  ![firstImageErrResolve]({{ site.baseurl }}/assets/images/20231118/firstImageErrResolve.png)<br>

  ![firstImageErrResolveCmd]({{ site.baseurl }}/assets/images/20231118/firstImageErrResolveCmd.png){: width="100%" }


<br><br><br>
##### 3. mysql 이미지 다운받기
<br>
- 사용한 명령어

```
docker run -d -p 13306:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=true --name mysql mysql:5.7
```
1. -p 13306:3306 ==> 호스트pc의 13306포트를 컨테이너의 3306번 포트포워딩 <br>
2. -e MYSQL_ALLOW_EMPTY_PASSWORD ==> root 패스워드 없애기옵션<br>
3. --name mysql ==> mysql 컨테이너 이름설정<br>
4. mysql:5.7 ==> 버전지정<br>

<br>
- 확인 (docker ps -a)

```
C:\WINDOWS\system32>docker ps -a
CONTAINER ID   IMAGE       COMMAND                   CREATED         STATUS         PORTS                                NAMES
f992f8a15c90   mysql:5.7   "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   33060/tcp, 0.0.0.0:13306->3306/tcp   mysql
```

<br><br><br>
##### 4. docker 커맨드
<br>
- 사용한 명령어

```
컨테이너 확인
docker container ls
docker ps

종료된 컨테이너도 확인
docker container ls -a
docker ps -a

종료된컨테이너 또는 컨테이너 삭제
docker container rm 컨테이너id

윈도우 도커 이미지 목록 특정 문자열찾기
docker images | findstr 16.04

리눅스버전은
docker images | grep16.04

이미지다운받기
docker pull ubuntu:16.04

pull + create + start
docker run ubuntu:16.04
```


<br><br><br>
##### result : 

- docker desktop 화면 (ubuntu의 경우 추가 스크립트가 없어서 바로 꺼진다)

![containerList]({{ site.baseurl }}/assets/images/20231118/containerList.png){: width="100%" }



