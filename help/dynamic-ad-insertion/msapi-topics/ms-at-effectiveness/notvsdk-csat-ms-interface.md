---
description: 선택적 pttrackingmode, pttrackingversion 및 pttrackingposition 쿼리 매개 변수를 사용하여 현재 비디오에 대한 광고 추적 정보를 전송할 URL을 가져옵니다. 응답은 추적 버전과 비디오 스트림이 실시간 또는 주문형(VOD)인지 여부에 따라 다릅니다.
seo-description: 선택적 pttrackingmode, pttrackingversion 및 pttrackingposition 쿼리 매개 변수를 사용하여 현재 비디오에 대한 광고 추적 정보를 전송할 URL을 가져옵니다. 응답은 추적 버전과 비디오 스트림이 실시간 또는 주문형(VOD)인지 여부에 따라 다릅니다.
seo-title: 플레이어가 매니페스트 서버와 상호 작용하는 API
title: 플레이어가 매니페스트 서버와 상호 작용하는 API
uuid: ab7a19e7-6c28-4960-a56b-3b33c525e6b3
translation-type: tm+mt
source-git-commit: 32a7901e3061cca03f1f1fa5ab06f5bb950d248a
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# 플레이어가 매니페스트 서버 {#api-for-players-to-interact-with-the-manifest-server}과(와) 상호 작용하기 위한 API

현재 비디오에 대한 광고 추적 정보를 보낼 URL을 얻으려면 선택적 `pttrackingmode`, `pttrackingversion` 및 `pttrackingposition` 쿼리 매개 변수를 사용하십시오. 응답은 추적 버전과 비디오 스트림이 실시간 또는 주문형(VOD)인지 여부에 따라 다릅니다.

## 쿼리 매개 변수 {#query-parameters}

**pttrackingmode**
예:pttrackingmode=simple을 지정하면 매니페스트 서버에서 추적 정보를 확인할 수 있습니다.
추적 정보를 요청하기 전에 M3U8을 가져오기 위한 요청에 지정합니다.지정하지 않으면 매니페스트 서버가 #EXT-X-MARKER 태그의 추적 정보를 반환합니다.
또는 단순 서버 측 추적 이외의 유효한 값을 지정하면 호출됩니다.

**pttrackingversion**
예:pttrackingversion=v2 이 매개 변수는 추적 정보를 반환하는 데 사용할 형식을 매니페스트 서버에 알려줍니다( [파일 형식 참조](../../msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
추적 정보를 요청하기 전에 M3U8을 가져오기 위한 요청에 지정합니다.이 정보를 지정하지 않거나 잘못된 값을 지정하면 매니페스트 서버에서 v1을 사용합니다.

**pttrackingposition**
예:pttrackingposition 이 매개 변수는 매니페스트 서버에 비디오의 추적 정보를 M3U8 파일에서 JSON 또는 VMAP 개체로 반환하도록 알려줍니다. 매니페스트 서버는 지정된 값을 무시하고 해당 세션에 대해 가지고 있는 모든 추적 정보를 전송합니다. 값이 전달되지 않으면 매니페스트 서버가 요청된 M3U8 파일을 반환합니다.
