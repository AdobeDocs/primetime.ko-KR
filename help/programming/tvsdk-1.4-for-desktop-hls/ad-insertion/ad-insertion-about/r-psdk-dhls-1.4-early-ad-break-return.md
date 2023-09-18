---
description: 라이브 스트림 광고 삽입의 경우, 광고 브레이크의 모든 광고가 완료될 때까지 재생되기 전에 광고 브레이크를 종료해야 할 수 있습니다.
title: 조기 광고 브레이크 반환 구현
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# 조기 광고 브레이크 반환 구현{#implementing-an-early-ad-break-return}

라이브 스트림 광고 삽입의 경우, 광고 브레이크의 모든 광고가 완료될 때까지 재생되기 전에 광고 브레이크를 종료해야 할 수 있습니다.

>[!NOTE]
>
>스플라이스 아웃/인 광고 마커에 가입해야 합니다( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, 및 `#EXT-X-CUE`).

다음은 고려해야 할 몇 가지 요구 사항입니다.

* 다음과 같은 마커 구문 분석 `EXT-X-CUE-IN` 선형 또는 FER 스트림에 나타나는 (또는 상응하는 마커 태그).

  마커를 광고 초기 반환점에 대한 마커로 등록합니다. 재생 전용 `adBreaks` 재생 중에 이 마커 위치까지. `adBreak` 행간으로 표시 `EXE-X-CUE-OUT` 마커.

* 2인 경우 `EXT-X-CUE-IN` 마커가 동일한 항목에 존재합니다. `EXT-X-CUE-OUT` 마커, 첫 번째 `EXT-X-CUE-IN` 표시되는 마커가 카운트됩니다.

* 다음과 같은 경우 `EXE-X-CUE-IN` 마커가 타임라인에 행간 없이 표시됨 `EXT-X-CUE-OUT` 마커, `EXE-X-CUE-IN` 마커가 삭제됩니다.

  라이브 스트림에서 앞에 오는 경우 `EXT-X-CUE-OUT` 마커가 창 밖으로 방금 이동했습니다. TVSDK가 이에 응답하지 않습니다.

* 광고 브레이크에서 조기에 돌아오는 경우 `adBreak` 광고 브레이크가 종료되어야 하는 원래 위치로 플레이헤드가 돌아올 때까지 재생하고 해당 위치에서 기본 컨텐츠 재생을 재개합니다.

## SpliceOut 및 SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 및 `SpliceIn` 마커는 광고 브레이크의 시작과 끝을 표시합니다. 기간 `SpliceOut` 유형 `EXE-X-CUE` 마커는 0이고 `SpliceIn` 유형 `EXE-X-CUE` 마커는 광고 브레이크의 끝을 표시합니다. 이 태그는 하나의 태그에 표시되며 유형에 따라 다릅니다.

**유형이 다른 하나의 마커**

예를 들어 유형이 다른 하나의 마커는 다음과 같습니다.

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

다른 유형의 한 마커에서 의 지속 시간이 `SpliceOut` 유형은 0이고, `SpliceOut` 및 `SpliceIn` 광고 브레이크마다 함께 작업해야 합니다. 현재, `SpliceOut` 기간이 0이 아닌 마커이며 연결할 필요가 없습니다. `SpliceIn` 마커가 더 일반적입니다.

**두 개의 개별 마커**

보다 일반적인 시나리오는 다음과 같습니다. `SpliceOut` 기간이 0이 아니고 연결할 필요가 없는 마커 `SpliceIn` 마커. 여기, 연결 `SpliceIn` 마커는 광고 브레이크 재생 중에 광고 브레이크의 끝을 표시하지만 광고 브레이크는 `SpliceIn` 마커 위치이며, 기본 콘텐츠는 이 위치에서 재생을 시작합니다.

예를 들어 두 개의 마커가 서로 구분되어 있습니다.

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
