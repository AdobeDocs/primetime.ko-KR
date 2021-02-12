---
description: 발행자는 Primetime 매니페스트 서버 클라이언트측 광고 추적 워크플로우와 연동되는 HLS 호환 비디오 플레이어를 제작할 수 있습니다. 실시간 스트림 및 VOD(Video On Demand) 케이스의 매니페스트 서버에 대한 인터페이스는 약간 다릅니다.
seo-description: 발행자는 Primetime 매니페스트 서버 클라이언트측 광고 추적 워크플로우와 연동되는 HLS 호환 비디오 플레이어를 제작할 수 있습니다. 실시간 스트림 및 VOD(Video On Demand) 케이스의 매니페스트 서버에 대한 인터페이스는 약간 다릅니다.
seo-title: 비 TVSDK 클라이언트측 추적 개요
title: 비 TVSDK 클라이언트측 추적 개요
uuid: fb23be01-3327-443d-82c4-fb0993e7fec1
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---


# 비 TVSDK 클라이언트측 추적 개요 {#overview-of-non-tvsdk-client-side-tracking}

발행자는 Primetime 매니페스트 서버 클라이언트측 광고 추적 워크플로우와 연동되는 HLS 호환 비디오 플레이어를 제작할 수 있습니다. 실시간 스트림 및 VOD(Video On Demand) 케이스의 매니페스트 서버에 대한 인터페이스는 약간 다릅니다.

매니페스트 서버는 API를 제공하여 사용자 지정 플레이어에서 광고 추적 이벤트를 보고하는 데 사용할 수 있는 다음 URL을 요청할 수 있도록 합니다.

* 광고 노출 수
* 광고 사분위수
* 광고 창 진행
* 콘텐트 창 진행

매니페스트 서버 API는 해당 서버를 사용하는 모든 비디오 플레이어가 최소 요구 사항을 충족한다고 가정합니다. 자세한 내용은 [비디오 플레이어 요구 사항](/help/primetime-ad-insertion/~old-msapi-topics/ms-player-req.md)을 참조하십시오.

## 클라이언트측 추적 워크플로 {#section_cst_flow}

![](assets/pt_ssai_notvsdk_csat_ai-workflow.png)

1. 플레이어는 게시자에서 매니페스트 서버 URL을 가져옵니다.
1. 플레이어는 광고 삽입 요구 사항에 맞는 쿼리 매개 변수를 추가하고 HTTP GET 요청을 결과 Bootstrap URL에 보냅니다. Bootstrap URL에는 다음 구문이 있습니다.

   ```URL
   http{s}://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{urlSafeBase64({Content URL})}.m3u8?{query parameters}
   ```

   예:

   ```URL
   https://manifest.auditude.com/auditude/variant/
   7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.m3u8?
   u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2&__sid__=docExample02
   ```

   URL에는 [매니페스트 서버에 명령 보내기](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-sending-cmd.md)에 설명된 요소가 포함되어 있습니다.

