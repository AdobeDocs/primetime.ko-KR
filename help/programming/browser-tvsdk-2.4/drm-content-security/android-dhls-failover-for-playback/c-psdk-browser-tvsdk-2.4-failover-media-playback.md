---
description: 실시간 및 VOD 미디어의 경우, Browser TVSDK는 중간 해상도 비트 전송률과 연관된 재생 목록을 다운로드한 다음 재생 목록에 정의된 중간 해상도 비트 전송률 미디어 세그먼트를 다운로드하여 재생을 시작합니다.
title: 미디어 재생
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# 미디어 재생 {#media-playback}

실시간 및 VOD 미디어의 경우, Browser TVSDK는 중간 해상도 비트 전송률과 연관된 재생 목록을 다운로드한 다음 재생 목록에 정의된 중간 해상도 비트 전송률 미디어 세그먼트를 다운로드하여 재생을 시작합니다.

Browser TVSDK는 고해상도 비트 전송률 재생 목록 및 관련 미디어를 빠르게 선택하고 다운로드 과정을 계속합니다.

## 재생 목록 장애 조치(failover) {#section_81A5822C108449E1A0E94A6E25DE9E8E} 없음

예를 들어 최상위 매니페스트 파일에 지정된 M3U8 파일이 다운로드되지 않는 경우 브라우저 TVSDK가 복구를 시도합니다. 복구할 수 없는 경우 애플리케이션에 다음 단계가 결정됩니다.

중간 해상도 비트 전송률과 연결된 재생 목록이 없는 경우 Browser TVSDK는 동일한 해상도의 변형 재생 목록을 검색합니다. 동일한 해상도를 찾으면 변형 재생 목록과 세그먼트가 일치하는 위치에서 다운로드되기 시작합니다. Browser TVSDK에서 동일한 해상도 재생 목록을 찾을 수 없는 경우 다른 비트 전송률 재생 목록 및 해당 변형을 순환하려고 합니다. 즉시 낮은 비트 전송률은 첫 번째 선택이고 그 다음 변형입니다. 유효한 재생 목록을 찾기 위해 낮은 비트 전송률 재생 목록 및 해당 변형이 모두 소진된 경우 Browser TVSDK는 최상위 비트 전송률로 이동하여 그 값을 계산합니다. 유효한 재생 목록을 찾을 수 없으면 프로세스가 실패하고 플레이어가 ERROR 상태로 이동합니다.

응용 프로그램에서 이 상황을 처리하는 방법을 결정할 수 있습니다. 예를 들어 플레이어 활동을 닫고 사용자에게 카탈로그 활동으로 안내할 수 있습니다. 관심 이벤트는 상태 또는 상태 변경 이벤트이고 해당 콜백은 on status changed 메서드입니다. 플레이어가 내부 상태를 ERROR로 변경하는지 여부를 모니터링하는 코드는 다음과 같습니다.

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
