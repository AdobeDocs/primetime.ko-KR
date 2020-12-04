---
seo-title: Tomcat 설치
title: Tomcat 설치
uuid: f7663eda-ad18-4a6e-bb9f-01c74721b047
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Tomcat {#install-tomcat} 설치

두 서버 모두에 Tomcat을 설치해야 합니다.
1. 설치 DVD의 [!DNL \Third Party\Tomcat\6.0.18\] 디렉토리에서 Tomcat을 설치합니다.

   >[!NOTE]
   >
   >경로에 공백이 없는 위치에 Tomcat이 설치되어 있는지 확인합니다. `C:\Program Files\Tomcat`을 입력할 수 있지만 `C:\Tomcat\`은 입력할 수 없습니다.

1. Tomcat을 시작하려면 `TomcatInstallDir>\bin\catalina.bat run`을 입력합니다.
1. 설치를 확인하려면 `https://<Hostname>:8080/`을 입력하여 Tomcat 랜딩 페이지로 이동합니다.
1. `crossdomain.xml` 파일을 만들고 `<TomcatInstallDir>\webapps\ROOT\` 디렉터리에 저장합니다.

   `https://drmtest2.adobe.com/crossdomain.xml` 디렉토리에서 파일을 복사할 수도 있습니다.
