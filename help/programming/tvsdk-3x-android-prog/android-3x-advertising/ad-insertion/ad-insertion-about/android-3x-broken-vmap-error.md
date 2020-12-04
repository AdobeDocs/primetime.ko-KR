---
description: TVSDK에서 광고 서버 응답에서 손상된 VMAP이 발생하면 1109(NETWORK_AD_URL_FAILED) 오류를 전달합니다.
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: TVSDK에서 광고 서버 응답에서 손상된 VMAP이 발생하면 1109(NETWORK_AD_URL_FAILED) 오류를 전달합니다.
seo-title: 손상된 VMAP에 대한 클라이언트 오류 처리
title: 손상된 VMAP에 대한 클라이언트 오류 처리
uuid: ab2c567d-d945-4ebe-b65a-c1f13518a576
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# 손상된 VMAP {#client-error-handling-for-broken-vmap}에 대한 클라이언트 오류 처리

TVSDK에서 광고 서버 응답에서 손상된 VMAP이 발생하면 1109(NETWORK_AD_URL_FAILED) 오류를 전달합니다.

광고 서버 응답의 성격과 광고 로드 설정에 따라, TVSDK에서 광고 서버 응답에서 손상된 VMAP이 발견되면 플레이어에서 1109 오류가 다르게 발생할 수 있습니다.

광고 서버 응답이 VMAP XML을 가리키는 시나리오를 생각해 보겠습니다. 또한 광고 서버 응답에는 4개의 사용 가능한 광고 슬롯이 있으며 각 슬롯이 동일한 VMAP을 가리킵니다. 마지막으로, 이 VMAP이 깨졌다고 합시다.

이 시나리오에서, 레이지 광고 해제가 활성화된 경우([레이지 광고 해결 활성화](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)), TVSDK는 1109 오류 2개를 발송합니다(예상했던 오류 한 개가 아님).타임라인을 통해 각 구문 분석 전달에 하나의 오류가 전달됩니다. 이 문제는 레이지 광고 해결이 활성화되면 TVSDK가 2회 패스로 광고를 구문 분석하기 때문입니다.첫 번째 패스는 프리롤 광고에 대한 컨텐츠 재생이 시작되기 직전에 일어나며, 중간 롤 및 포스트롤 광고의 경우 두 번째 패스가 재생 시작 후 발생합니다.

>[!NOTE]
>
>이 시나리오에서, 레이지 광고 해결을 비활성화하면 TVSDK에서 1109 오류가 하나만 발생합니다(구문 분석 패스는 하나만).