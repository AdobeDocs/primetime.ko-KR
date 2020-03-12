---
description: 선택적 pttrackingmode, pttrackingversion 및 pttrackingposition 쿼리 매개 변수를 사용하여 현재 비디오에 대한 광고 추적 정보를 전송할 URL을 가져옵니다. 응답은 추적 버전 및 비디오 스트림이 라이브인지 주문형(VOD)인지에 따라 다릅니다.
seo-description: 선택적 pttrackingmode, pttrackingversion 및 pttrackingposition 쿼리 매개 변수를 사용하여 현재 비디오에 대한 광고 추적 정보를 전송할 URL을 가져옵니다. 응답은 추적 버전 및 비디오 스트림이 라이브인지 주문형(VOD)인지에 따라 다릅니다.
seo-title: 매니페스트 서버와 상호 작용할 플레이어용 API
title: 매니페스트 서버와 상호 작용할 플레이어용 API
uuid: ab7a19e7-6c28-4960-a56b-3b33c525e6b3
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# 매니페스트 서버와 상호 작용할 플레이어용 API {#api-for-players-to-interact-with-the-manifest-server}

선택 사항, `pttrackingmode`및 `pttrackingversion``pttrackingposition` 쿼리 매개 변수를 사용하여 현재 비디오에 대한 광고 추적 정보를 전송할 URL을 가져옵니다. 응답은 추적 버전 및 비디오 스트림이 라이브인지 주문형(VOD)인지에 따라 다릅니다.

## 쿼리 매개 변수 {#query-parameters}

|**pttrackingmode**|예:pttrackingmode=simple단순 지정을 사용하면 매니페스트 서버에서 추적 정보를 확인할 수 있습니다.
추적 정보를 요청하기 전에 M3U8을 가져오도록 요청에서 지정합니다.지정하지 않으면 매니페스트 서버가 #EXT-X-MARKER 태그의 추적 정보를 반환합니다.
또는 단순 추적 이외의 유효한 값을 지정하면 서버측 추적이 호출됩니다.

|**pttrackingversion**|예:pttrackingversion=v2이 매개 변수는 추적 정보를 반환하는 데 사용할 형식을 매니페스트 서버에 알려줍니다(파일 형식 [참조](../../msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
추적 정보를 요청하기 전에 M3U8을 가져오도록 요청에서 지정하십시오.이 정보를 지정하지 않거나 잘못된 값을 지정하면 매니페스트 서버에서 v1을 사용합니다.

|**pttrackingposition**|예:pttrackingposition이 매개 변수는 매니페스트 서버에 비디오의 추적 정보를 M3U8 파일에서 JSON 또는 VMAP 개체로 반환하도록 지시합니다.매니페스트 서버는 지정된 값을 무시하고 해당 세션에 대해 가지고 있는 추적 정보를 모두 전송합니다. 값이 전달되지 않으면 매니페스트 서버는 요청된 M3U8 파일을 반환합니다.