---
cloud: experience-cloud
product: adobe primetime
audience: end-user
user-guide-title: Primetime Ad Insertion 도움말
user-guide-description: 서버에 사용자 타겟팅된 동적 광고를 삽입하여 컨텐츠를 상용화하고 개인화된 광고를 통해 고객의 참여를 유도하는 방법을 설명합니다.
translation-type: tm+mt
source-git-commit: fac84687085f289e984c189665bfe775337592b3
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 9%

---


# Primetime Ad Insertion Help {#ad-insertion}

+ [Primetime Ad Insertion 개요](home.md)
+ Primetime Ad Insertion 시작하기{#get-started}
   + [개요](get-started-ptai.md)
   + [Primetime Ad Insertion 사용 준비](setup-ptai.md)
   + [광고 서버 통합](integrate-ad-server.md)
   + [CDN 통합](integrate-cdn.md)
   + [라이브/선형 스트림에서 광고 삽입 사용](ad-insertion-live-linear-stream.md)
   + [VOD에 광고 삽입 사용](ad-insertion-vod.md)
   + [광고 추적 설정](set-up-ad-tracking.md)
+ [Primetime Ad Insertion 릴리스 노트](https://docs.adobe.com/content/help/en/primetime/release-notes/ptai/ptai-19x-release-notes.html)
+ [매니페스트 서버 디버깅 도구](manifest-server-debugging-tool.md)

<!-- + [Server Side Ad Insertion debugging dashboard](ssai-debugging-dashboard.md)-->
+ Ad Insertion용 매니페스트 서버 API {#manifest-server}
   + [매니페스트 서버 상호 작용 개요](msapi-topics/ms-overview.md)
   + Manifest Server 시작하기 {#get-started}
      + [매니페스트 서버로 명령 보내기](msapi-topics/ms-getting-started/ms-sending-cmd.md)
      + [매니페스트 서버 쿼리 매개 변수](msapi-topics/ms-getting-started/ms-api-query-params.md)
   + 광고 삽입 요청 {#ad-insert}
      + [광고 삽입 요청](msapi-topics/ms-insert-ads/ms-ad-insert.md)
      + [클라이언트 및 상황별 선택적 쿼리 매개 변수](msapi-topics/ms-insert-ads/ms-api-query-param-situation.md)
      + [페일오버/백업 스트림으로 HLS 플레이어 전환 촉진](msapi-topics/ms-insert-ads/hls-switching-to-failover.md)
      + [다중 비트 전송률 스트림](msapi-topics/ms-insert-ads/ms-api-mbr-streams.md)
      + [부분 광고 중단 삽입](msapi-topics/ms-insert-ads/partial-ad-break-insetion.md)
      + [CRS 광고 전달을 위한 다양한 CDN 지원](msapi-topics/ms-insert-ads/ms-api-multi-cdns-for-crs.md)
   + VOD 타임라인 교체 {#replace-vod}
      + [VOD 변경](msapi-topics/ms-changes-vod-timeline/ms-replace-vod-timeline.md)
      + [VOD 타임라인 포맷](msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)
      + [VOD 타임라인 교체](msapi-topics/ms-changes-vod-timeline/t-ms-replace-vod-timeline.md)
   + 광고 효과 추적 {#ad}
      + [광고 추적](msapi-topics/ms-at-effectiveness/ms-at-overview.md)
      + [클라이언트측 광고 추적 활성화](msapi-topics/ms-at-effectiveness/ms-enable-client-side-ad-tracking.md)
      + [비TVSDK 클라이언트측 추적 개요](msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md)
      + [플레이어가 매니페스트 서버와 상호 작용하는 API](msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)
      + [EXT-X-MARKER Directive](msapi-topics/ms-at-effectiveness/ms-api-playlists.md)
   + [쿠키](msapi-topics/ms-cookies.md)
   + [WebVTT 캡션 지원](msapi-topics/ms-webvtt-captions.md)
   + 파일 포맷 목록 {#list}
      + [파일 포맷](msapi-topics/ms-list-file-formats/ms-api-file-formats.md)
      + [변형 매니페스트 재생 목록을 요청하는 URL용 JSON 형식](msapi-topics/ms-list-file-formats/ms-json-m3u8.md)
      + [URL 추적을 위한 JSON 포맷](msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md)
      + [URL 추적을 위한 VMAP 형식](msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md)
   + [비디오 플레이어 요구 사항](msapi-topics/ms-player-req.md)
+ Primetime 크리에이티브 리패키징 서비스 {#crs}
   + [CRS 개요](creative-repackaging-service/crs-overview.md)
   + [CRS의 주요 사용](creative-repackaging-service/jit-async-hls-conv.md)
   + [다중 CDN 지원](creative-repackaging-service/multi-cdn-supportt.md)
   + [JIT 재패키징을 위한 자세한 워크플로우](creative-repackaging-service/jit-repackage.md)
   + [CRS를 사용하여 ID3 시간 지정 메타데이터 태그 삽입](creative-repackaging-service/inject-id3.md)
   + [API 재패키징](creative-repackaging-service/api-repackage.md)
