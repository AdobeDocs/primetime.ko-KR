---
description: 매니페스트 서버는 모든 HLS 비디오 형식에 대해 게시자가 활성화된 WebVTT 캡션을 지원합니다. WebVTT 캡션 컨텐츠에 광고를 삽입하라는 요청을 받으면 올바르게 됩니다.
seo-description: 매니페스트 서버는 모든 HLS/DASH 비디오 형식에 대해 게시자가 활성화된 WebVTT 캡션을 지원합니다. WebVTT 캡션 컨텐츠에 광고를 삽입하라는 요청을 받으면 올바르게 됩니다.
seo-title: WebVTT 캡션 지원
title: WebVTT 캡션 지원
uuid: 1dc728b0-5aeb-4c48-8f3b-54ff4b135742
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# WebVTT 캡션 지원 {#support-for-webvtt-captions}

매니페스트 서버는 HLS/DASH 비디오 형식에 대해 게시자가 활성화된 WebVTT 캡션을 지원합니다. WebVTT 캡션 컨텐츠에 광고를 삽입하라는 요청을 받으면 올바르게 됩니다.

게시자가 컨텐츠에 WebVTT 캡션을 포함하는 경우 매니페스트 서버는 캡션이 있는 콘텐츠 스트림을 클라이언트에 전송합니다. 매니페스트 서버에서 캡션을 지원하려면 WebVTT를 게시자가 활성화해야 합니다. 클라이언트가 WebVTT 캡션을 사용하도록 설정하고 매니페스트 서버에 요청을 보내면 매니페스트 서버는 타임라인 및 WebVTT 트랙을 조작하고 연결된 광고 및 캡션이 포함된 콘텐츠를 클라이언트에 반환합니다.

VOD 컨텐츠 스트림에 대한 워크플로우는 다음과 같습니다.

1. 클라이언트는 WebVTT 캡션이 활성화된 콘텐츠 스트림을 매니페스트 서버로 보냅니다.
1. 매니페스트 서버가 광고를 콘텐츠 스트림에 연결하도록 타임라인을 조작합니다.
1. 매니페스트 서버는 WebVTT 트랙을 조작하여 콘텐츠(광고 포함)에 캡션을 추가합니다.
1. 매니페스트 서버는 삽입된 광고 및 캡션과 함께 콘텐츠 스트림을 클라이언트에 전달합니다.

>[!NOTE]
>
>WebVTT 캡션 세그먼트가 중간 롤 광고 내에 있으면 뷰어에는 해당 중간 롤 광고 중단 전후에 해당 캡션이 재생되는 것을 볼 수 있습니다. 예를 들어 10초 캡션 세그먼트에 30초 중롤 광고가 5초 점에 표시되면 뷰어는 중간 롤 광고 중단 5초 전에 그리고 중간 롤 후 5초 동안 해당 캡션 세그먼트를 표시합니다.

>[!NOTE]
>
>클라이언트가 비디오가 영어와 같은 특정 언어로 재생되도록 요청한 다음 비디오를 프랑스어로 재생하도록 요청하는 경우 매니페스트 서버는 클라이언트가 언어를 프랑스어로 변경하도록 요청했음을 감지할 수 없습니다. 클라이언트가 매니페스트 서버와 통신할 수 없으므로 매니페스트 서버는 광고의 M3U8 마스터 파일에 지정된 첫 번째 언어를 사용하여 광고 캡션을 비디오 스트림에 삽입합니다.