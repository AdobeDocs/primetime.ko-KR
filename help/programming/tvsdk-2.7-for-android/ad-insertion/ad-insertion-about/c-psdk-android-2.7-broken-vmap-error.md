---
description: TVSDK는 광고 서버 응답에서 손상된 VMAP이 발생하면 1109(NETWORK_AD_URL_FAILED) 오류를 발송합니다.
keywords: 1109;NETWORK_AD_URL_FAILED;손상된 VMAP
title: 손상된 VMAP에 대한 클라이언트 오류 처리
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 손상된 VMAP에 대한 클라이언트 오류 처리 {#client-error-handling-for-broken-vmap}

TVSDK는 광고 서버 응답에서 손상된 VMAP이 발생하면 1109(NETWORK_AD_URL_FAILED) 오류를 발송합니다.

광고 서버 응답의 특성 및 광고 로드 설정에 따라 TVSDK에서 광고 서버 응답에 손상된 VMAP이 발생하면 플레이어가 다른 수의 1109 오류를 수신할 수 있습니다.

광고 서버 응답이 VMAP XML을 가리키는 시나리오를 생각해 보겠습니다. 또한 광고 서버 응답에는 각각 동일한 VMAP을 가리키는 4개의 사용 가능한 광고 슬롯이 있다고 가정합니다. 마지막으로 이 VMAP이 깨졌다고 가정해 보겠습니다.

이 시나리오에서는 지연 광고 해결이 활성화된 경우( [지연 광고 해결 활성화](../../../tvsdk-2.7-for-android/ad-insertion/c-psdk-android-2.7-lazy-ad-resolving/t-psdk-android-2.7-enable-lazy-ad-resolving.md)), TVSDK는 두 개의 1109 오류를 발송합니다(예상대로 하나가 아님). 타임라인을 통해 각 구문 분석 전달에 하나의 오류가 발송됩니다. 이는 레이지 광고 확인이 활성화된 경우 TVSDK가 2회 패스로 광고를 구문 분석하기 때문입니다. 첫 번째 패스는 프리롤 광고에 대해 콘텐츠 재생이 시작되기 직전에 발생하고 두 번째 패스는 미드롤 및 포스트롤 광고에 대해 재생이 시작된 후에 발생합니다.

>[!NOTE]
>
>이 시나리오에서 지연 광고 해결을 사용하지 않도록 설정하면 TVSDK에서 1109 오류를 하나만 실행합니다(구문 분석 패스 하나만 실행).
