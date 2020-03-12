---
seo-title: 안전한 스트리밍을 위한 Adobe Access Server 배포 개요
title: 안전한 스트리밍을 위한 Adobe Access Server 배포 개요
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 안전한 스트리밍을 위한 Adobe Access Server 배포 개요 {#deploying-the-adobe-access-server-for-protected-streaming-overview}

보호 스트리밍을 위한 Adobe Access Server를 배포하기 전에 요구 사항 섹션에 나열된 Java 및 Tomcat 버전을 설치했는지 확인하십시오.

보호된 스트리밍을 위한 Adobe Access Server 패키지에 포함되어 [!DNL flashaccesserver.war]있습니다. 이 WAR 파일을 배포하려면 Tomcat의 [!DNL webapps] 디렉토리에 복사합니다. 이전에 WAR 파일을 배포한 경우 압축을 푼 WAR 디렉토리(Tomcat [!DNL flashaccessserver] 의 [!DNL webapps] 디렉토리)를 수동으로 삭제해야 할 수 있습니다. Tomcat이 WAR 파일의 압축을 풀지 않도록 하려면 Tomcat의 [!DNL server.xml] 디렉토리에서 [!DNL conf] 파일을 편집하고 `unpackWARs` 속성을 `false`로 설정합니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Tomcat이 System 클래스 경로에 포함하도록 구성한 경우(보호 스트리밍을 [!DNL commons-logging.jar] 위한 Adobe Access Server의 경우 필요 없음) Log4J를 사용하도록 commons-logging을 구성해야 합니다.

서버는 최적의 성능을 위해 플랫폼별 라이브러리(Microsoft Windows [!DNL jsafe.dll] 또는 Linux [!DNL libjsafe.so] 에서)를 선택적으로 사용합니다. 플랫폼에 [!DNL thirdparty/cryptoj/]*적합한 라이브러리를&#x200B;*환경 변수(또는 Linux`PATH``LD_LIBRARY_PATH`)에 의해 지정된 위치로 복사합니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>64비트 버전은 운영 체제와 JDK 모두 64비트를 지원하는 경우에만 사용해야 하며, 그렇지 않은 경우 32비트 버전을 사용해야 합니다.

