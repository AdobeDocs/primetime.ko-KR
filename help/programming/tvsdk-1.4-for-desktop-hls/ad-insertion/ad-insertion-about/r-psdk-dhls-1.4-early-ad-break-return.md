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


# 조기 광고 중단 반품 구현{#implementing-an-early-ad-break-return}

라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.

>[!NOTE]
>
>스플릿 아웃/인 광고 마커(, `#EXT-X-CUE-OUT`및 `#EXT-X-CUE-IN``#EXT-X-CUE`)를 구독해야 합니다.

고려해야 할 몇 가지 요구 사항은 다음과 같습니다.

* 선형 또는 FER 스트림에 나타나는 `EXT-X-CUE-IN` (또는 상응하는 마커 태그)와 같은 구문 분석 마커

   마커를 광고 초기 반환점에 대한 마커로 등록합니다. 재생하는 동안 이 마커 위치 `adBreaks` 가 될 때까지 재생할 수 있으며, 이렇게 되면 행간 `adBreak` `EXE-X-CUE-OUT` 마커로 표시된 지속 시간이 재정의됩니다.

* 동일한 마커에 두 `EXT-X-CUE-IN` 개의 마커가 `EXT-X-CUE-OUT` 있는 경우 나타나는 첫 번째 `EXT-X-CUE-IN` 마커는 카운트되는 마커입니다.

* 타임라인에 `EXE-X-CUE-IN` 선행 `EXT-X-CUE-OUT` 마커가 없는 마커가 나타나면 `EXE-X-CUE-IN` 마커가 무시됩니다.

   라이브 스트림에서는 행간 `EXT-X-CUE-OUT` 표시자가 창 밖으로 이동된 경우 TVSDK가 응답하지 않습니다.

* 광고 중단에서 일찍 돌아오는 경우 광고 중단이 종료되어야 할 때 재생 헤드가 원래 위치로 돌아가 해당 위치에서 주요 컨텐츠 재생을 다시 시작할 때까지 `adBreak` 재생됩니다.

## SpliceOut 및 SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 및 `SpliceIn` 마커는 광고 중단의 시작과 끝을 표시합니다. 마커 `SpliceOut` 유형 `EXE-X-CUE` 의 지속 시간은 0일 수 있으며 마커 `SpliceIn` `EXE-X-CUE` 유형은 광고 분류의 끝을 표시합니다. 태그는 하나의 태그에 나타나며 유형별로 다릅니다.

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

유형이 다른 하나의 마커에서 유형 기간이 0이면 모든 광고 나누기에 대해 `SpliceOut` 와 `SpliceOut` `SpliceIn` 함께 작업해야 합니다. 현재 지속 시간이 0이 `SpliceOut` 아닌 마커로 연결 마커가 필요하지 않은 `SpliceIn` 경우가 더 일반적입니다.

**두 개의 개별 마커**

더 일반적인 시나리오는 0이 아닌 기간이 있는 마커이며 연결 마커가 필요하지 `SpliceOut` `SpliceIn` 않습니다. 여기에 연결 `SpliceIn` `SpliceIn` 마커는 광고 중단 재생 중에 광고 중단의 끝을 표시하지만, 광고 나누기는 마커 위치에서 짧게 잘리며, 주 컨텐츠는 이 위치에서 재생됩니다.

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

