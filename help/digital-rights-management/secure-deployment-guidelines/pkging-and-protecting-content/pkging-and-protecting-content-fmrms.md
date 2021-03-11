---
description: Flash Media Rights Management Server 1.x 및 Adobe Primetime DRM은 서로 다른 메타데이터를 사용하여 컨텐츠를 패키징하고 라이선스를 요청합니다. Primetime DRM에서 FMRMS 버전 1.x 콘텐츠를 사용하려면 메타데이터를 변환해야 합니다.
title: Flash Media Rights Management Server 1.x와의 호환성 보장
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}와의 호환성 보장

Flash Media Rights Management Server 1.x 및 Adobe Primetime DRM은 서로 다른 메타데이터를 사용하여 컨텐츠를 패키징하고 라이선스를 요청합니다. Primetime DRM에서 FMRMS 버전 1.x 콘텐츠를 사용하려면 메타데이터를 변환해야 합니다.

Primetime DRM SDK는 다음 메타데이터 변환 옵션을 지원합니다.

* 오프라인(권장)

   오프라인 프로세스를 통해 Primetime DRM 메타데이터를 생성하고 클라이언트가 요청할 때까지 메타데이터를 저장할 수 있습니다. 메타데이터가 오프라인으로 생성된 경우 라이선스 서버는 1.x CEK 또는 Packager 자격 증명을 액세스할 필요가 없습니다. 라이센스 서버가 실시간으로 메타데이터를 생성할 필요가 없으므로 오프라인으로 전환하면 성능이 향상됩니다.
* On-Demand

   Primetime DRM 메타데이터는 클라이언트가 메타데이터를 요청할 때 생성됩니다. Primetime DRM 클라이언트가 버전 1.x 콘텐츠를 다운로드하면 클라이언트는 DRM 메타데이터를 Primetime DRM SDK로 보냅니다. SDK는 DRM 메타데이터를 현재 포맷으로 변환하고 메타데이터에 CEK(콘텐츠 암호화 키)를 암호화하여 포함하고 해당 콘텐츠를 다시 Primetime DRM 클라이언트로 보냅니다.

   >[!NOTE]
   >
   >Primetime DRM 1.x 메타데이터에는 CEK가 포함되지 않습니다.

   메타데이터를 변환하려면 Primetime DRM에서 Primetime DRM 1.x 콘텐츠 암호화 키에 대한 액세스 권한이 필요합니다. Flash Media Rights Management Server 1.x에서 마이그레이션할 때, LiveCycle ES 데이터베이스에 컨텐츠 암호화 키를 계속 저장하거나 사용자 정의 솔루션을 구현하여 다른 위치에 컨텐츠 암호화 키를 안전하게 저장할 수 있습니다. LiveCycle ES 데이터베이스에 컨텐츠 암호화 키를 저장하기로 결정한 경우 *LiveCycle® ES2 **용 보안 강화 및 보안에서 데이터베이스*의 중요 콘텐츠에 대한 액세스 보호**

Flash Media Rights Management Server 1.x를 사용하여 패키지된 컨텐츠와의 호환성을 보장하는 방법에 대한 자세한 내용은 [Adobe Primetime API 참조 설명서](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)의 Adobe Primetime DRM API를 참조하십시오.
