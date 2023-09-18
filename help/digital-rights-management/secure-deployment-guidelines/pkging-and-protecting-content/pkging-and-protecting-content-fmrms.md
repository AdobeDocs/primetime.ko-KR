---
description: Flash 미디어 Rights Management 서버 1.x 및 Adobe Primetime DRM은 다른 메타데이터를 사용하여 콘텐츠를 패키징하고 라이선스를 요청합니다. Primetime DRM이 FMRMS 버전 1.x 콘텐츠를 사용하려면 메타데이터를 변환해야 합니다.
title: Flash 미디어 Rights Management 서버 1.x와의 호환성 보장
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Flash 미디어 Rights Management 서버 1.x와의 호환성 보장 {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash 미디어 Rights Management 서버 1.x 및 Adobe Primetime DRM은 다른 메타데이터를 사용하여 콘텐츠를 패키징하고 라이선스를 요청합니다. Primetime DRM이 FMRMS 버전 1.x 콘텐츠를 사용하려면 메타데이터를 변환해야 합니다.

Primetime DRM SDK는 메타데이터의 변환을 위해 다음 옵션을 지원합니다.

* 오프라인(권장)

  오프라인 프로세스에서 Primetime DRM 메타데이터를 생성하고 클라이언트가 요청할 때까지 메타데이터를 저장합니다. 오프라인에서 메타데이터를 생성하는 경우 라이센스 서버는 1.x CEK 또는 packager 자격 증명에 액세스할 필요가 없습니다. 라이선스 서버는 실시간으로 메타데이터를 생성할 필요가 없기 때문에 오프라인을 전환하면 더 나은 성능을 제공합니다.
* 온디맨드

  Primetime DRM 메타데이터는 클라이언트가 메타데이터를 요청할 때 생성됩니다. Primetime DRM 클라이언트가 버전 1.x 콘텐츠를 다운로드하면 클라이언트는 DRM 메타데이터를 Primetime DRM SDK로 전송합니다. SDK는 DRM 메타데이터를 현재 형식으로 변환하고, 콘텐츠 암호화 키(CEK)를 암호화하여 메타데이터에 임베드한 다음, 콘텐츠를 Primetime DRM 클라이언트로 다시 전송합니다.

  >[!NOTE]
  >
  >Primetime DRM 1.x 메타데이터는 CEK를 포함하지 않습니다.

  메타데이터를 변환하려면 Primetime DRM은 Primetime DRM 1.x 콘텐츠 암호화 키에 액세스해야 합니다. Flash Media Rights Management 서버 1.x에서 마이그레이션할 때 컨텐츠 암호화 키를 LiveCycle ES 데이터베이스에 계속 저장하거나, 사용자 지정 솔루션을 구현하여 컨텐츠 암호화 키를 다른 위치에 안전하게 저장할 수 있습니다. LiveCycle ES 데이터베이스에 콘텐츠 암호화 키를 저장하기로 결정한 경우, 아래 설명된 권장 사항을 따르십시오. *데이터베이스의 중요한 콘텐츠에 대한 액세스 보호* 위치: **LiveCycle® ES2 보안 강화**.

Flash Media Rights Management 서버 1.x를 사용하여 패키지된 콘텐츠와의 호환성을 확인하는 방법에 대한 자세한 내용은 의 Adobe Primetime DRM API를 참조하십시오 [Adobe Primetime API 참조](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
