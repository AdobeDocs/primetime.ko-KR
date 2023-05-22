---
title: 보호된 스트리밍을 위해 Adobe Primetime DRM 서버 배포
description: 보호된 스트리밍을 위해 Adobe Primetime DRM 서버 배포
copied-description: true
exl-id: 814c08e6-5d09-495b-b529-cedc9b9c02a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 보호된 스트리밍을 위해 Adobe Primetime DRM 서버 배포{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

보호된 스트리밍을 위해 Adobe Primetime DRM 서버를 배포하려면 먼저 요구 사항 항목에 나열된 대로 Java 및 Tomcat 버전을 설치해야 합니다.

보호 스트리밍 패키지용 Primetime DRM 서버에는 [!DNL flashaccesserver.war]. 다음과 같은 경우:

* 이 WAR 파일을 배포하려면 Tomcat의 [!DNL webapps] 디렉토리.
* 이전에 WAR 파일을 배포한 경우 압축을 푼 WAR 디렉토리( [!DNL flashaccessserver] 톰캣 [!DNL webapps] directory).

* Tomcat이 WAR 파일의 압축을 푸는 것을 방지하려면 다음을 편집합니다. [!DNL server.xml] Tomcat의 파일 [!DNL conf] 디렉터리 및 구성 `unpackWARs` 속성을 로 설정하여 `false`.

>[!NOTE]
>
>Tomcat에 을 포함하도록 구성한 경우 [!DNL commons-logging.jar] 시스템 클래스 경로(Primetime DRM Server for Protected Streaming에는 필요하지 않음)에서 Log4J를 사용하도록 commons-logging을 구성해야 합니다.

서버는 선택적으로 플랫폼별 라이브러리( )를 사용합니다. [!DNL jsafe.dll] Microsoft Windows에서 또는 [!DNL libjsafe.so] 최적의 성능을 위해 Linux에서. 다음에서 플랫폼에 적절한 라이브러리를 복사할 수 있습니다. [!DNL thirdparty/cryptoj/]*platform* 에 의해 지정된 위치로 `PATH` 환경 변수 또는 `LD_LIBRARY_PATH` Linux에서.

>[!NOTE]
>
>운영 체제와 JDK가 모두 64비트를 지원하는 경우 64비트 버전만 사용해야 합니다. 그렇지 않으면 32비트 버전을 사용해야 합니다.
