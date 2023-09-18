---
title: 사용자 지정 권한 부여 확장
description: 라이센스 획득 중에 사용자 지정 인증 논리를 호출하여 요청하는 클라이언트에 라이센스를 발급해야 하는지 여부를 결정할 수 있습니다.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 사용자 지정 권한 부여 확장 {#custom-authorization-extensions}

라이센스 획득 중에 사용자 지정 인증 논리를 호출하여 요청하는 클라이언트에 라이센스를 발급해야 하는지 여부를 결정할 수 있습니다.

고유한 고객 인증 확장을 구현하려면 먼저 다음을 살펴보십시오. [!DNL SampleAuthorizer.java] sample 디렉토리에 있는 샘플 코드(이 샘플의 컴파일된 버전은 flashaccess-license-server-ext-sample.jar에 있음).

고유한 확장을 빌드하려면 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 인터페이스 및 확인 `flashaccess-license-server-exts.jar` 및 `commons-logging.jar` 빌드 경로에 있습니다. `adobe-flashaccess-sdk.jar` 의 특정 필드를 활용하는 경우 빌드 경로에도 있어야 합니다. `IMessageFacade`). 확장을 배포하려면 jar 또는 클래스 파일을 *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. jar 또는 클래스 파일을 업데이트해야 하는 경우 업데이트된 버전을 사용하기 전에 서버를 다시 시작해야 합니다. 또한 권한 부여자 클래스 이름을 테넌트 구성 파일에 추가해야 합니다.
