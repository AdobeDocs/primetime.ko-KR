---
title: 라이선스 서버 및 감시 폴더 패키지 배포 개요
description: 라이선스 서버 및 감시 폴더 패키지 배포 개요
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 라이선스 서버 배포 및 감시 폴더 패키지 개요 {#deploying-the-license-server-and-watched-folder-packager-overview}

라이센스 서버 WAR 파일을 Tomcat의 [!DNL webapps] 디렉토리로 복사합니다. 이전에 WAR 파일을 배포한 경우 Tomcat의 [!DNL webapps] 디렉토리에서 압축되지 않은 WAR 디렉토리( [!DNL flashaccess], [!DNL edcws] 및 [!DNL flashaccess-packager])를 수동으로 삭제해야 할 수 있습니다. Tomcat이 WAR 파일의 압축을 해제하지 않도록 하려면 Tomcat의 conf 디렉토리에서 [!DNL server.xml] 파일을 편집하고 `unpackWARs` 속성을 `false`로 설정합니다.

속성 파일( [!DNL flashaccess-refimpl.properties])은 서버가 속성을 로드하려면 클래스 경로에 있어야 합니다. 이 파일을 디렉토리에 복사하고 적절한 값으로 파일을 업데이트합니다. Tomcat의 [!DNL conf] 디렉토리에서 [!DNL catalina.properties] 파일을 편집하고 [!DNL flashaccess-refimpl.properties]가 포함된 디렉토리를 `shared.loader` 속성에 추가합니다. 로깅을 구성하기 위한 [!DNL log4j.xml] 파일도 클래스 경로에 있어야 합니다(예를 보려면 [!DNL resources\log4j.xml] 참조).

참조 구현 서버는 여러 인증서 파일, 정책 파일 및 기타 리소스를 사용합니다. 이러한 파일은 모두 하나의 리소스 폴더에 있습니다. 기본적으로 리소스 폴더는 [!DNL C:\flashaccess-server-resources]이지만 이 위치는 [!DNL flashaccess-refimpl.properties]에서 수정할 수 있습니다. 서버를 시작하기 전에 필요한 모든 리소스를 이 위치에 복사하십시오.

Tomcat 및 라이센스 서버를 시작하려면 Tomcat의 [!DNL bin] 디렉토리에서 `catalina.bat start`을(를) 실행하십시오.
