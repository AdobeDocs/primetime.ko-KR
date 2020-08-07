---
seo-title: 안전한 스트리밍을 위한 Adobe Primetime DRM 서버 배포
title: 안전한 스트리밍을 위한 Adobe Primetime DRM 서버 배포
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 안전한 스트리밍을 위한 Adobe Primetime DRM 서버 배포{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

보호 스트리밍을 위한 Adobe Primetime DRM 서버를 배포하려면 요구 사항 항목에 나와 있는 대로 Java 및 Tomcat 버전을 설치해야 합니다.

보호된 스트리밍을 위한 Primetime DRM Server 패키지에 포함되어 있습니다 [!DNL flashaccesserver.war]. 다음의 경우

* 이 WAR 파일을 배포하려면 Tomcat의 [!DNL webapps] 디렉토리에 복사해야 합니다.
* 이전에 WAR 파일을 배포했다면 압축을 푼 WAR 디렉토리(Tomcat의 디렉토리 [!DNL flashaccessserver] 에서)를 삭제해야 할 수 [!DNL webapps] 있습니다.

* Tomcat이 WAR 파일의 압축을 풀지 않도록 하려면 Tomcat의 [!DNL server.xml] 디렉토리에서 [!DNL conf] 파일을 편집하고 `unpackWARs` 속성을 로 설정하여 구성합니다 `false`.

>[!NOTE]
>
>Tomcat이 시스템 클래스 경로 [!DNL commons-logging.jar] (보호된 스트리밍을 위한 Primetime DRM Server에 필요 없음)에 포함되도록 구성한 경우 Log4J를 사용하도록 commons-logging을 구성해야 합니다.

선택적으로 서버에서는 최적의 성능을 위해 플랫폼 전용 라이브러리(Microsoft Windows [!DNL jsafe.dll] 또는 Linux [!DNL libjsafe.so] 에서)를 사용합니다. 플랫폼에 적합한 라이브러리를 [!DNL thirdparty/cryptoj/]*플랫폼&#x200B;*에서`PATH`환경 변수 또는 Linux에서 지정한 위치로 복사할 수`LD_LIBRARY_PATH`있습니다.

>[!NOTE]
>
>64비트 버전은 운영 체제와 JDK 모두 64비트를 지원하는 경우에만 사용해야 합니다. 그렇지 않은 경우 32비트 버전을 사용해야 합니다.

