---
description: pttrackingmode=simple 또는 ptplayer=ios-mobileweb인 경우, 매니페스트 서버는 클라이언트가 콘텐츠를 설명하는 M3U8 파일을 요청하는 데 사용할 URL인 기본-M3U8이 포함된 JSON 형식의 파일을 다시 보냅니다.
title: 변형 매니페스트 재생 목록 요청을 위한 URL용 JSON 형식
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# 변형 매니페스트 재생 목록 요청을 위한 URL용 JSON 형식 {#json-format-for-url-for-requesting-variant-manifest-playlist}

If `pttrackingmode=simple` 또는 `ptplayer=ios-mobileweb`, 매니페스트 서버는 클라이언트가 콘텐츠를 설명하는 M3U8 파일을 요청하는 데 사용할 URL인 기본-M3U8이 포함된 JSON 형식의 파일을 다시 보냅니다.

다음은 가 포함된 JSON 파일의 형식입니다. `Master-M3U8` URL.

```
{
"Master-M3U8": "https://manifest.auditude.com/auditude/variant/{publisherAssetID}/
  {sessionId}/{Base 64 of the url of the content}.m3u8
  ?u={Ad Request Id}
  &z={Ad Zone Id}
  &pttrackingmode=simple
  &pttrackingversion=v1
  &{other query parameters}"
}
```
