---
title: Protected Streaming용 Adobe Access Server 배포 개요
description: Protected Streaming용 Adobe Access Server 배포 개요
copied-description: true
exl-id: fdefa13a-14ec-4301-ab39-2ceea830463d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Protected Streaming용 Adobe Access Server 배포 개요 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

보호된 스트리밍을 위해 Adobe Access Server을 배포하기 전에 요구 사항 섹션에 나열된 Java 및 Tomcat 버전을 설치했는지 확인하십시오.

Adobe Access Server for Protected Streaming 패키지에는 다음이 포함됩니다 [!DNL flashaccesserver.war]. 이 WAR 파일을 배포하려면 Tomcat의 [!DNL webapps] 디렉토리. 이전에 WAR 파일을 배포한 경우 압축을 푼 WAR 디렉토리를 수동으로 삭제해야 할 수 있습니다( [!DNL flashaccessserver] 톰캣 [!DNL webapps] directory). Tomcat이 WAR 파일의 압축을 푸는 것을 방지하려면 [!DNL server.xml] Tomcat의 파일 [!DNL conf] 디렉터리 및 설정 `unpackWARs` 특성 대상 `false`.

>[!NOTE]
>
>Tomcat에 을 포함하도록 구성한 경우 [!DNL commons-logging.jar] 시스템 클래스 경로(보호되는 스트리밍용 Adobe Access Server에는 필요하지 않음)에서 Log4J를 사용하도록 commons-logging을 구성해야 합니다.

서버는 선택적으로 플랫폼별 라이브러리( )를 사용합니다. [!DNL jsafe.dll] Microsoft Windows에서 또는 [!DNL libjsafe.so] Linux의 경우) 최적의 성능을 제공합니다. 다음에서 플랫폼에 적절한 라이브러리를 복사합니다. [!DNL thirdparty/cryptoj/]*platform* 에 의해 지정된 위치로 `PATH` 환경 변수(또는 `LD_LIBRARY_PATH` Linux에서).

>[!NOTE]
>
>64비트 버전은 운영 체제와 JDK가 모두 64비트를 지원하는 경우에만 사용하고 그렇지 않으면 32비트 버전을 사용해야 합니다.
