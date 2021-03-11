---
title: WAR 파일 배포
description: WAR 파일 배포
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# WAR 파일 배포{#deploy-the-war-files}

1. WAR 파일을 Tomcat의 [!DNL webapps] 디렉토리로 복사합니다.

   * 개인화 서버:[!DNL flashaccess.war]
   * 키 생성 서버:[!DNL flashaccess-kgs.war]

1. Adobe에서 제공하는 패키지의 [!DNL ROOT] 폴더를 [!DNL webapps] 디렉토리로 복사합니다.

   개인화 서버도 [!DNL crossdomain.xml] 파일을 호스팅해야 합니다. ([!DNL ROOT] 폴더에는 [!DNL crossdomain.xml] 파일이 포함되어 있습니다.[!DNL ROOT]은(는) 모두 대문자로 되어 있어야 합니다.) 키 생성 서버는 이 파일을 필요로 하지 않습니다.

