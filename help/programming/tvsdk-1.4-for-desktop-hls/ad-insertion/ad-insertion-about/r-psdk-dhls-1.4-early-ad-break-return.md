---
description: 라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.
seo-description: 라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.
seo-title: 조기 광고 중단 반품 구현
title: 조기 광고 중단 반품 구현
uuid: 984b6ed0-c929-49a3-9553-e30d1a7758ed
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# 조기 광고 중단 반환 구현{#implementing-an-early-ad-break-return}

라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.

>[!NOTE]
>
>스플라인 아웃/인 광고 마커( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` 및 `#EXT-X-CUE`)에 가입해야 합니다.

고려해야 할 몇 가지 요구 사항은 다음과 같습니다.

* 선형 또는 FER 스트림에 나타나는 `EXT-X-CUE-IN`(또는 상응하는 마커 태그)와 같은 구문 분석 마커

   마커를 광고 초기 반환점에 대한 마커로 등록합니다. 재생하는 동안 이 마커 위치를 지정할 때까지 `adBreaks`만 재생합니다. 이 경우 맨 앞의 `EXE-X-CUE-OUT` 마커로 표시된 `adBreak`의 지속 시간이 재정의됩니다.

* 동일한 `EXT-X-CUE-OUT` 마커에 대해 두 개의 `EXT-X-CUE-IN` 마커가 존재하는 경우 나타나는 첫 번째 `EXT-X-CUE-IN` 마커는 카운트되는 마커입니다.

* `EXE-X-CUE-IN` 마커가 행간 `EXT-X-CUE-OUT` 마커 없이 타임라인에 나타나면 `EXE-X-CUE-IN` 마커가 무시됩니다.

   라이브 스트림에서 행간 `EXT-X-CUE-OUT` 마커가 방금 창 밖으로 이동한 경우 TVSDK가 응답하지 않습니다.

* 광고 중단으로부터 조기 귀환하는 경우 광고 중단이 종료되어야 하는 시점에 재생 헤드가 원래 위치로 돌아가 해당 위치에서 기본 컨텐츠 재생을 재개할 때까지 `adBreak`이 재생됩니다.

## SpliceOut 및 SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 및  `SpliceIn` 마커는 광고 중단의 시작과 끝을 표시합니다. `EXE-X-CUE` 마커의 `SpliceOut` 유형의 지속 시간은 0일 수 있으며 `EXE-X-CUE` 마커의 `SpliceIn` 유형은 광고 중단의 끝을 표시합니다. 태그는 하나의 태그에 나타나며 유형별로 다릅니다.

**유형이 다른 하나의 마커**

예를 들어, 다음은 서로 다른 유형의 마커입니다.

```
#EXTM3U#EXT-X-TARGETDURATION:10
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:44
  
#EXTINF:9.9,
https://server-host/path/file44.ts
#EXTINF:4.2,
https://server-host/path/file45.ts
  
#EXT-X-CUE:TYPE="SpliceOut",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138",AVAIL-NUM="1",AVAILS-EXPECTED="10"
#EXTINF:5.8,
https://server-host/path/file46.ts
#EXTINF:9.9,
https://server-host/path/file47.ts
...
#EXTINF:9.9,
https://server-host/path/file56.ts
#EXTINF:4.2,
https://server-host/path/file57.ts
#EXT-X-CUE:TYPE="SpliceIn",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138"
#EXTINF:9.9,
https://server-host/path/file58.ts
```

유형이 다른 하나의 마커에서 `SpliceOut` 유형의 지속 시간이 0이면 모든 광고 중단에 대해 `SpliceOut` 및 `SpliceIn`이(가) 함께 작업해야 합니다. 현재 길이가 0이 아닌 `SpliceOut` 마커로 `SpliceIn` 마커를 더 일반적으로 연결할 필요가 없습니다.

**두 개의 개별 마커**

더 일반적인 시나리오는 0이 아닌 기간이 있는 `SpliceOut` 마커이며 `SpliceIn` 마커를 연결할 필요가 없습니다. 여기서 `SpliceIn` 마커는 광고 재생 중에 광고 중단의 끝을 표시하지만 광고 나누기는 `SpliceIn` 마커 위치에서 짧게 잘리며, 주 컨텐츠는 이 위치에서 재생됩니다.

예를 들어 두 개의 개별 마커가 있습니다.

```
#EXT-X-CUE-OUT:ID=105,DURATION=30.0,TIME=1081.08
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589090425811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589150485811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589210545811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589270605811,format=m3u8-aapl-v4)
#EXT-X-CUE-IN:ID=105,TIME=1105.104
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589330665811,format=m3u8-aapl-v4)
```

