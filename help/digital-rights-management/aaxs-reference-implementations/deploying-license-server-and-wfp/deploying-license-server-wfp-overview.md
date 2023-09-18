---
title: 라이선스 서버 및 감시 폴더 패키지 배포 개요
description: 라이선스 서버 및 감시 폴더 패키지 배포 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 라이선스 서버 및 감시 폴더 패키지 배포 개요 {#deploying-the-license-server-and-watched-folder-packager-overview}

Tomcat에 라이센스 서버 WAR 파일 복사 [!DNL webapps] 디렉토리. 이전에 WAR 파일을 배포한 경우 압축을 푼 WAR 디렉토리를 수동으로 삭제해야 할 수 있습니다( [!DNL flashaccess], [!DNL edcws], 및 [!DNL flashaccess-packager] 톰캣 [!DNL webapps] directory). Tomcat이 WAR 파일의 압축을 푸는 것을 방지하려면 [!DNL server.xml] tomcat의 conf 디렉토리에 있는 파일을 설정하고 `unpackWARs` 특성 대상 `false`.

속성 파일( [!DNL flashaccess-refimpl.properties])는 서버에서 속성을 로드하기 위해 클래스 경로에 있어야 합니다. 이 파일을 디렉토리에 복사하고 적절한 값으로 파일을 업데이트합니다. 편집 [!DNL catalina.properties] Tomcat의 파일 [!DNL conf] 디렉터리 및 다음 디렉터리가 포함된 디렉터리 추가 [!DNL flashaccess-refimpl.properties] (으)로 `shared.loader` 속성. 다음 [!DNL log4j.xml] 로깅 구성을 위한 파일도 클래스 경로에 있어야 합니다(참조). [!DNL resources\log4j.xml] 예를 들어).

참조 구현 서버는 여러 인증서 파일, 정책 파일 및 기타 리소스를 사용합니다. 이러한 파일은 모두 하나의 리소스 폴더에 있습니다. 기본적으로 리소스 폴더는 [!DNL C:\flashaccess-server-resources], 그러나 이 위치는에서 수정할 수 있습니다. [!DNL flashaccess-refimpl.properties]. 서버를 시작하기 전에 필요한 모든 리소스를 이 위치에 복사해야 합니다.

Tomcat 및 라이센스 서버를 시작하려면 다음을 실행합니다. `catalina.bat start` Tomcat에서 [!DNL bin] 디렉토리.
