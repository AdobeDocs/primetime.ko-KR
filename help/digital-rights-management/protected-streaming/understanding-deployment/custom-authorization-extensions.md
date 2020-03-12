---
description: 라이센스 취득 중에 사용자 지정 인증 로직을 호출하여 요청한 클라이언트에 라이센스를 발급할지 여부를 결정할 수 있습니다.
seo-description: 라이센스 취득 중에 사용자 지정 인증 로직을 호출하여 요청한 클라이언트에 라이센스를 발급할지 여부를 결정할 수 있습니다.
seo-title: 사용자 정의 인증 확장
title: 사용자 정의 인증 확장
uuid: 588b05e5-3402-4586-bbd4-58b7e9a58ee4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 사용자 정의 인증 확장{#custom-authorization-extensions}

라이센스 취득 중에 사용자 지정 인증 로직을 호출하여 요청한 클라이언트에 라이센스를 발급할지 여부를 결정할 수 있습니다.

고유한 고객 인증 확장을 구현하려면 먼저 샘플 디렉토리에 있는 [!DNL SampleAuthorizer.java] 샘플 코드를 살펴보아야 합니다. 이 샘플의 컴파일된 버전은 에 [!DNL flashaccess-license-server-ext-sample.jar]있습니다.

고유한 확장 기능을 만들려면 `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` 인터페이스를 구현하고 빌드 경로에 있는지 확인해야 합니다( 에서 특정 필드를 사용하는 [!DNL flashaccess-license-server-exts.jar] 경우 빌드 경로에도 있어야 [!DNL commons-logging.jar] 함 [!DNL adobe-flashaccess-sdk.jar] `IMessageFacade`).

확장을 배포하려면 jar 또는 클래스 파일을 LicenseServer.ConfigRoot에 복사해야 *합니다* [!DNL /flashaccessserver/libs].

jar 또는 클래스 파일을 업데이트하려면 업데이트된 버전을 사용하기 전에 서버를 다시 시작해야 합니다. 또한 Authorizer 클래스 이름을 테넌트 구성 파일에 추가해야 합니다.
