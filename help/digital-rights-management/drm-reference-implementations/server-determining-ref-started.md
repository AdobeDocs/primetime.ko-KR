---
title: 라이선스 서버가 제대로 시작되었는지 확인
description: 라이선스 서버가 제대로 시작되었는지 확인
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# 라이선스 서버가 제대로 시작되었는지 확인 {#check-whether-the-license-server-started-properly}

참조 구현 라이선스 서버가 올바르게 시작되었는지 여부를 확인하는 방법에는 몇 가지가 있습니다. 한 가지 방법은 [!DNL catalina.log] 하지만 라이선스 서버가 자체 로그 파일에 로깅하므로 이 작업으로는 충분하지 않을 수 있습니다.
1. 다음을 확인: [!DNL AdobeFlashAccess.log] 파일.

   여기서 참조 구현 라이선스 서버가 로그 정보를 기록합니다. 이 로그 파일의 위치는 [!DNL log4j.xml] 모든 위치를 가리키도록 파일을 수정할 수 있습니다. 기본적으로 로그 파일은 를 실행하는 작업 디렉터리에 복사됩니다 `catalina` Tomcat 스크립트.
1. 다음 URL로 이동하여 &quot;License Server가 올바르게 설정되었는지&quot;라는 텍스트가 표시되는지 확인합니다.
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
