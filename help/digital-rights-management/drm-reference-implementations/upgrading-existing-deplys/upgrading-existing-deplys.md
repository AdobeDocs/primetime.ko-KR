---
description: 버전 3.0 참조 구현 라이선스 서버 또는 감시 폴더 패키저를 지원하는 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 .war 파일을 Adobe Primetime DRM Reference Implementation Server에 포함된 파일로 교체해야 합니다.
seo-description: 버전 3.0 참조 구현 라이선스 서버 또는 감시 폴더 패키저를 지원하는 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 .war 파일을 Adobe Primetime DRM Reference Implementation Server에 포함된 파일로 교체해야 합니다.
seo-title: 기존 배포 업그레이드
title: 기존 배포 업그레이드
uuid: 1a40aae9-f639-41fa-b42d-cf8cdfcde694
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 개요 {#upgrade-existing-deployments-overview}

버전 3.0 참조 구현 라이선스 서버 또는 감시 폴더 패키저를 지원하는 서버를 업그레이드하려면 응용 프로그램 서버에 배포된 .war 파일을 Adobe Primetime DRM Reference Implementation Server에 포함된 파일로 교체해야 합니다.

참조 구현 라이센스 서버에 도메인 등록을 사용하려면 몇 개의 새 데이터베이스 테이블이 필요합니다. 전체 참조 구현 데이터베이스를 다시 만들고 실행해야 `CreateSampleDB.sql`합니다.

데이터베이스 레코드를 유지하고 새 테이블을 추가하려면:

1. 다음 표를 만드는 명령을 열고 `CreateSampleDB.sql` 실행합니다.

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. 도메인 지원을 [!DNL flashaccess-refimpl.properties] 사용하려면 다음 속성을 추가하십시오.

   * `HandlerConfiguration.DomainCAs.n` or `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` and `DomainRegistrationHandler.ServerCredential.password` or `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. iOS 클라이언트에 원격 키 제공을 [!DNL flashaccess-refimpl.properties] 지원하기 위해 다음 속성을 추가합니다.

   * `HandlerConfiguration.KeyServerCertificate` or `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`