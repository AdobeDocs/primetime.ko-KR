---
description: 라이브 및 VOD(video-on-demand) 미디어의 경우 TVSDK는 중간 해상도 비트 전송률과 관련된 재생 목록을 다운로드하여 재생을 시작하고 해당 재생 목록에 정의된 미디어 세그먼트를 다운로드합니다. 고해상도 비트 레이트 재생 목록 및 관련 미디어를 빠르게 선택하고 다운로드 프로세스를 계속합니다.
title: 미디어 재생 및 장애 조치
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# 미디어 재생 및 장애 조치{#media-playback-and-failover}

라이브 및 VOD(video-on-demand) 미디어의 경우 TVSDK는 중간 해상도 비트 전송률과 관련된 재생 목록을 다운로드하여 재생을 시작하고 해당 재생 목록에 정의된 미디어 세그먼트를 다운로드합니다. 고해상도 비트 레이트 재생 목록 및 관련 미디어를 빠르게 선택하고 다운로드 프로세스를 계속합니다.

## 누락된 재생 목록 장애 조치(failover) {#section_E6B6A15930894F56A0A8501577B35E7F}

전체 재생 목록이 누락된 경우(예: 최상위 매니페스트 파일에 지정된 M3U8 파일이 다운로드되지 않은 경우) TVSDK는 복구를 시도합니다. 복구할 수 없는 경우 애플리케이션이 다음 단계를 결정합니다.

중간 해상도 비트 전송률과 연결된 재생 목록이 없으면 TVSDK는 동일한 해상도로 변형 재생 목록을 검색합니다. 동일한 해상도를 발견하면 일치하는 위치에서 변형 플레이리스트 및 세그먼트 다운로드를 시작합니다. TVSDK에서 동일한 해상도 재생 목록을 찾지 못할 경우 다른 비트율 재생 목록과 해당 변형을 차례로 재생합니다. 즉시 낮은 비트율이 첫 번째 선택 항목이고 그 다음 변형 항목입니다. 유효한 재생 목록을 찾으려고 할 때 낮은 비트율 재생 목록 및 해당 변형이 모두 소진되면 TVSDK가 상위 비트율로 이동하고 여기에서 카운트합니다. 유효한 재생 목록을 찾을 수 없으면 프로세스가 실패하고 플레이어가 ERROR 상태로 이동합니다.

응용 프로그램에서 이 상황을 처리하는 방법을 결정할 수 있습니다. 예를 들어 플레이어 활동을 닫고 사용자를 카탈로그 활동으로 안내할 수 있습니다. 관심 있는 이벤트는 `STATUS_CHANGED` 이벤트이고 해당 콜백은 `onStatusChange` 메서드를 사용합니다. 다음은 플레이어가 내부 상태를 ERROR로 변경하는지 여부를 모니터링하는 코드입니다.

자세한 내용은 `PSDKDemo` 파일. 이벤트 리스너는 MediaPlayer 인스턴스에 연결됩니다.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
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

## 세그먼트 장애 조치(failover) 누락 {#section_ED8CF666289042D39E9914D42BDD9BA4}

세그먼트가 누락된 경우(예: 특정 세그먼트가 다운로드되지 않은 경우) TVSDK는 다양한 장애 조치 시도를 통해 복구를 시도합니다. 복구할 수 없는 경우 오류가 발생합니다.

예를 들어 매니페스트 파일이 없거나, 세그먼트를 다운로드할 수 없는 등의 이유로 서버에서 세그먼트가 누락된 경우 TVSDK는 다음 옵션을 시도하여 장애 조치(failover)를 시도합니다.

1. 변형 파일의 동일한 세그먼트에 동일한 비트 속도로 장애 조치(failover)를 시도합니다.
1. 동일한 파일에서 대체 비트 전송률(ABR 스위치)로 전환합니다.
1. 사용 가능한 모든 변형에서 사용 가능한 모든 비트 전송률을 순환합니다.
1. 세그먼트를 건너뛰고 경고를 발행합니다.

TVSDK에서 대체 세그먼트를 가져올 수 없으면 `CONTENT_ERROR` 오류 알림입니다. 이 알림에는 코드가 있는 내부 알림이 포함됩니다 `DOWNLOAD_ERROR` 코드. 문제가 있는 스트림이 대체 오디오 트랙인 경우 TVSDK는 `AUDIO_TRACK_ERROR` 오류 알림입니다.

비디오 엔진이 지속적으로 세그먼트를 얻을 수 없는 경우 연속 세그먼트 건너뛰기를 5로 제한하며, 그 후 재생이 중지되고 TVSDK에서 를 발행합니다 `NATIVE_ERROR` 코드 5.

>[!NOTE]
>
>ABR(Adaptive Bit Rate) 제어 매개 변수는 장애 조치가 발생할 때 고려하지 않습니다. 이는 장애 조치(failover) 메커니즘이 비트 전송률 프로필에 관계없이 현재 사용 가능한 재생 목록을 백업 스트림으로 사용하도록 설계되었기 때문입니다.
>
>페일오버 작업 중에 프로파일 스위치가 있을 수 있습니다. 재생 목록 세그먼트 중 하나를 다운로드하는 동안 오류가 발생하면 최소/최대 허용 비트 전송률과 같은 ABR 제어 매개 변수가 무시됩니다.
