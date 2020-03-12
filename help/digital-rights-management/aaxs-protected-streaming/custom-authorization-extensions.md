---
seo-title: 사용자 정의 인증 확장
title: 사용자 정의 인증 확장
description: 사용자 지정 인증 로직은 라이센스 획득 중에 호출되어 요청을 하는 클라이언트에 라이센스를 발급할지를 결정할 수 있습니다.
seo-description: 사용자 지정 인증 로직은 라이센스 획득 중에 호출되어 요청을 하는 클라이언트에 라이센스를 발급할지를 결정할 수 있습니다.
uuid: fb40db6f-30aa-46e3-9eeb-faff3cfedab1
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0

---


# 사용자 정의 인증 확장 {#custom-authorization-extensions}

사용자 지정 인증 로직은 라이센스 획득 중에 호출되어 요청을 하는 클라이언트에 라이센스를 발급할지를 결정할 수 있습니다.

자체 고객 인증 확장을 구현하려면 먼저 샘플 디렉토리에 있는 [!DNL SampleAuthorizer.java] 샘플 코드를 살펴보십시오(이 샘플의 컴파일된 버전은 flashaccess-license-server-ext-sample.jar에 있음).

자체 확장을 만들려면 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 인터페이스를 구현하고, 에서 특정 필드를 활용하는 경우 빌드 경로에 있으며 빌드 경로에 `flashaccess-license-server-exts.jar` 있는 `commons-logging.jar` 상태여야 `adobe-flashaccess-sdk.jar` 합니다 `IMessageFacade`. 확장 기능을 배포하려면 jar 또는 클래스 파일을 LicenseServer.ConfigRoot에 *복사하십시오* `/flashaccessserver/libs`. jar 또는 클래스 파일을 업데이트해야 하는 경우 업데이트된 버전을 사용하기 전에 서버를 다시 시작해야 합니다. 또한 Authorizer 클래스 이름을 테넌트 구성 파일에 추가해야 합니다.
