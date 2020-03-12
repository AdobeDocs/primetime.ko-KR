---
description: TV SDK를 가장 효과적으로 사용하려면 구체적인 운영 사항을 고려하고 특정 모범 사례를 따라야 합니다.
seo-description: TV SDK를 가장 효과적으로 사용하려면 구체적인 운영 사항을 고려하고 특정 모범 사례를 따라야 합니다.
seo-title: 고려 사항 및 우수 사례
title: 고려 사항 및 우수 사례
uuid: 62a5d641-6f37-4e4d-bbc2-414bf3681d9c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 고려 사항 및 우수 사례{#considerations-and-best-practices}

TV SDK를 가장 효과적으로 사용하려면 구체적인 운영 사항을 고려하고 특정 모범 사례를 따라야 합니다.

## 고려 사항 {#section_tvsdk_considerations}

TVSDK 사용 시 다음 정보를 기억하십시오.

* Adobe Primetime은 에뮬레이터 또는 시뮬레이터에서는 작동하지 않습니다.

   테스트에 실제 디바이스를 사용해야 합니다.
* 재생은 HLS(HTTP Live Streaming) 컨텐츠에만 지원됩니다.
* 비디오 및 오디오 스트림이 동일한 변환에 있거나, 비디오 및 오디오 스트림이 별도의 변환에 있는 경우 기본 비디오 컨텐츠를 멀티플렉싱할 수 있습니다.
* TVSDK API는 ActionScript에서 구현됩니다.
* 비디오를 재생하려면 AVE(Adobe Video Engine)가 필요합니다. 이는 미디어 리소스에 액세스할 수 있는 방법과 시기에 영향을 줍니다.

   * 자막은 AVE에서 제공하는 범위까지 지원됩니다.
   * 인코더 정밀도에 따라 실제 인코딩된 미디어 지속 시간은 스트림 리소스 매니페스트에 기록된 지속 시간과 다를 수 있습니다.

      이상적인 가상 타임라인과 실제 재생 타임라인 간에 안정적으로 다시 동기화할 수 있는 방법은 없습니다. 광고 관리 및 비디오 분석을 위한 스트림 재생의 진행 추적 시 실제 재생 시간이 사용되어야 하므로 보고 및 사용자 인터페이스 동작이 미디어 및 광고 컨텐츠를 정확하게 추적하지 못할 수 있습니다.
   * 이 플랫폼의 TVSDK에서 모든 HTTP 요청에 대해 들어오는 사용자 에이전트 이름에 다음 문자열 패턴이 할당됩니다.

      ```
      "Adobe Flash Player"
      ```

## 모범 사례 {#section_tvsdk_best_practices}

다음은 TVSDK에 대한 권장 방법입니다.

* 프로그램 컨텐츠에 HLS 버전 3.0 이상을 사용합니다.
* DHLS용 TVSDK 1.4의 경우 기본적으로 레이지 광고 로딩이 활성화됩니다.

   프리롤 또는 미드롤이 없는 컨텐츠의 경우 컨텐츠 로딩 속도를 높이는 `AdvertisingMetadata.delayAdLoading` 데 사용할 수 있습니다.