1. 매니페스트 서버가 해당 플레이어에 대한 세션을 설정하고 고유한 세션 ID를 생성합니다. 새 변형 M3U8 재생 목록 URL을 만들어 플레이어에 JSON 응답으로 반환합니다. JSON에는 다음 구문이 있습니다.

   ```JSON
   {
    "Master-M3U8": "https://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{SessionID}/
       {urlSafeBase64(content URL)}.m3u8?u={Asset ID}&z={Zone ID}&pttrackingmode=simple&pttrackingversion=v2
       &{Any other query parameters}"
   }
   ```

   예:

   ```JSON
   https://pcor3.manifest.auditude.com/auditude/variant/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. 플레이어는 JSON 응답의 URL을 사용하여 매니페스트 서버에서 새 변형 M3U8 마스터 재생 목록을 요청합니다.

1. 매니페스트 서버는 다음과 유사한 구문을 갖는 스트림 수준 재생 목록 URL이 포함된 새 변형 M3U8을 반환합니다.

   ```URL
   http{s}://{manifest-server:port}/auditude/{live|vod}/{PublisherAssetID}/
     {rendition}/{groupID}/{urlSafeBase64(bit rate stream URL)}.m3u8?u={Ad Request Id}&z={Ad Zone Id}&{Any other query parameters}
   ```

   예:

   ```URL
   #EXTM3U
   #EXT-X-VERSION:5
   #EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,DEFAULT=YES,FORCED=NO,LANGUAGE="eng",URI="https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/webvtt/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvd2VidnR0L1RPUy1lbjIubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2"
   #EXT-X-STREAM-INF:BANDWIDTH=10000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/10000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTAwMDAvdG9jXzEwMDAwLm0zdTg.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=1300000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/1300/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTMwMC90b2NfMTMwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=3400000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/3400/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMzQwMC90b2NfMzQwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=2100000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/2100/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMjEwMC90b2NfMjEwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=800000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/800/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvODAwL3RvY184MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=5000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/5000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwMC90b2NfNTAwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=7500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/7500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNzUwMC90b2NfNzUwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. 플레이어는 광고 스티칭된 내용을 재생하기 위해 적절한 단일 비트 전송률, 스트림 수준 매니페스트 URL을 선택합니다. 예:

   ```URL
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. 매니페스트 서버는 콘텐츠 및 광고 TS 세그먼트 링크에 대한 링크가 포함된 스트림 수준 매니페스트를 반환합니다. 예:

   ```
      #EXTM3U
   #EXT-X-VERSION:3
   #EXT-X-TARGETDURATION:8
   #EXT-X-PLAYLIST-TYPE:VOD
   
   #EXT-X-DISCONTINUITY
   #EXTINF:8,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00001.ts
   #EXTINF:7,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00002.ts
   
   #EXT-X-DISCONTINUITY
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.0.ts
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.4000.ts
   #EXTINF:4.833,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.8000.ts   
   ```

   >[!NOTE]
   >
   >플레이어가 스트림 수준 재생 목록 URL을 선택하여 콘텐츠 스트림을 받습니다. 매니페스트 서버는 CDN에서 원래 재생 목록을 검색합니다. 일부 인코더에서는 다음과 같이 `#EXTINF` title 속성에 추가 세부 사항을 삽입할 수 있습니다.
   >
   >
   ```
   >#EXTINF:6.006,LTC=2017-08-23T13:25:47+00:00
   >```

   매니페스트 서버는 비표준 속성의 의미를 유추하여 광고를 스티칭하는 재생 목록에 대해 수정할 수 없으므로 매니페스트 서버는 이 태그의 지속 시간 정보를 제외한 모든 추가 특성을 제거합니다. 자세한 내용은 HLS 사양의 [EXTINF](https://tools.ietf.org/html/rfc8216#section-4.3.2.1) 항목을 참조하십시오.

1. 추적 정보를 요청하기 위해 플레이어는 선택한 비트 전송률의 스트림 수준 재생 목록 URL에 영숫자 값이 있는 쿼리 매개 변수 `pttrackingposition`을 추가합니다. 예:

   ```URL
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d
   &z=173475&pttrackingmode=simple&pttrackingversion=v2&pttrackingposition=1
   ```

1. 매니페스트 서버는 현재 요청한 스트림 수준 m3u8 파일의 광고 추적 데이터를 포함하는 [JSON](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md) 또는 [VMAP](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md) 객체로 채워진 재생 목록 파일을 반환합니다.

   >[!NOTE]
   >
   >매니페스트 서버는 광고가 현재 요청된 스트림 수준 재생 목록에 삽입된 경우에만 광고 추적 개체를 생성합니다. 플레이어가 삽입된 광고를 포함하지 않는 재생 목록을 재생하는 경우 매니페스트 서버는 광고 추적 재생 목록 요청에 대한 HTTP 상태 201을 반환합니다. 플레이어가 재생되지 않는 스트림에 대해 광고 추적 요청을 하면 매니페스트 서버는 HTTP 상태 500을 반환합니다. 예를 들어 현재 재생 요청이 500.m3u8인 경우 매니페스트 서버는 광고 추적 요청에 대해 500.m3u8의 JSON|VMAP을 반환합니다. 그러나 이후에 플레이어에서 스트림을 전환하여 800.m3u8을 재생하면 500.m3u8의 광고 추적 정보가 유효하지 않아 404 오류가 발생합니다.

   >[!NOTE]
   >
   >매니페스트 서버는 Bootstrap URL의 `pttrackingversion` 값을 기반으로 광고 추적 개체를 생성합니다. `pttrackingversion`이(가) 생략되거나 잘못된 값이 있는 경우 매니페스트 서버는 요청된 각 스트림 수준 재생 목록에서 `#EXT-X-MARKER` 태그의 광고 추적 정보를 자동으로 채웁니다. 자세한 내용은 [을(를) 참조하십시오](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md).

1. 플레이어는 적절한 시간에 각 광고 추적 이벤트에 대해 각 광고 추적 URL을 요청합니다.

>[!NOTE]
>
>라이브 스트림의 경우 Packager가 라이브 이벤트가 진행되는 동안 재생 목록을 지속적으로 업데이트하므로 Live Stream의 경우 6단계부터 10단계까지 반복합니다.

비디오가 재생되면 플레이어는 재생 헤드 위치를 추적하고 Primetime 광고 삽입에서 받은 추적 URL과 함께 이 위치를 사용해야 합니다. 추적 URL은 재생 시작으로부터 시간 오프셋으로 그룹화됩니다. 각 시간 오프셋에 대해 추적 정보를 전송할 각 광고 시스템에 대한 URL이 있습니다. 형식에 대한 자세한 내용은 라이브 비디오와 VOD(Video On Demand)를 통해 다릅니다.