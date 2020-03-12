---
description: 광고 서버 응답에서 TVSDK가 손상된 VMAP을 발견하면 1109(NETWORK_AD_URL_FAILED) 오류를 전달합니다.
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: 광고 서버 응답에서 TVSDK가 손상된 VMAP을 발견하면 1109(NETWORK_AD_URL_FAILED) 오류를 전달합니다.
seo-title: 손상된 VMAP에 대한 클라이언트 오류 처리
title: 손상된 VMAP에 대한 클라이언트 오류 처리
uuid: ab2c567d-d945-4ebe-b65a-c1f13518a576
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 손상된 VMAP에 대한 클라이언트 오류 처리 {#client-error-handling-for-broken-vmap}

광고 서버 응답에서 TVSDK가 손상된 VMAP을 발견하면 1109(NETWORK_AD_URL_FAILED) 오류를 전달합니다.

광고 서버 응답의 성격과 광고 로딩 설정에 따라 TVSDK가 광고 서버 응답에서 손상된 VMAP을 발견하면 플레이어에서 1109 오류 수를 다르게 수신할 수 있습니다.

광고 서버 응답이 VMAP XML을 가리키는 시나리오를 생각해 보겠습니다. 또한 광고 서버 응답에는 4개의 사용 가능한 광고 슬롯이 있으며 각 슬롯이 동일한 VMAP을 가리킵니다. 마지막으로, 이 VMAP이 고장났다고 합시다.

이 시나리오에서 레이지 광고 해결이 활성화된 경우([레이지 광고 해결](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)활성화), TVSDK는 1109 오류 2개를 전달합니다(예상 오류는 아님).타임라인을 통해 구문 분석 전달될 때마다 하나의 오류가 전달됩니다. 이는 레이지 광고 해결이 활성화되면 TVSDK가 2회 패스로 광고를 구문 분석하기 때문입니다.첫 번째 패스는 프리롤 광고에 대한 컨텐츠 재생이 시작되기 직전에 발생하며 중간 롤 및 포스트롤 광고의 경우 재생 시작 후 두 번째 패스가 발생합니다.

>[!NOTE]
>
>이 시나리오에서 레이지 광고 해결을 비활성화하면 TVSDK에서 1109 오류(구문 분석 패스 하나만)를 하나만 발생합니다.