---
seo-title: Tomcat 설치
title: Tomcat 설치
uuid: f7663eda-ad18-4a6e-bb9f-01c74721b047
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Tomcat 설치 {#install-tomcat}

두 서버 모두에 Tomcat을 설치해야 합니다.
1. 설치 DVD의 [!DNL \Third Party\Tomcat\6.0.18\] 디렉토리에서 Tomcat을 설치합니다.

   >[!NOTE]
   >
   >경로에 공백이 없는 위치에 Tomcat이 설치되어 있는지 확인합니다. 입장할 수 `C:\Program Files\Tomcat`있지만 들어갈 수는 없습니다 `C:\Tomcat\`.

1. Tomcat을 시작하려면 Enter 키를 `TomcatInstallDir>\bin\catalina.bat run`입력합니다.
1. 설치를 확인하려면 를 입력하여 Tomcat 랜딩 페이지로 이동합니다 `https://<Hostname>:8080/`.
1. 파일을 `crossdomain.xml` 만들어 `<TomcatInstallDir>\webapps\ROOT\` 디렉토리에 배치합니다.

   또한 `https://drmtest2.adobe.com/crossdomain.xml` 디렉토리에서 파일을 복사할 수도 있습니다.
