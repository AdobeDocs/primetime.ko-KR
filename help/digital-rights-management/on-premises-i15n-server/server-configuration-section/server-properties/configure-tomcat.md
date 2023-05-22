---
title: Tomcat 구성
description: Tomcat 구성
copied-description: true
exl-id: 766b66dd-6070-4b0d-a860-a426fca05e56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Tomcat 구성{#configure-tomcat}

개별화 서버에서 Tomcat의 [!DNL conf/server.xml] 액세스 로그에 추가 정보를 포함할 파일입니다. 이 정보는 보고 목적으로 사용할 수 있습니다.

1. 에 대한 구성을 찾습니다. `AccessLogValve` 위치: [!DNL server.xml] 패턴을 다음과 같이 수정합니다.

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` 의 값을 기록합니다. `x-forwarded-for` 머리글입니다. Apache 역방향 프록시를 사용하여 Tomcat 서버에 요청을 전달하는 경우 이 헤더에는 원래 클라이언트의 IP 주소가 포함되지만, `%h` apache 서버의 IP 주소를 기록합니다. `%{request-id}r` 은 개별화 애플리케이션 로그에 포함된 요청 ID에 해당하는 요청 식별자를 기록합니다.

1. 편집 [!DNL conf/server.xml] 및 설정 `unpackwars` 속성을 false로 설정합니다.

   개별화 및 키 생성 서버 모두의 경우 편집하는 것이 좋습니다 [!DNL conf/server.xml] 및 설정 `unpackwars` 다음으로 속성: `false`. 그렇지 않으면 WAR을 업데이트할 때 압축을 푼 WAR 폴더도 정리해야 할 수 있습니다.

>[!NOTE]
>
>향후 DRM 클라이언트에서는 Tomcat에서 사용할 수 있는 CORS(원본 간 리소스 공유) 필터를 활성화하고 구성해야 합니다. 현재 DRM 클라이언트에는 이 요구 사항이 없습니다.
