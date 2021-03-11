---
description: TVSDK에서 광고 서버 응답에서 VMAP이 손상되면 1109(NETWORK_AD_URL_FAILED) 오류를 전달합니다.
keywords: 1109;NETWORK_AD_URL_FAILED;손상된 VMAP
title: 손상된 VMAP에 대한 클라이언트 오류 처리
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 손상된 VMAP {#client-error-handling-for-broken-vmap}에 대한 클라이언트 오류 처리

TVSDK에서 광고 서버 응답에서 VMAP이 손상되면 1109(NETWORK_AD_URL_FAILED) 오류를 전달합니다.

광고 서버 응답의 성격에 따라, 그리고 광고 로드 설정에 따라, TVSDK에서 광고 서버 응답에서 손상된 VMAP이 발견되면 플레이어에서 1109 오류가 다르게 발생할 수 있습니다.

광고 서버 응답이 VMAP XML을 가리키는 시나리오를 생각해 보겠습니다. 또한 광고 서버 응답에는 4개의 사용 가능한 광고 슬롯이 있으며 각 슬롯이 동일한 VMAP을 가리킵니다. 마지막으로, 이 VMAP이 깨졌다고 합시다.

이 시나리오에서, 레이지 광고 해제가 활성화되어 있는 경우([레이지 광고 해결 활성화](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)), TVSDK는 2개의 1109 오류(예상된 오류 없음)를 전달합니다.타임라인을 통해 각 구문 분석 전달에 하나의 오류가 전달됩니다. 레이지 광고 해제가 활성화되면 TVSDK가 2회 패스로 광고를 구문 분석하기 때문입니다.첫 번째 패스는 프리롤 광고에 대한 컨텐츠 재생이 시작되기 직전에 일어나며, 중간 롤 및 포스트롤 광고의 경우 재생 시작 후 두 번째 패스가 발생합니다.

>[!NOTE]
>
>이 시나리오에서 레이지 광고 해결을 비활성화하는 경우 TVSDK는 1109 오류를 하나만 발생시킵니다(구문 분석 패스 하나만).