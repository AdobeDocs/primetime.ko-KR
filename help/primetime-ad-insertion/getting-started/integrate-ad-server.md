---
title: 광고 서버 통합
description: 광고 서버 통합
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 광고 서버 통합 {#integrate-ad-server}

시작하려면 Primetime Ad Insertion 콘솔에 액세스할 수 있는 로그인이 제공됩니다. 이 콘솔에서 Primetime Ad Insertion이 광고 요청을 선택한 광고 서버에 전달하는 데 사용하는 규칙을 설정합니다. Primetime Ad Insertion은 대부분의 VAST 또는 VMAP 호환 광고 서버를 지원합니다.

>[!NOTE]
>
>[IAB VAST 페이지](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast)

## 매크로 지원 {#macro-support}

Primetime Ad Insertion은 모든 스트림에 대해 다음 광고 서버 매크로를 활성화합니다.

* 캐시 무효화
* 애플리케이션 컨텍스트 또는 페이지 URL
* 사용 가능한 기간
* 현재 비디오 자산

추가 매크로가 필요한 경우 Adobe Primetime 지원 담당자에게 문의하십시오.

## 고급 기능 {#advanced-features}

Primetime Ad Insertion은 고급 기능을 활성화하는 규칙 기반 의사 결정도 제공합니다. 인벤토리 권한을 기반으로 다른 광고 서버로 광고를 라우팅하거나 개별 광고에 대한 빈도 제한을 활성화하려는 경우 이 작업이 중요할 수 있습니다. 자세한 내용은 [고급 기능](/help/primetime-ad-insertion/advanced-features/route-ads-based-on-rules.md).
