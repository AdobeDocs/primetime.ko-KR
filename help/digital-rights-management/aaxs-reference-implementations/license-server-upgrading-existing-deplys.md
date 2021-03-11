---
title: 기존 배포 업그레이드
description: 기존 배포 업그레이드
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 기존 배포 업그레이드 {#upgrading-existing-deployments}

버전 3.0 참조 구현 라이선스 서버 또는 감시 폴더 패키지를 실행하는 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 [!DNL .war] 파일을 Adobe 액세스 참조 구현 서버에 포함된 파일로 바꿉니다.

참조 구현 라이센스 서버에서 도메인 등록을 사용하려는 경우 몇 개의 새 데이터베이스 테이블이 필요합니다. 전체 참조 구현 데이터베이스를 다시 만들려면 `CreateSampleDB.sql`을(를) 실행하십시오. 기존 데이터베이스 레코드를 유지하고 새 테이블을 추가하려면 `CreateSampleDB.sql`을 열고 다음 테이블을 만드는 명령만 실행합니다.

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

도메인 지원을 사용하려면 flashaccess-refimpl.properties에 다음 속성을 추가해야 합니다.

* `HandlerConfiguration.DomainCAs.n` or  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 및  `DomainRegistrationHandler.ServerCredential.password`또는  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

iOS 클라이언트에 대한 원격 키 제공을 지원하려면 다음 속성을 [!DNL flashaccess-refimpl.properties]에 추가해야 합니다.

* `HandlerConfiguration.KeyServerCertificate` or  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

