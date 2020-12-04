---
description: 'null'
seo-description: 'null'
seo-title: 라이선스 서버가 제대로 시작되었는지 확인
title: 라이선스 서버가 제대로 시작되었는지 확인
uuid: a6a034c9-b3c4-4e26-b901-d2c132c00c52
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 라이선스 서버가 {#check-whether-the-license-server-started-properly} 제대로 시작되었는지 확인

참조 구현 라이센스 서버의 시작 여부를 확인하는 방법에는 여러 가지가 있습니다. 한 가지 방법은 [!DNL catalina.log] 로그를 확인하는 것이지만 라이센스 서버가 자체 로그 파일에 로그하기 때문에 충분하지 않을 수 있습니다.
1. [!DNL AdobeFlashAccess.log] 파일을 확인합니다.

   여기에서 참조 구현 라이센스 서버가 로그 정보를 기록합니다. 이 로그 파일의 위치는 [!DNL log4j.xml] 파일로 표시되므로 모든 위치를 가리키도록 수정할 수 있습니다. 기본적으로 로그 파일은 `catalina` Tomcat 스크립트를 실행하는 작업 디렉토리로 복사됩니다.
1. 다음 URL로 이동하여 &quot;라이센스 서버가 올바르게 설정됨&quot;이라는 텍스트가 표시되는지 확인합니다.
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
