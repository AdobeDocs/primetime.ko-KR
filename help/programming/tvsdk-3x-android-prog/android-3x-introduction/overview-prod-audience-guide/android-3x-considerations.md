---
description: TVSDK를 가장 효과적으로 사용하려면 TVSDK의 운영에 대한 특정 세부 사항을 고려하고 특정 모범 사례를 따라야 합니다.
title: 고려 사항 및 우수 사례
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# 고려 사항 및 우수 사례 {#considerations-and-best-practices}

TVSDK를 가장 효과적으로 사용하려면 TVSDK의 운영에 대한 특정 세부 사항을 고려하고 특정 모범 사례를 따라야 합니다.

## {#section_tvsdk_considerations} 고려 사항

TVSDK를 사용할 때는 다음 정보를 기억하십시오.

* TVSDK API는 Java로 구현됩니다.
* Adobe Primetime은 현재 Android 에뮬레이터에서 작동하지 않습니다.

   테스트에 실제 디바이스를 사용해야 합니다.
* 재생은 HLS(HTTP Live Streaming) 컨텐츠에 대해서만 지원됩니다.
* 기본 비디오 컨텐츠는 멀티플렉싱(동일한 변환의 비디오 및 오디오 스트림) 또는 멀티플렉싱되지 않은(개별 변환의 비디오 및 오디오 스트림)으로 멀티플렉싱할 수 있습니다.
* 현재 대부분의 TVSDK API 작업을 기본 Android 스레드인 UI 스레드에서 실행해야 합니다.

   기본 스레드에서 올바르게 실행되는 작업은 백그라운드 스레드에서 실행될 때 오류를 throw하고 종료할 수 있습니다.
* 비디오를 재생하려면 Adobe 비디오 엔진(AVE)이 필요합니다. 이는 미디어 리소스에 액세스할 수 있는 방법 및 시기에 영향을 줍니다.

   * 닫힌 캡션은 AVE에서 제공하는 범위까지 지원됩니다.
   * 인코더 정밀도에 따라 실제 인코딩된 미디어 지속 시간은 스트림 리소스 매니페스트에 기록된 지속 시간과 다를 수 있습니다.

      이상적인 가상 타임라인과 실제 재생 타임라인 간에 안정적으로 다시 동기화할 수 있는 방법은 없습니다. 광고 관리 및 비디오 분석을 위해 스트림 재생의 진행 추적 시 실제 재생 시간이 사용되므로 보고 및 사용자 인터페이스 동작이 미디어 및 광고 컨텐츠를 정확하게 추적하지 못할 수 있습니다.
   * 이 플랫폼의 TVSDK에서 모든 미디어 요청에 대해 들어오는 사용자 에이전트 이름은 다음 문자열 패턴으로 지정됩니다.

      ```
      "Adobe Primetime/" + originalUserAgent
      ```

      광고 관련 모든 호출은 광고 삽입 메타데이터를 설정하는 동안 설정하는 경우 Android 기본 사용자 에이전트 또는 사용자 지정 사용자 에이전트를 사용합니다.

## 우수 사례 {#section_tvsdk_best_practices}

다음은 TVSDK에 대한 권장 방법입니다.

* 프로그램 내용에 HLS 버전 3.0 이상을 사용합니다.
* 대부분의 TVSDK 작업은 배경 스레드가 아닌 기본(UI) 스레드에서 실행됩니다.
* Android용 TVSDK 3.0의 경우 기본적으로 게으른 광고 해결이 활성화되어 있습니다.

프리롤 또는 미드롤이 없는 내용의 경우 `AdvertisingMetadata.setPreroll(false)`을 사용하여 내용 로드를 가속화할 수 있습니다.