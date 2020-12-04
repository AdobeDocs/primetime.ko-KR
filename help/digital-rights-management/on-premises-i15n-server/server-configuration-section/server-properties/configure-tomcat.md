---
seo-title: Tomcat 구성
title: Tomcat 구성
uuid: 5f23aa33-29d7-4b41-87a4-59dc5b433de4
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Tomcat{#configure-tomcat} 구성

개인화 서버에서 액세스 로그에 추가 정보를 포함하도록 Tomcat의 [!DNL conf/server.xml] 파일을 수정합니다. 이 정보를 보고용으로 사용할 수 있습니다.

1. [!DNL server.xml]에서 `AccessLogValve`에 대한 구성을 찾아 다음과 같이 패턴을 수정합니다.

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` 는  `x-forwarded-for` 헤더 값을 기록합니다. Tomcat 서버로 요청을 전달하는 데 Apache 역방향 프록시를 사용하는 경우 이 헤더에 원본 클라이언트의 IP 주소가 포함되지만 `%h`은 Apache 서버의 IP 주소를 기록합니다. `%{request-id}r` 는 개인화 응용 프로그램 로그에 포함된 요청 ID에 해당하는 요청 식별자를 기록합니다.

1. [!DNL conf/server.xml]을 편집하고 `unpackwars` 속성을 false로 설정합니다.

   개인화 및 키 생성 서버 모두의 경우 [!DNL conf/server.xml]을 편집하고 `unpackwars` 속성을 `false`로 설정하는 것이 좋습니다. 그렇지 않으면 WAR를 업데이트할 때 압축을 푼 WAR 폴더도 정리해야 할 수 있습니다.

>[!NOTE]
>
>향후 DRM 클라이언트는 Tomcat에 사용할 수 있는 CORS(Cross-Origin Resource Sharing) 필터를 활성화하고 구성해야 합니다. 현재 DRM 클라이언트는 이러한 요구 사항을 가지고 있지 않습니다.

