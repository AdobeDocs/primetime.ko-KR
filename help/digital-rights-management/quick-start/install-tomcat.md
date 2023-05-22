---
title: Tomcat 설치
description: Tomcat 설치
copied-description: true
exl-id: aed8fc1c-0d75-47ca-bbd4-c0934a66e284
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Tomcat 설치 {#install-tomcat}

두 서버 모두에 Tomcat을 설치해야 합니다.
1. 에서 Tomcat 설치 [!DNL \Third Party\Tomcat\6.0.18\] 설치 DVD의 디렉토리.

   >[!NOTE]
   >
   >경로에 공백이 없는 위치에 Tomcat이 설치되었는지 확인합니다. 다음을 입력할 수 있습니다. `C:\Program Files\Tomcat`, 그러나 아님 `C:\Tomcat\`.

1. Tomcat을 시작하려면 을 입력합니다. `TomcatInstallDir>\bin\catalina.bat run`.
1. 설치를 확인하려면 다음을 입력하여 Tomcat 랜딩 페이지로 이동합니다. `https://<Hostname>:8080/`.
1. 만들기 `crossdomain.xml` 파일을 만든 다음 `<TomcatInstallDir>\webapps\ROOT\` 디렉토리.

   에서 파일을 복사할 수도 있습니다. `https://drmtest2.adobe.com/crossdomain.xml` 디렉토리.
