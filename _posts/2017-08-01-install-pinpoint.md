---
layout: post
title: NAVER PINPOINT 윈도우 설치
date : 2017-08-01
---

## Pinpoint ?
***
![pinpoint-tutorial.PNG]({{ site.baseurl }}/images/post/pinpoint-tutorial.PNG)

Pinpoint 는 네이버에서 개발한 APM Tool 이다.
* Github URL : [pinpoint github](https://github.com/naver/pinpoint)
* QuickStart : [QuickStart Windows](https://github.com/naver/pinpoint/blob/master/quickstart/README.Win.ko.md)

## Installation
***
**설치전 환경셋팅**

* JDK 6 이 설치되어야 할 것 ( 1.6.0_45 버전을 추천함)
* JDK 7 이 설치되어야 할 것 ( 1.7.0_80 버전을 추천함)
* JDK 8 이 설치되어야 할 것
* 설치된 JDK 가 아래와 같은 이름으로 JAVA_HOME 시스템 환경변수 등록이 되어 있어야 함 
* JDK 6 : JAVA_6_HOME ( JAVA 6 이 설치된 경로 )
* JDK 7 : JAVA_7_HOME ( JAVA 7 이 설치된 경로 )
* JDK 8 : JAVA_8_HOME ( JAVA 8 이 설치된 경로 )
* Apache Maven 3.3.x 버전이 설치되어야 함

**Pinpoint Stable 버전 다운로드** 

* 현재 기준으로 Stable 버전은 [1.6.2 release](https://github.com/naver/pinpoint/releases/tag/1.6.2)
* Clone 으로 소스를 내려받을경우에는 1.6.2 tag release 를 내려받거나 아니면 Source code Zip 을 내려받는다.
* Source Code 는 적당한 곳에 압축을 해제함 ( Pinpoint_Home )

**Hbase 설치**
* HBase 1.0.3 최상위 버전으로 다운르도 받는다.  [Apache Hbase Download](http://archive.apache.org/dist/hbase/)
* hbase 압축을 풀며 최종 위치가 [Pinpoint_Home\quickstart\hbase\hbase] 가 되어야 한다.

**Pinpoint 설치**
* mvn install -Dmaven.test.skip=true 명령어를 이용하여 Pinpoint 모듈을 설치하는데 간혹 환경설정의 영향을 받아 Maven 을 찾을 수 없다고 하면 아래와 같은 순서대로 진행한다.
* [pinpoint github](https://github.com/naver/pinpoint) master branch 에 있는 mvnw.cmd 파일과 .mvn/wrapper/ 에 있는 2개의 maven-wrapper 관련 파일을 다운로드 받아 Pinpoint_Home에 똑같은 위치에 적용시켜준다.
* 그후 다시 mvn instal -Dmaven.test.skip=true Go! 필요한 라이브러리를 다운로드 받기위해 빌드 속도가 많이 느릴 수 있다. 모듈이 정상적으로 패키징되면 Pinpoint 의 설치는 끝이라 볼 수 있다.

**HBase 시작 및 테이블 초기화**
* Pinpoint_Home\quickstart\bin\start-hbase.cmd (hbase 시작)
* start-hbase를 시작하면 cmd 창에서 스크립트 파일을 복사할것이냐는 문구가 나오는데 YES 하고 진행하면 경로를 못찾는 문제가 간혹있다. 그럴경우에는 Pinpoint_Home\quickstart\hbase\hbase\bin\start-hbase.cmd 파일을 실행 할것.
* Pinpoint_Home\quickstart\bin\init-base.cmd (테이블 초기화)

**Pinpoint 데몬 시작**

Pinpoint 는 Collector (수집), Web UI (모니터링 웹화면), Test Application 기본 구성되어있다.
* Collector :  Pinpoint_Home\quickstart\bin\start-collector.cmd
* TestApp : Pinpoint_Home\quickstart\bin\start-testapp.cmd
* WEB : Pinpoint_Home\quickstart\bin\start-web.cmd

**결과확인

정상적으로 실행중인 데몬은 Hbase 를 포함한 3개의 Pinpoint 데몬이여야 한다.

* Web : http://localhost:28080
* TESTAPP : http://localhost:28081

## JAVA Agent 실행
***
APM을 이용한 성능 테스트는 개발환경에서도 가능 하다. Pinpoint 설치과정에서 각 모듈별 패키징된 파일이 있을 것이다. 그중에서 java agent 도 있으며 java 를 실행할때 vm argument 로 지정해서 어플리케이션을 실행하면 Pinpoint 가 동작한다.

* Java Agent 경로 : Pinpoint_Home\agent\target\pinpoint-agent-1.6.2\pinpoint-bootstrap-1.6.2.jar

Java Agent 를 실행할때 필요한 Vm argument는 아래와 같다
* -javaagent:Pinpoint_Home\agent\target\pinpoint-agent-1.6.2\pinpoint-bootstrap-1.6.2.jar
* -Dpinpoint.agentId=TESTAPP1 (에이전트 ID : 고유한 값이여야 한다.) 
* -Dpinpoint.applicationName=TESTAPP_WEB ( 웹에 보여줄 Application 이름 )
