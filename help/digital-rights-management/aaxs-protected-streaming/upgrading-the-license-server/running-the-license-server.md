---
description: Adobe Access Server for Protected Streaming을 실행하는 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 flashaccessserver.war 파일을 최신 Adobe 액세스에 포함된 파일로 바꿉니다. 위에서 설명한 새 구성 옵션을 사용하려면 서버의 flashaccess-tenant.xml을 업데이트합니다. 또한 jsafe.dll 또는 libjsafe.so를 최신 Adobe 액세스에 포함된 버전으로 업데이트해야 합니다.
title: 보호된 스트리밍을 위한 Adobe Access Server 실행
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 보호된 스트리밍을 위한 Adobe Access Server 실행{#running-the-adobe-access-server-for-protected-streaming}

Adobe Access Server for Protected Streaming을 실행하는 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 flashaccessserver.war 파일을 최신 Adobe 액세스에 포함된 파일로 바꿉니다. 위에서 설명한 새 구성 옵션을 사용하려면 서버의 flashaccess-tenant.xml을 업데이트합니다. 또한 jsafe.dll 또는 libjsafe.so를 최신 Adobe 액세스에 포함된 버전으로 업데이트해야 합니다.

Adobe Access Server Adobe for Protected Streaming을 실행하기 전에 라이선스 서버와 함께 제공된 유틸리티를 사용하여 구성 파일이 유효한지 확인하는 것이 좋습니다. 자세한 내용은 &quot;[구성 검사기](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Tomcat과 라이센스 서버를 시작하려면 Tomcat의 bin 디렉토리에서 &quot;catalina.bat start&quot; 또는 &quot;catalina.sh start&quot;를 실행합니다.

서버가 시작된 후 를 열어 서버가 제대로 구성되었는지 확인합니다. *https:// license-server-host:port/flashaccessserver/tenant-name/flashaccess/license/v1* 을 클릭합니다. 테넌트 구성이 성공적으로 로드되면 확인 메시지가 표시됩니다.
