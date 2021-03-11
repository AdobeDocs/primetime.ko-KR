---
description: 예를 들어 최상위 매니페스트 파일에 지정된 M3U8 파일이 다운로드되지 않는 경우 TVSDK가 복구를 시도합니다. 복구할 수 없는 경우 응용 프로그램에서 다음 단계를 결정합니다.
title: 재생 목록 장애 조치(failover)가 없습니다.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# 재생 목록 장애 조치(failover){#missing-playlist-failover} 없음

예를 들어 최상위 매니페스트 파일에 지정된 M3U8 파일이 다운로드되지 않는 경우 TVSDK가 복구를 시도합니다. 복구할 수 없는 경우 응용 프로그램에서 다음 단계를 결정합니다.

중간 해상도 비트 전송률과 연결된 재생 목록이 없는 경우 TVSDK는 동일한 해상도의 변형 재생 목록을 검색합니다. 동일한 해상도를 찾으면 변형 재생 목록과 세그먼트가 일치하는 위치에서 다운로드되기 시작합니다. TVSDK에서 동일한 해상도 재생 목록을 찾을 수 없는 경우 다른 비트 전송률 재생 목록 및 해당 변형을 순환하려고 합니다. 즉시 낮은 비트 전송률은 첫 번째 선택이고 그 다음 변형입니다. 유효한 재생 목록을 찾기 위해 낮은 비트 전송률 재생 목록 및 해당 변형이 모두 소진된 경우 TVSDK는 최상위 비트 전송률로 이동하여 그 값을 계산합니다. 유효한 재생 목록을 찾을 수 없으면 프로세스가 실패하고 플레이어가 ERROR 상태로 이동합니다.

응용 프로그램에서 이 상황을 처리하는 방법을 결정할 수 있습니다. 예를 들어 플레이어 활동을 닫고 사용자에게 카탈로그 활동으로 안내할 수 있습니다. 관심 이벤트는 `STATE_CHANGED` 이벤트이고 해당 콜백은 `onStateChanged` 메서드입니다. 플레이어가 내부 상태를 ERROR로 변경하는지 여부를 모니터링하는 코드는 다음과 같습니다.

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

자세한 내용은 SDK의 [!DNL PlayerFragment.java] 파일을 참조하십시오.

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

클라이언트 측 네트워크가 다운된 경우 이 코드를 사용하여 확인할 수 있습니다.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API는 클라이언트측 네트워크가 다운되었는지 확인하는 데 사용되는 URL을 제공합니다. http 요청에 대해 http 응답 코드 200을 반환하는 유효한 URL이어야 합니다.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

setNetworkDownVerificationUrl이 설정되지 않은 경우 TVSDK는 기본적으로 MainManifest URL을 사용하여 네트워크가 다운되었는지 확인합니다.
