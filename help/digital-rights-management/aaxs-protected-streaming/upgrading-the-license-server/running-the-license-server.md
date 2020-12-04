---
description: 보호된 스트리밍을 위해 Adobe Access Server을 실행 중인 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 flashaccess server.war 파일을 최신 Adobe 액세스에 포함된 파일로 교체합니다. 위에 설명된 새 구성 옵션을 사용하려면 서버의 flashaccess-tenant.xml을 업데이트하십시오. 또한 최신 Adobe 액세스에 포함된 버전으로 jsafe.dll 또는 libjsafe.so를 업데이트해야 합니다.
seo-description: 보호된 스트리밍을 위해 Adobe Access Server을 실행 중인 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 flashaccess server.war 파일을 최신 Adobe 액세스에 포함된 파일로 교체합니다. 위에 설명된 새 구성 옵션을 사용하려면 서버의 flashaccess-tenant.xml을 업데이트하십시오. 또한 최신 Adobe 액세스에 포함된 버전으로 jsafe.dll 또는 libjsafe.so를 업데이트해야 합니다.
seo-title: 안전한 스트리밍을 위한 Adobe Access Server 실행
title: 안전한 스트리밍을 위한 Adobe Access Server 실행
uuid: 3819500d-ad2f-49eb-8aa4-e50a55461608
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 보호된 스트리밍을 위한 Adobe Access Server 실행{#running-the-adobe-access-server-for-protected-streaming}

보호된 스트리밍을 위해 Adobe Access Server을 실행 중인 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 flashaccess server.war 파일을 최신 Adobe 액세스에 포함된 파일로 교체합니다. 위에 설명된 새 구성 옵션을 사용하려면 서버의 flashaccess-tenant.xml을 업데이트하십시오. 또한 최신 Adobe 액세스에 포함된 버전으로 jsafe.dll 또는 libjsafe.so를 업데이트해야 합니다.

보호된 스트리밍을 위한 Adobe Access Server을 실행하기 전에 라이센스 서버와 함께 제공된 유틸리티를 사용하여 구성 파일이 유효한지 확인할 것을 Adobe이 권장합니다. 자세한 내용은 &quot;[구성 유효성 검사기](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;을 참조하십시오.

Tomcat 및 라이센스 서버를 시작하려면 Tomcat의 bin 디렉토리에서 &quot;catalina.bat start&quot; 또는 &quot;catalina.sh start&quot;를 실행합니다.

서버가 시작된 후 브라우저 창에서 *https:// license-server-host:port/flashaccess server/tenant-name/flashaccess/license/v1*&#x200B;을 열어 서버가 올바르게 구성되어 있는지 확인합니다. 테넌트 구성이 성공적으로 로드되면 확인 메시지가 표시됩니다.
