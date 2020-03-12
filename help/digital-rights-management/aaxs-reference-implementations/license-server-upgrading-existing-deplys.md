---
seo-title: 기존 배포 업그레이드
title: 기존 배포 업그레이드
uuid: 57e62a88-e541-435c-8274-7f1602548601
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 기존 배포 업그레이드 {#upgrading-existing-deployments}

버전 3.0 Reference Implementation License Server 또는 Watched Folder Packager를 실행하는 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 파일을 Adobe Access Reference Implementation Server에 포함된 파일로 바꿉니다. [!DNL .war]

참조 구현 라이센스 서버에 도메인 등록을 사용하려는 경우 몇 개의 새 데이터베이스 테이블이 필요합니다. 전체 참조 구현 데이터베이스를 다시 만들려면 실행하십시오 `CreateSampleDB.sql`. 기존 데이터베이스 레코드를 유지하고 새 테이블을 추가하려면 다음 테이블을 만들기 위해 명령을 열고 `CreateSampleDB.sql`실행하기만 하면 됩니다.

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

도메인 지원을 사용하려면 flashaccess-refimpl.properties에 다음 속성을 추가해야 합니다.

* `HandlerConfiguration.DomainCAs.n` or `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 및 `DomainRegistrationHandler.ServerCredential.password`또는 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

iOS 클라이언트에 대한 원격 키 제공을 [!DNL flashaccess-refimpl.properties] 지원하려면 다음 속성을 추가해야 합니다.

* `HandlerConfiguration.KeyServerCertificate` or `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

