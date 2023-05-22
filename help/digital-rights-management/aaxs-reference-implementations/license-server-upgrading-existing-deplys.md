---
title: 기존 배포 업그레이드
description: 기존 배포 업그레이드
copied-description: true
exl-id: e07b883f-d5f7-40d3-9221-a0dc2d859a5a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 기존 배포 업그레이드 {#upgrading-existing-deployments}

버전 3.0 참조 구현 라이선스 서버 또는 감시 폴더 패키지를 실행하는 서버를 업그레이드하려면 [!DNL .war] Adobe 액세스 참조 구현 서버에 포함된 파일과 함께 Application Server에 배포된 파일

참조 구현 라이선스 서버에 도메인 등록을 사용하려면 몇 개의 새 데이터베이스 테이블이 필요합니다. 전체 참조 구현 데이터베이스를 다시 만들려면 다음을 실행합니다 `CreateSampleDB.sql`. 기존 데이터베이스 레코드를 보존하고 새 테이블을 추가하려면 를 엽니다. `CreateSampleDB.sql`명령을 실행하여 다음 테이블만 생성합니다.

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

도메인 지원을 사용하려면 flashaccess-refimpl.properties에 다음 속성을 추가해야 합니다.

* `HandlerConfiguration.DomainCAs.n` 또는 `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` 및 `DomainRegistrationHandler.ServerCredential.password`, 또는 `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

다음 속성을에 추가해야 합니다. [!DNL flashaccess-refimpl.properties] iOS 클라이언트에 원격 키 전달을 지원하려면

* `HandlerConfiguration.KeyServerCertificate` 또는 `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
