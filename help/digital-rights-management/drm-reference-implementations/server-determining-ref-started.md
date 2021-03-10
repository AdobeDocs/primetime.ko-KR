---
title: 라이선스 서버가 제대로 시작되었는지 확인
description: 라이선스 서버가 제대로 시작되었는지 확인
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# 라이선스 서버가 {#check-whether-the-license-server-started-properly} 제대로 시작되었는지 확인

참조 구현 라이센스 서버가 올바르게 시작되었는지 확인하는 방법에는 여러 가지가 있습니다. 한 가지 방법은 [!DNL catalina.log] 로그를 확인하는 것입니다. 그러나 라이센스 서버가 자체 로그 파일에 기록되므로 충분하지 않을 수 있습니다.
1. [!DNL AdobeFlashAccess.log] 파일을 확인합니다.

   여기에서 참조 구현 라이센스 서버가 로그 정보를 기록합니다. 이 로그 파일의 위치는 [!DNL log4j.xml] 파일로 표시되므로 원하는 위치를 가리키도록 수정할 수 있습니다. 기본적으로 로그 파일은 `catalina` Tomcat 스크립트를 실행하는 작업 디렉토리에 복사됩니다.
1. 다음 URL로 이동하여 &quot;라이센스 서버가 올바르게 설정됨&quot;이라는 텍스트가 표시되는지 확인합니다.
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
