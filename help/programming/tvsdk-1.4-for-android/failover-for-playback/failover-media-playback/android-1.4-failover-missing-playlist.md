---
description: '전체 재생 목록이 누락된 경우(예: 최상위 매니페스트 파일에 지정된 M3U8 파일이 다운로드되지 않은 경우) TVSDK는 복구를 시도합니다. 복구할 수 없는 경우 애플리케이션이 다음 단계를 결정합니다.'
title: 누락된 재생 목록 장애 조치(failover)
exl-id: aab2dde3-aee2-4ade-b8f9-91c72df0c747
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 누락된 재생 목록 장애 조치(failover){#missing-playlist-failover}

전체 재생 목록이 누락된 경우(예: 최상위 매니페스트 파일에 지정된 M3U8 파일이 다운로드되지 않은 경우) TVSDK는 복구를 시도합니다. 복구할 수 없는 경우 애플리케이션이 다음 단계를 결정합니다.

중간 해상도 비트 전송률과 연결된 재생 목록이 없으면 TVSDK는 동일한 해상도로 변형 재생 목록을 검색합니다. 동일한 해상도를 발견하면 일치하는 위치에서 변형 플레이리스트 및 세그먼트 다운로드를 시작합니다. TVSDK에서 동일한 해상도 재생 목록을 찾지 못할 경우 다른 비트율 재생 목록과 해당 변형을 차례로 재생합니다. 즉시 낮은 비트율이 첫 번째 선택 항목이고 그 다음 변형 항목입니다. 유효한 재생 목록을 찾으려고 할 때 낮은 비트율 재생 목록 및 해당 변형이 모두 소진되면 TVSDK가 상위 비트율로 이동하고 여기에서 카운트합니다. 유효한 재생 목록을 찾을 수 없으면 프로세스가 실패하고 플레이어가 ERROR 상태로 이동합니다.

응용 프로그램에서 이 상황을 처리하는 방법을 결정할 수 있습니다. 예를 들어 플레이어 활동을 닫고 사용자를 카탈로그 활동으로 안내할 수 있습니다. 관심 있는 이벤트는 `STATE_CHANGED` 이벤트이고 해당 콜백은 `onStateChanged` 메서드를 사용합니다. 다음은 플레이어가 내부 상태를 ERROR로 변경하는지 여부를 모니터링하는 코드입니다.

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

자세한 내용은 [!DNL PlayerFragment.java] sdk의 파일:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

클라이언트측 네트워크가 다운된 경우 이 코드를 사용하여 확인할 수 있습니다.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API는 클라이언트측 네트워크가 다운되었는지 확인하는 데 사용되는 URL을 제공합니다. 유효한 URL이어야 하며, HTTP 요청에 대해 HTTP 응답 코드 200을 반환합니다.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

setNetworkDownVerificationUrl이 설정되지 않은 경우 TVSDK는 기본적으로 MainManifest url을 사용하여 네트워크가 다운되었는지 확인합니다.
