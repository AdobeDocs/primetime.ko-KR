---
title: Adobe Primetime Ad Insertion 시작
description: Adobe Primetime Ad Insertion 시작하기
exl-id: 629ea2a5-1b50-4451-a478-95d02f192145
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Adobe Primetime Ad Insertion 시작 {#ptai-get-started}

Primetime Ad Insertion은 콘텐츠 및 광고를 제공하는 시스템을 조정하여 개인화된 스트림 내 광고 경험을 만든 다음 광고주를 위해 광고 재생을 추적합니다.

Primetime Ad Insertion은 비디오 매니페스트를 다시 작성하여 비디오 게재 클라이언트 애플리케이션과 상호 작용하여 각 뷰어에 대해 타깃팅된 광고 및 개인화된 경험을 제공합니다. 이러한 매니페스트는 광고 서버에서 제공되는 콘텐츠와 광고를 결합하고, 필요한 경우 자세한 광고 추적 지침을 포함하는 메타데이터를 포함할 수 있습니다. Primetime Ad Insertion은 클라이언트측과 서버측 광고 추적을 모두 지원합니다.

시스템이 제대로 설정되면 일반적인 워크플로우는 다음과 같이 표시될 수 있습니다.

1. 클라이언트 응용 프로그램은 [BOOTSTRAP URL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) 비디오 스트림에 대한 정보를 사용하여 GET 요청을 Primetime Ad Insertion에 보냅니다.  Primetime Ad Insertion은 다양한 광고 시그널링 포맷으로 HLS 및 DASH를 지원합니다.

1. Primetime Ad Insertion은 게시자의 CDN에서 클라이언트 애플리케이션으로 콘텐츠 매니페스트를 다시 전송하여 응답합니다.

1. 클라이언트 애플리케이션은 생성된 매니페스트에서 재생할 적절한 스트림을 선택하고 Primetime Ad Insertion에 요청합니다.

1. Primetime Ad Insertion은 컨텐츠 CDN에서 요청된 스트림을 가져오고, 모든 큐 정보를 구문 분석/읽고, 광고 서버를 호출하고, 필요에 따라 광고 브레이크를 바꿉니다.

1. Primetime Ad Insertion은 리소스 URL을 다시 작성하고 광고 크리에이티브에 코드 변환이 필요한지 여부를 감지하여 매니페스트를 정규화합니다. 를 참조하십시오. [Just-in-time 광고 트랜스코딩](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md).

1. Primetime Ad Insertion은 필요한 광고 크리에이티브를 가져오고 적절한 조각을 매니페스트에 삽입합니다.

1. Primetime Ad Insertion은 광고를 포함하여, 결합된 최종 매니페스트를 재생을 위해 클라이언트 애플리케이션에 전달합니다.

1. 광고 게재 및 가시성은 클라이언트 또는 서버측 광고 추적을 통해 측정할 수 있습니다. 다음을 참조하십시오. [광고 추적 설정](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md).

Primetime Ad Insertion은 대부분의 HLS/DASH 클라이언트 및 플레이어 구성을 지원합니다. 지원되는 특정 광고 신호 형식에 대한 자세한 내용은 을 참조하십시오. [지원되는 큐 형식](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md).
