---
seo-title: WAR 파일 배포
title: WAR 파일 배포
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# WAR 파일 배포{#deploy-the-war-files}

1. WAR 파일을 Tomcat의 [!DNL webapps] 디렉토리로 복사합니다.

   * 개인화 서버: [!DNL flashaccess.war]
   * 키 생성 서버: [!DNL flashaccess-kgs.war]

1. Adobe에서 제공한 패키지의 [!DNL ROOT] 폴더를 [!DNL webapps] 디렉토리로 복사합니다.

   Indification Server는 [!DNL crossdomain.xml] 파일을 호스트해야 합니다. ( [!DNL ROOT] 폴더에는 [!DNL crossdomain.xml] 파일이 들어 있습니다.모두 대문자로 [!DNL ROOT] 표시되어야 합니다.) 키 생성 서버에는 이 파일이 필요하지 않습니다.

