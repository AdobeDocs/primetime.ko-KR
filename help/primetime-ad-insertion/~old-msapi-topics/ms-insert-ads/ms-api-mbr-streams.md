---
description: 광고 삽입에 대한 클라이언트 요청은 일반적으로 변형 M3U8 형식 재생 목록에서 두 개 이상의 비트 전송률을 지정합니다. 매니페스트 서버는 각 비트 전송률에 대해 별도의 M3U8 링크가 포함된 새로운 변형 M3U8 파일을 생성하여 반환합니다. 또한 고유한 그룹 ID를 생성하여 이러한 M3U8을 함께 연결합니다.
title: 여러 비트 전송률 스트림
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 여러 비트 전송률 스트림 {#multiple-bit-rate-streams}

광고 삽입에 대한 클라이언트 요청은 일반적으로 변형 M3U8 형식 재생 목록에서 두 개 이상의 비트 전송률을 지정합니다. 매니페스트 서버는 각 비트 전송률에 대해 별도의 M3U8 링크가 포함된 새로운 변형 M3U8 파일을 생성하여 반환합니다. 또한 고유한 그룹 ID를 생성하여 이러한 M3U8을 함께 연결합니다.

매니페스트 서버는 클라이언트의 Bootstrap URL 요청에 있는 정보를 사용하여 콘텐츠 변형 플레이리스트를 검색합니다. 스트림 수준 콘텐츠에 대한 매니페스트 서버 링크를 포함하는 새 변형 재생 목록을 생성합니다. 클라이언트는 이러한 매개 변수를 사용하여 광고 삽입 요청을 구성합니다. 매니페스트 서버의 스트림 수준 콘텐츠 링크는 다음 형식을 갖습니다.

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** 매니페스트 서버는 콘텐츠의 재생 목록 유형을 기반으로 이 값을 설정합니다. 라이브/선형(#EXT-X-PLAYLIST-TYPE:EVENT) 또는 VOD(#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** Bootstrap URL 요청에 제공된 특정 컨텐츠에 대한 게시자의 고유 ID.

* **`rendition`** 매니페스트 서버는 콘텐츠 스트림의 BANDWIDTH 값을 기반으로 이 값을 설정하고 이를 사용하여 광고의 비트율과 콘텐츠의 비트율을 일치시킵니다. 비트 전송률이 가장 낮은 광고 렌디션이 초과하지 않는 한 광고 비트 전송률은 콘텐츠의 비트 전송률을 초과할 수 없습니다.

* **`groupID`** 매니페스트 서버는 이 값을 생성하여 클라이언트가 요청하는 비트율 렌디션에 관계없이 광고를 일관되게 배치하는 데 사용합니다.

* **`base64-encoded url of the bit rate stream`** 매니페스트 서버 URL-safe base64는 콘텐츠 스트림의 절대 URL을 인코딩합니다. 각 스트림에는 자체 URL이 있습니다.

* **`Query parameters`** Bootstrap URL 요청에 제공된 쿼리 매개 변수입니다.

