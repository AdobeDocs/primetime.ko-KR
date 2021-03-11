---
title: 사용자 정의 인증 확장
description: 사용자 지정 인증 로직은 라이센스 취득 중에 호출되어 요청을 받은 클라이언트에 라이센스를 발급할지를 결정할 수 있습니다.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 사용자 정의 인증 확장 {#custom-authorization-extensions}

사용자 지정 인증 로직은 라이센스 취득 중에 호출되어 요청을 받은 클라이언트에 라이센스를 발급할지를 결정할 수 있습니다.

고유한 고객 인증 확장을 구현하려면 먼저 샘플 디렉토리에 있는 [!DNL SampleAuthorizer.java] 샘플 코드를 확인합니다. 이 샘플의 컴파일된 버전은 flashaccess-license-server-ext-sample.jar에 있습니다.

자체 확장을 만들려면 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 인터페이스를 구현하고 `flashaccess-license-server-exts.jar` 및 `commons-logging.jar`이(가) `IMessageFacade`의 특정 필드를 사용하는 경우 빌드 경로 `adobe-flashaccess-sdk.jar`에도 있어야 합니다. 확장을 배포하려면 jar 또는 클래스 파일을 *LicenseServer.ConfigRoot* `/flashaccessserver/libs`에 복사합니다. jar 또는 클래스 파일을 업데이트해야 하는 경우 업데이트된 버전을 사용하기 전에 서버를 다시 시작해야 합니다. 또한 권한이 있는 클래스 이름을 테넌트 구성 파일에 추가해야 합니다.
