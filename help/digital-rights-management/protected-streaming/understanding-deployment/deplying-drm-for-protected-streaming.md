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


# 보호된 스트리밍을 위한 Adobe Primetime DRM 서버 배포{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

보호 스트리밍을 위한 Adobe Primetime DRM 서버를 배포하려면 요구 사항 항목에 나와 있는 대로 Java 및 Tomcat 버전을 설치해야 합니다.

보호된 스트리밍을 위한 Primetime DRM Server 패키지에는 [!DNL flashaccesserver.war]이 포함됩니다. 다음의 경우

* 이 WAR 파일을 배포하려면 Tomcat의 [!DNL webapps] 디렉토리로 복사해야 합니다.
* 이전에 WAR 파일을 배포했다면 압축을 푼 WAR 디렉터리( [!DNL flashaccessserver] Tomcat의 [!DNL webapps] 디렉토리에서)를 삭제해야 할 수 있습니다.

* Tomcat이 WAR 파일의 압축을 해제하지 않도록 하려면 Tomcat의 [!DNL conf] 디렉토리에서 [!DNL server.xml] 파일을 편집하고 `false`(으)로 설정하여 `unpackWARs` 속성을 구성하십시오.

>[!NOTE]
>
>Tomcat이 시스템 클래스 경로에 [!DNL commons-logging.jar]을(를) 포함하도록 구성한 경우(보호된 스트리밍을 위한 Primetime DRM Server에 필요 없음) Log4J를 사용하도록 commons-logging을 구성해야 합니다.

서버에서는 최적의 성능을 위해 플랫폼별 라이브러리([!DNL jsafe.dll], Linux에서는 [!DNL libjsafe.so])를 선택적으로 사용합니다. 플랫폼의 적절한 라이브러리를 [!DNL thirdparty/cryptoj/]*platform*&#x200B;에서 `PATH` 환경 변수 또는 Linux의 `LD_LIBRARY_PATH`에 의해 지정된 위치로 복사할 수 있습니다.

>[!NOTE]
>
>64비트 버전은 운영 체제와 JDK 모두 64비트를 지원하는 경우에만 사용해야 합니다. 그렇지 않은 경우 32비트 버전을 사용해야 합니다.

