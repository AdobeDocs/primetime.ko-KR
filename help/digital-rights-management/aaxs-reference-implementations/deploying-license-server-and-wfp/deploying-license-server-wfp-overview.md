---
seo-title: 라이선스 서버 및 감시 폴더 패키지 배포 개요
title: 라이선스 서버 및 감시 폴더 패키지 배포 개요
uuid: 4b71f2f4-f971-4382-ae41-171f7dfdfe21
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 라이선스 서버 및 감시 폴더 패키지 배포 개요 {#deploying-the-license-server-and-watched-folder-packager-overview}

라이센스 서버 WAR 파일을 Tomcat의 [!DNL webapps] 디렉토리로 복사합니다. 이전에 WAR 파일을 배포한 경우 압축을 푼 WAR 디렉토리( [!DNL flashaccess], [!DNL edcws]및 [!DNL flashaccess-packager] Tomcat의 [!DNL webapps] 디렉토리)를 수동으로 삭제해야 할 수 있습니다. Tomcat이 WAR 파일의 압축을 풀지 않도록 하려면 Tomcat의 conf 디렉토리에서 [!DNL server.xml] 파일을 편집하고 `unpackWARs` 속성을 로 `false`설정합니다.

속성 파일( [!DNL flashaccess-refimpl.properties])은 서버가 속성을 로드하려면 클래스 경로에 있어야 합니다. 이 파일을 디렉토리에 복사하고 적절한 값으로 파일을 업데이트합니다. Tomcat의 [!DNL catalina.properties] 디렉토리에서 파일을 편집하고 [!DNL conf] [!DNL flashaccess-refimpl.properties] `shared.loader` 속성이 포함된 디렉토리를 추가합니다. 로깅을 구성하는 [!DNL log4j.xml] 파일도 클래스 경로에 있어야 합니다(예 [!DNL resources\log4j.xml] 참조).

참조 구현 서버는 여러 인증서 파일, 정책 파일 및 기타 리소스를 사용합니다. 이러한 파일은 모두 하나의 리소스 폴더에 있습니다. 기본적으로 리소스 폴더는 [!DNL C:\flashaccess-server-resources]있지만 이 위치는 에서 수정할 수 있습니다 [!DNL flashaccess-refimpl.properties]. 서버를 시작하기 전에 필요한 모든 리소스를 이 위치에 복사해야 합니다.

Tomcat 및 라이센스 서버를 시작하려면 Tomcat `catalina.bat start` 의 [!DNL bin] 디렉토리에서 실행하십시오.
