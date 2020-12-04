---
seo-title: Flash Media Rights Management Server 1.x와의 호환성 보장
title: Flash Media Rights Management Server 1.x와의 호환성 보장
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}과의 호환성 보장

Flash 미디어 Rights Management 서버 1.x 및 Adobe 액세스 기능은 컨텐츠를 패키지화하고 라이선스를 요청하는 데 서로 다른 메타데이터를 사용합니다. Adobe 액세스가 FMRMS 버전 1.x 컨텐츠를 사용하려면 메타데이터를 변환해야 합니다.

Adobe 액세스 SDK는 두 가지 메타데이터 변환 옵션을 지원합니다.

* 오프라인(권장)

   오프라인 프로세스에서 Adobe 액세스 메타데이터를 생성하여 클라이언트가 요청할 때 사용할 수 있도록 저장합니다. Adobe은 이 옵션을 권장합니다. 메타데이터가 오프라인으로 생성된 경우 라이선스 서버는 1.x CEK나 Packager 자격 증명에 액세스할 필요가 없습니다. 또한 라이센스 서버에서 실시간으로 메타데이터를 생성할 필요가 없기 때문에 오프라인으로 전환하면 성능이 향상됩니다.

* On-Demand

   클라이언트가 요청 시 Adobe 액세스 메타데이터를 on-demand로 생성합니다. Adobe Access 클라이언트가 버전 1.x 컨텐츠를 다운로드할 때 DRM 메타데이터(DRM 헤더)를 Adobe 액세스 SDK로 보냅니다. SDK는 DRM 메타데이터를 현재 형식으로 변환합니다. SDK는 메타데이터에 있는 CEK(컨텐츠 암호화 키)를 암호화하여 포함하고 컨텐츠를 Adobe 액세스 클라이언트로 다시 전송합니다. (Adobe Access 1.x 메타데이터에는 CEK가 포함되어 있지 않습니다.)

   메타데이터를 변환하려면 Adobe Access 1.x 컨텐츠 암호화 키에 액세스해야 합니다. Flash Media Rights Management Server 1.x에서 마이그레이션할 때, LiveCycle ES 데이터베이스에 컨텐츠 암호화 키를 계속 저장하거나, 사용자 정의 솔루션을 구현하여 컨텐츠 암호화 키를 다른 곳에 안전하게 저장할 수 있습니다. LiveCycle ES 데이터베이스에 컨텐츠 암호화 키를 계속 저장하도록 선택하는 경우, LiveCycle ES *에 있는 &quot;데이터베이스의 민감한 컨텐츠에 대한 액세스 보호&quot;에 설명된 권장 사항을 따릅니다.*

Flash 미디어 Rights Management Server 1.x를 사용하여 패키지된 컨텐츠와의 호환성을 보장하는 방법에 대한 자세한 내용은 *Adobe 액세스 API 참조*&#x200B;를 참조하십시오.
