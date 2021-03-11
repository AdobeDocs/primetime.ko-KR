---
title: Flash Media Rights Management Server 1.x와의 호환성 확인
description: Flash Media Rights Management Server 1.x와의 호환성 확인
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x} 호환 여부 확인

Flash Media Rights Management Server 1.x 및 Adobe 액세스는 컨텐츠를 패키징하고 라이선스를 요청하는 데 서로 다른 메타데이터를 사용합니다. Adobe 액세스가 FMRMS 버전 1.x 컨텐츠를 사용하려면 메타데이터를 변환해야 합니다.

Adobe 액세스 SDK는 메타데이터를 변환하기 위한 두 가지 옵션을 지원합니다.

* 오프라인(권장)

   Adobe 액세스 메타데이터를 오프라인 프로세스에서 생성하여 클라이언트가 요청할 때 사용할 수 있도록 저장합니다. Adobe에서는 이 옵션을 권장합니다. 메타데이터가 오프라인으로 생성된 경우 라이선스 서버는 1.x CEK 또는 Packager 자격 증명을 액세스할 필요가 없습니다. 또한 라이센스 서버가 실시간으로 메타데이터를 생성할 필요가 없으므로 오프라인으로 전환하면 성능이 향상됩니다.

* On-Demand

   클라이언트가 요청 시 Adobe 액세스 메타데이터를 On-Demand로 생성할 수 있습니다. Adobe Access 클라이언트가 버전 1.x 컨텐츠를 다운로드할 때 DRM 메타데이터(DRM 헤더라고도 함)를 Adobe 액세스 SDK로 전송합니다. SDK는 DRM 메타데이터를 현재 형식으로 변환합니다. SDK는 CEK(Content Encryption Key)를 암호화하여 메타데이터에 포함하고 컨텐츠를 Adobe Access 클라이언트로 다시 전송합니다. (Adobe Access 1.x 메타데이터에는 CEK가 없습니다.)

   메타데이터를 변환하려면 Adobe 액세스 권한이 Adobe Access 1.x 컨텐츠 암호화 키에 액세스해야 합니다. Flash Media Rights Management Server 1.x에서 마이그레이션할 때, LiveCycle ES 데이터베이스에 컨텐츠 암호화 키를 계속 저장할 수 있으며, 사용자 정의 솔루션을 구현하여 다른 곳에 컨텐츠 암호화 키를 안전하게 저장할 수 있습니다. LiveCycle ES 데이터베이스에 컨텐츠 암호화 키를 계속 저장하도록 선택하는 경우 LiveCycle ES *에 대한 보안 및 강화를 위해*&#x200B;데이터베이스의 중요 컨텐츠에 대한 액세스 보호&quot;에 설명된 권장 사항을 따릅니다.

Flash Media Rights Management Server 1.x를 사용하여 패키지된 컨텐츠와의 호환성을 보장하는 방법에 대한 자세한 내용은 *Adobe 액세스 API 참조*&#x200B;를 참조하십시오.
