---
layout: post
title: SCOUTER APM 설치
date : 2017-08-01
---

## Scouter ?
***
![scouter.png]({{ site.baseurl }}/images/post/scouter.png)

Scouter 는 Pinpoint와 같은 APM 의 종류 중 하나로 Opensource 로 제작되었다.
* Github Scouter : [QuickStart github](https://github.com/scouter-project/scouter)
* QuickStart : [Scouter QuickStart](https://github.com/scouter-project/scouter/blob/master/scouter.document/main/Quick-Start.md)

Scouter는 윈도우에서도 빠른 시작이 가능하도록 Demo를 제공하고 있음
* Window Demo : [QuickStart Windows](https://github.com/naver/pinpoint/blob/master/quickstart/README.Win.ko.md)

## Installation
***
**설치전 환경셋팅**

JDK 7 이상 설치 하며 기본으로 환경변수에 JAVA_HOME 이 지정되어야 함  
<br/>


**Scouter 다운로드** 

빠른 실행이 가능한 Demo 를 제공하므로 이것을 [다운로드](https://github.com/scouter-project/scouter-demo/releases/download/v1.7.1/demo-env1.zip)  
<br/>


**Scouter Client 프로그램 다운로드**
* 각 운영체제에 맞는 클라이언트를 다운로드 받는다 윈도우에 설치할것이기 떄문에 당근 윈도우버전으로 [다운로드](https://github.com/scouter-project/scouter/releases/download/v1.7.1/scouter.client.product-win32.win32.x86_64.zip)  
<br/>

**Scouter 서버 실행**

Scouter 서버를 압축푼 디렉토리로 이동후에  실행
```
start-scouter-server.bat
```
<br/><br/>

**Scouter Client 실행**

아래는 클라이언트 접속정보의 기본값이다.
* Server Address : 127.0.0.1:6100
* ID : admin
* Password : admin  
<br/>

**JAVA Agent**

Scouter 는 Demo application 이 포함되어있어 star-tomcat.bat 을 실행하면 embedded tomcat 이 실행되면서
자동적으로 Scouter 에 모니터링된다. 다른 방법으로는 JAVA Agent 를 이용하여 현재 개발중이나 다른 어플리케이션 시작 옵션에 적용하여 모니터링 할 수 있다. Agent 옵션에는 Agent 경로와 환경설정 파일을 지정해주어야한다.
```
-javaagent:scouter\agent.java\scouter.agent.jar  
-Dscouter.config=scouter\agent.java\conf\scouter.conf  
```
<br/>

**NON-HTTP Servlet 추적**

보통의 APM 은 HTTP 호출로 들어오는 요청이 시작점이되어  모니터링을 시작하는데. Scouter 에서는 데몬이나 배치형식의 메소드 추적이 가능하다. 자세한 내용은 [이곳](https://github.com/scouter-project/scouter/blob/master/scouter.document/use-case/NON-HTTP-Servi ce-Trace.md)에 있다.  
필자는 이 환경정보에서 기본적으로 변경한 설정을 사용한다.
```
#scouter.conf  
hook_method_patterns=com.mypackage*.* ( mypackage 하위 모든 클래스를 모니터링에 포함 )  
trace_auto_service_enabled=true
```