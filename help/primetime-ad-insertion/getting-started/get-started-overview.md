---
title: Adobe Primetime Ad Insertion 시작하기
description: Adobe Primetime Ad Insertion 시작하기
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Adobe Primetime Ad Insertion {#ptai-get-started} 시작하기

Primetime Ad Insertion은 개인화된 인스트림 광고 경험을 만든 다음 광고업체를 위해 광고 재생을 추적하는 컨텐츠와 광고를 제공하는 시스템을 공동으로 재구성합니다.

Primetime Ad Insertion은 각 뷰어에 타겟팅된 광고와 개인화된 경험을 제공하기 위해 비디오 매니페스트를 다시 작성하여 비디오 전달 클라이언트 애플리케이션과 상호 작용합니다. 이러한 매니페스트는 광고 서버에서 제공되는 컨텐츠와 광고를 결합하며 선택적으로 자세한 광고 추적 지침을 포함하는 메타데이터를 포함할 수 있습니다. Primetime Ad Insertion은 클라이언트측과 서버측 광고 추적을 모두 지원합니다.

시스템이 제대로 설정되면 일반적인 워크플로우는 다음과 같이 표시됩니다.

1. 클라이언트 응용 프로그램은 비디오 스트림에 대한 정보가 포함된 [Bootstrap URL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)을 생성하고 GET 요청을 Primetime Ad Insertion에 보냅니다.  Primetime Ad Insertion은 다양한 광고 신호 포맷으로 HLS 및 DASH를 지원합니다.

1. Primetime Ad Insertion은 발행자의 CDN에서 콘텐츠 매니페스트를 클라이언트 애플리케이션으로 다시 전송함으로써 응답합니다.

1. 클라이언트 응용 프로그램은 생성된 매니페스트의 적절한 스트림을 선택하여 재생하고 Primetime Ad Insertion에 대한 요청을 만듭니다.

1. Primetime Ad Insertion은 요청된 스트림을 컨텐츠 CDN에서 가져오고, 큐 정보를 구문 분석/읽고, 광고 서버를 호출하며, 필요에 따라 광고 차단 기능을 대체합니다.

1. Primetime Ad Insertion은 리소스 URL을 다시 작성하고 광고 크리에이티브가 트랜스코딩해야 하는지 여부를 확인하여 매니페스트를 정규화합니다. [Just-in-time 광고 트랜스코딩](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md)을 참조하십시오.

1. Primetime Ad Insertion은 필요한 광고 크리에이티브를 가져오고 해당 조각을 매니페스트에 삽입합니다.

1. Primetime Ad Insertion은 광고를 포함한 최종 연결된 매니페스트를 클라이언트 애플리케이션에 재생하기 위해 전달합니다.

1. 광고 전달 및 보기 기능은 클라이언트 또는 서버측 광고 추적을 통해 측정할 수 있습니다. [광고 추적 설정](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md)을 참조하십시오.

Primetime Ad Insertion은 대부분의 HLS/DASH 클라이언트 및 플레이어 구성을 지원합니다. 지원되는 특정 광고 신호 형식에 대한 자세한 내용은 [지원되는 큐 형식](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md)을 참조하십시오.
