---
description: pttrackingmode=simple 또는 ptplayer=ios-mobileweb인 경우 매니페스트 서버는 컨텐트를 설명하는 M3U8 파일을 요청하는 데 사용할 클라이언트의 URL인 기본-M3U8이 포함된 JSON 형식 파일을 다시 전송합니다.
seo-description: pttrackingmode=simple 또는 ptplayer=ios-mobileweb인 경우 매니페스트 서버는 컨텐트를 설명하는 M3U8 파일을 요청하는 데 사용할 클라이언트의 URL인 기본-M3U8이 포함된 JSON 형식 파일을 다시 전송합니다.
seo-title: 변형 매니페스트 재생 목록을 요청하는 URL용 JSON 형식
title: 변형 매니페스트 재생 목록을 요청하는 URL용 JSON 형식
uuid: 9f9693d0-3c93-4555-b20c-7f4576742f41
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 변형 매니페스트 재생 목록 {#json-format-for-url-for-requesting-variant-manifest-playlist} 요청을 위한 URL의 JSON 형식

`pttrackingmode=simple` 또는 `ptplayer=ios-mobileweb`인 경우 매니페스트 서버가 컨텐트를 설명하는 M3U8 파일을 요청하는 데 사용할 클라이언트의 URL인 기본-M3U8이 포함된 JSON 형식 파일을 다시 전송합니다.

이 형식은 `Master-M3U8` URL이 포함된 JSON 파일의 형식입니다.

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
