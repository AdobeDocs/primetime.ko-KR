---
seo-title: 안전한 스트리밍을 위한 Adobe Access Server 배포 개요
title: 안전한 스트리밍을 위한 Adobe Access Server 배포 개요
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 보호된 스트리밍을 위한 Adobe Access Server 배포 개요 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

보호 스트리밍을 위한 Adobe Access Server을 배포하기 전에 요구 사항 섹션에 나열된 Java 및 Tomcat 버전을 설치했는지 확인하십시오.

보호된 스트리밍용 Adobe Access Server 패키지에는 [!DNL flashaccesserver.war]이 포함됩니다. 이 WAR 파일을 배포하려면 Tomcat의 [!DNL webapps] 디렉토리로 복사합니다. 이전에 WAR 파일을 배포한 경우 압축을 푼 WAR 디렉터리( [!DNL flashaccessserver] Tomcat의 [!DNL webapps] 디렉토리에서)를 수동으로 삭제해야 할 수 있습니다. Tomcat이 WAR 파일의 압축을 해제하지 않도록 하려면 Tomcat의 [!DNL conf] 디렉토리에서 [!DNL server.xml] 파일을 편집하고 `unpackWARs` 특성을 `false`으로 설정합니다.

>[!NOTE]
>
>Tomcat이 시스템 클래스 경로에 [!DNL commons-logging.jar]을 포함하도록 구성한 경우(보호 스트리밍을 위한 Adobe Access Server에 필요하지 않음) Log4J를 사용하도록 commons-logging을 구성해야 합니다.

서버에서는 최적의 성능을 위해 플랫폼별 라이브러리([!DNL jsafe.dll], Microsoft Windows의 경우 [!DNL libjsafe.so])를 선택적으로 사용합니다. 플랫폼에 적합한 라이브러리를 [!DNL thirdparty/cryptoj/]*platform*&#x200B;에서 `PATH` 환경 변수(또는 Linux의 `LD_LIBRARY_PATH`)로 지정된 위치로 복사합니다.

>[!NOTE]
>
>64비트 버전은 운영 체제와 JDK 모두 64비트를 지원하는 경우에만 사용해야 하며, 그렇지 않은 경우 32비트 버전을 사용해야 합니다.

