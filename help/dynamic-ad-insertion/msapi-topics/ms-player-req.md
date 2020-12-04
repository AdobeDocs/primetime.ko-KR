---
description: 모든 비디오 플레이어는 매니페스트 서버가 광고를 삽입하고 광고 추적을 활성화하는 데 사용하는 기능을 제공해야 합니다.
seo-description: 모든 비디오 플레이어는 매니페스트 서버가 광고를 삽입하고 광고 추적을 활성화하는 데 사용하는 기능을 제공해야 합니다.
seo-title: 비디오 플레이어 요구 사항
title: 비디오 플레이어 요구 사항
uuid: 29593d67-2901-4d9e-a08f-23c8a7667283
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# 비디오 플레이어 요구 사항 {#video-player-requirements}

모든 비디오 플레이어는 매니페스트 서버가 광고를 삽입하고 광고 추적을 활성화하는 데 사용하는 기능을 제공해야 합니다.

Primetime 광고 삽입 API를 사용하려면 비디오 플레이어가 다음을 충족해야 합니다.

* 컨텐츠가 재생될 때 재생 헤드 위치를 추적할 수 있습니다.
* 지정된 시간에 추적 URL을 요청할 수 있습니다.
* 다음을 포함하여 HLS v3 이상을 지원하는 장치 플랫폼에서 실행됩니다.

   * `EXT-X-DISCONTINUITY` 태그로 표시된 PTS 불연속성
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* HTTP 리디렉션 및 JSON 구문 분석을 지원하는 플랫폼에서 실행됩니다.
* CORS를 지원하는 플랫폼에서 실행됩니다.