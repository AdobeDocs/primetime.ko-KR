---
description: Flash Media Rights Management Server 1.x 및 Adobe Primetime DRM은 서로 다른 메타데이터를 사용하여 컨텐츠를 패키지하고 라이선스를 요청합니다. Primetime DRM에서 FMRMS 버전 1.x 콘텐츠를 사용하려면 메타데이터를 변환해야 합니다.
seo-description: Flash Media Rights Management Server 1.x 및 Adobe Primetime DRM은 서로 다른 메타데이터를 사용하여 컨텐츠를 패키지하고 라이선스를 요청합니다. Primetime DRM에서 FMRMS 버전 1.x 콘텐츠를 사용하려면 메타데이터를 변환해야 합니다.
seo-title: Flash Media Rights Management Server 1.x와의 호환성 보장
title: Flash Media Rights Management Server 1.x와의 호환성 보장
uuid: dd70941e-9015-4fb0-b265-557b6252e051
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Flash Media Rights Management Server 1.x와의 호환성 보장 {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x 및 Adobe Primetime DRM은 서로 다른 메타데이터를 사용하여 컨텐츠를 패키지하고 라이선스를 요청합니다. Primetime DRM에서 FMRMS 버전 1.x 콘텐츠를 사용하려면 메타데이터를 변환해야 합니다.

Primetime DRM SDK는 다음 메타데이터 변환 옵션을 지원합니다.

* 오프라인(권장)

   오프라인 프로세스에서 Primetime DRM 메타데이터를 생성하고 클라이언트가 요청할 때까지 메타데이터를 저장할 수 있습니다. 메타데이터가 오프라인으로 생성된 경우 라이선스 서버는 1.x CEK 또는 Packager 자격 증명에 액세스할 필요가 없습니다. 라이센스 서버가 실시간으로 메타데이터를 생성할 필요가 없으므로 오프라인으로 전환하면 성능이 향상됩니다.
* On-Demand

   Primetime DRM 메타데이터는 클라이언트가 메타데이터를 요청할 때 생성됩니다. Primetime DRM 클라이언트가 버전 1.x 콘텐츠를 다운로드할 때 클라이언트는 DRM 메타데이터를 Primetime DRM SDK로 보냅니다. SDK는 DRM 메타데이터를 현재 형식으로 변환하고, 메타데이터에 CEK(콘텐츠 암호화 키)를 암호화하고 포함하고, 해당 콘텐츠를 다시 Primetime DRM 클라이언트로 보냅니다.

   >[!NOTE]
   >
   >Primetime DRM 1.x 메타데이터는 CEK를 포함하지 않습니다.

   메타데이터를 변환하려면 Primetime DRM이 Primetime DRM 1.x 콘텐츠 암호화 키에 액세스해야 합니다. Flash Media Rights Management Server 1.x에서 마이그레이션할 때 LiveCycle ES 데이터베이스에 컨텐츠 암호화 키를 계속 저장하거나 사용자 정의 솔루션을 구현하여 컨텐츠 암호화 키를 다른 위치에 안전하게 저장할 수 있습니다. LiveCycle ES 데이터베이스에 컨텐츠 암호화 키를 저장하기로 결정한 경우 LiveCycle® ES2의 *보안 강화 및 보안* 섹션에서 데이터베이스의 **민감한 컨텐츠에 대한 액세스**&#x200B;보호에 설명된 권장 사항을 따릅니다.

Flash Media Rights Management Server 1.x를 사용하여 패키지된 컨텐츠와의 호환성을 보장하는 방법에 대한 자세한 내용은 Adobe Primetime API 참조에서 Adobe Primetime DRM [API를 참조하십시오](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
