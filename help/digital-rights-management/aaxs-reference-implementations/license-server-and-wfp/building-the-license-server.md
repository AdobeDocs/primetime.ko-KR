---
title: 라이선스 서버 구축
description: 라이선스 서버 구축
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 라이선스 서버 구축 {#building-the-license-server}

참조 구현 라이선스 서버에는 라이선스 서버를 배포하기 위한 WAR 파일이 포함되어 있습니다. 또한 모든 라이선스 서버 소스 코드와 Ant 빌드 스크립트(참조 Implementation\Server\refimpl\build-refimpl.xml)가 포함되어 있으므로 코드를 쉽게 변경할 수 있습니다.

>[!NOTE]
>
>이 단계는 소스 코드를 수정하려는 경우에만 필요합니다. 평가를 위해 이 단계를 건너뛰고 제공된 대로 WAR 파일을 사용할 수 있습니다.

Ant 스크립트를 실행하기 전에 스크립트를 수정하여 Adobe 액세스 SDK, Tomcat, MySQL 및 Log4J의 위치를 지정합니다. 텍스트 편집기에서 build-refimpl.xml을 열고 속성 값을 편집합니다 `sdkdir, tomcatdir, mysqldir, and log4jdir`. 소스 코드를 컴파일하고 참조 구현을 위한 WAR 파일을 만들려면 다음을 사용하여 스크립트를 실행합니다. `ant -f build-refimpl.xml all` Ant 스크립트가 포함된 디렉터리입니다. 스크립트가 완료되면 [!DNL refimpl-build/wars] 서버 WAR 파일이 포함된 디렉터리가 만들어집니다.
