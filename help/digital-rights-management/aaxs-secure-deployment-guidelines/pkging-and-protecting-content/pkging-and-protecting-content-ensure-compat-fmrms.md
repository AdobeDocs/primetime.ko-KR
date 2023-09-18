---
title: Flash 미디어 Rights Management 서버 1.x와의 호환성 보장
description: Flash 미디어 Rights Management 서버 1.x와의 호환성 보장
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Flash 미디어 Rights Management 서버 1.x와의 호환성 보장{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management 서버 1.x 및 Adobe 액세스는 콘텐츠를 패키징하고 라이선스를 요청하는 데 다른 메타데이터를 사용합니다. Adobe 액세스 시 FMRMS 버전 1.x 콘텐츠를 사용하려면 메타데이터를 변환해야 합니다.

Adobe 액세스 SDK는 메타데이터를 변환하는 두 가지 옵션을 지원합니다.

* 오프라인(권장)

  오프라인 프로세스에서 Adobe 액세스 메타데이터를 생성하고 클라이언트가 요청할 때 사용할 수 있도록 저장합니다. Adobe은 이 옵션을 권장합니다. 오프라인에서 메타데이터를 생성하는 경우 라이센스 서버는 1.x CEK 또는 packager 자격 증명에 액세스할 필요가 없습니다. 또한 라이선스 서버가 실시간으로 메타데이터를 생성할 필요가 없기 때문에 오프라인을 전환하면 더 나은 성능을 제공합니다.

* 온디맨드

  클라이언트가 요청할 때 Adobe 액세스 메타데이터를 온디맨드로 생성합니다. Adobe 액세스 클라이언트가 버전 1.x 컨텐츠를 다운로드하면 DRM 메타데이터(DRM 헤더라고도 함)가 Adobe 액세스 SDK로 전송됩니다. SDK는 DRM 메타데이터를 현재 형식으로 변환합니다. SDK는 콘텐츠 암호화 키(CEK)를 암호화하여 메타데이터에 임베드한 다음 Adobe 액세스 클라이언트로 콘텐츠를 다시 전송합니다. (Adobe 액세스 1.x 메타데이터에 CEK가 포함되어 있지 않습니다.)

  메타데이터를 변환하려면 Adobe Access에서 Adobe Access 1.x 콘텐츠 암호화 키에 액세스해야 합니다. Flash 미디어 Rights Management 서버 1.x에서 마이그레이션할 때 컨텐츠 암호화 키를 LiveCycle ES 데이터베이스에 계속 저장하거나, 사용자 지정 솔루션을 구현하여 컨텐츠 암호화 키를 다른 곳에 안전하게 저장할 수 있습니다. LiveCycle ES 데이터베이스에 콘텐츠 암호화 키를 계속 저장하도록 선택하는 경우 의 &quot;데이터베이스의 중요한 콘텐츠에 대한 액세스 보호&quot;에 설명된 권장 사항을 따르십시오. *LiveCycle ES의 보안 강화*.

Flash 미디어 Rights Management 서버 1.x를 사용하여 패키지된 콘텐츠와의 호환성을 확인하는 방법에 대한 자세한 내용은 *Adobe 액세스 API 참조*.
