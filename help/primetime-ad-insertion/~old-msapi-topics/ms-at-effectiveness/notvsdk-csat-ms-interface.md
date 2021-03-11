---
description: 선택적 pttrackingmode, pttrackingversion 및 pttrackingposition 쿼리 매개 변수를 사용하여 현재 비디오에 대한 광고 추적 정보를 보낼 URL을 가져옵니다. 응답은 추적 버전과 비디오 스트림이 실시간 또는 주문형(VOD)인지 여부에 따라 다릅니다.
title: 플레이어가 매니페스트 서버와 상호 작용할 수 있는 API
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# 플레이어가 매니페스트 서버 {#api-for-players-to-interact-with-the-manifest-server}와 상호 작용할 수 있는 API

선택 사항인 `pttrackingmode`, `pttrackingversion` 및 `pttrackingposition` 쿼리 매개 변수를 사용하여 현재 비디오에 대한 광고 추적 정보를 보낼 URL을 가져옵니다. 응답은 추적 버전과 비디오 스트림이 실시간 또는 주문형(VOD)인지 여부에 따라 다릅니다.

## 쿼리 매개 변수 {#query-parameters}

**pttrackingmode**

예:`pttrackingmode=simple`
단순 지정은 추적 정보를 원하는 매니페스트 서버에 알립니다.
추적 정보를 요청하기 전에 M3U8을 가져오도록 요청에 지정합니다.지정하지 않으면 매니페스트 서버가 #EXT-X-MARKER 태그의 추적 정보를 반환합니다.
또는 단순 추적 이외의 유효한 값을 지정하면 서버측 추적이 호출됩니다.

**pttrackingversion**

예:`pttrackingversion=v2`
이 매개 변수는 추적 정보를 반환하는 데 사용할 형식을 매니페스트 서버에 알려줍니다([파일 형식](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md) 참조).
추적 정보를 요청하기 전에 M3U8을 가져오도록 요청에서 지정하십시오.이 정보를 지정하지 않거나 잘못된 값을 지정하면 매니페스트 서버에서 v1을 사용합니다.

**pttrackingposition**

예:`pttrackingposition`
이 매개 변수는 매니페스트 서버에 비디오의 추적 정보를 M3U8 파일에서 JSON 또는 VMAP 개체로 반환하도록 지시합니다. 매니페스트 서버는 지정된 값을 무시하고 해당 세션에 대해 가지고 있는 추적 정보를 모두 전송합니다. 값이 전달되지 않으면 매니페스트 서버가 요청된 M3U8 파일을 반환합니다.
