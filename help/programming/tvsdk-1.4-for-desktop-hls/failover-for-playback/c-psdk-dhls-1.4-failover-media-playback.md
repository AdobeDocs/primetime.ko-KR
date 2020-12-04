---
description: 실시간 및 VOD(Video-On-Demand) 미디어의 경우 TVSDK는 중간 해상도 비트 전송률과 연관된 재생 목록을 다운로드하여 재생을 시작하고 해당 재생 목록에 정의된 미디어 세그먼트를 다운로드합니다. 고해상도 비트 전송률 재생 목록 및 관련 미디어를 빠르게 선택하고 다운로드 과정을 계속합니다.
seo-description: 실시간 및 VOD(Video-On-Demand) 미디어의 경우 TVSDK는 중간 해상도 비트 전송률과 연관된 재생 목록을 다운로드하여 재생을 시작하고 해당 재생 목록에 정의된 미디어 세그먼트를 다운로드합니다. 고해상도 비트 전송률 재생 목록 및 관련 미디어를 빠르게 선택하고 다운로드 과정을 계속합니다.
seo-title: 미디어 재생 및 장애 조치
title: 미디어 재생 및 장애 조치
uuid: 197a6ee0-f1ff-40ac-bd49-eafeae6167d4
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# 미디어 재생 및 장애 조치{#media-playback-and-failover}

실시간 및 VOD(Video-On-Demand) 미디어의 경우 TVSDK는 중간 해상도 비트 전송률과 연관된 재생 목록을 다운로드하여 재생을 시작하고 해당 재생 목록에 정의된 미디어 세그먼트를 다운로드합니다. 고해상도 비트 전송률 재생 목록 및 관련 미디어를 빠르게 선택하고 다운로드 과정을 계속합니다.

## 재생 목록 장애 조치(failover) {#section_E6B6A15930894F56A0A8501577B35E7F} 없음

예를 들어 최상위 매니페스트 파일에 지정된 M3U8 파일이 다운로드되지 않으면 TVSDK가 복구를 시도합니다. 복구할 수 없는 경우 애플리케이션에 다음 단계가 결정됩니다.

중간 해상도 비트 전송률과 연결된 재생 목록이 없는 경우 TVSDK는 동일한 해상도의 변형 재생 목록을 검색합니다. 동일한 해상도를 찾으면 변형 재생 목록과 세그먼트를 일치하는 위치에서 다운로드할 수 있습니다. TVSDK가 동일한 해상도 재생 목록을 찾지 못할 경우 다른 비트 전송률 재생 목록과 해당 변형을 순환하려고 합니다. 바로 낮은 비트 전송률은 첫 번째 선택이고, 그 다음 변형입니다. 유효한 재생 목록을 찾기 위해 낮은 비트 전송률 재생 목록 및 해당 변형이 모두 소진된 경우 TVSDK는 최고 비트 전송률로 이동하여 이후 계산합니다. 유효한 재생 목록을 찾을 수 없으면 프로세스가 실패하고 플레이어가 ERROR 상태로 이동합니다.

애플리케이션에서 이 상황을 처리하는 방법을 결정할 수 있습니다. 예를 들어 플레이어 활동을 닫고 사용자에게 카탈로그 활동으로 안내할 수 있습니다. 관심 이벤트는 `STATUS_CHANGED` 이벤트이고 해당 콜백은 `onStatusChange` 메서드입니다. 플레이어가 내부 상태를 ERROR로 변경하는지 여부를 모니터링하는 코드는 다음과 같습니다.

자세한 내용은 `PSDKDemo` 파일을 참조하십시오. 이벤트 리스너는 MediaPlayer 인스턴스에 연결됩니다.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

클라이언트 측 네트워크가 다운된 경우 이 코드를 사용하여 확인할 수 있습니다.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API는 클라이언트측 네트워크가 다운되었는지 확인하는 데 사용되는 URL을 제공합니다. http 요청에 대해 http 응답 코드 200을 반환하는 유효한 url이어야 합니다.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

setNetworkDownVerificationUrl이 설정되지 않은 경우 TVSDK는 기본적으로 MainManifest url을 사용하여 네트워크가 다운되었는지 확인합니다.

## 세그먼트 장애 조치(failover) {#section_ED8CF666289042D39E9914D42BDD9BA4} 없음

세그먼트가 누락된 경우(예: 특정 세그먼트가 다운로드되지 않으면 TVSDK는 다양한 장애 조치 시도를 통해 복구를 시도합니다. 복구할 수 없는 경우 오류가 발생합니다.

예를 들어 매니페스트 파일이 없기 때문에 서버에서 세그먼트가 누락된 경우 세그먼트를 다운로드할 수 없는 등의 방법으로 TVSDK는 다음 옵션을 사용하여 실패 시도를 합니다.

1. 변형 파일에서 동일한 비트 속도로 동일한 세그먼트에 대한 장애 조치(failover)를 시도합니다.
1. 동일한 파일의 대체 비트 전송률(ABR 스위치)으로 전환합니다.
1. 사용 가능한 모든 변형의 모든 비트 전송률을 순환합니다.
1. 세그먼트를 건너뛰고 경고를 표시합니다.

TVSDK가 대체 세그먼트를 가져올 수 없는 경우 `CONTENT_ERROR` 오류 알림을 트리거합니다. 이 알림에는 `DOWNLOAD_ERROR` 코드와 함께 내부 알림이 포함되어 있습니다. 문제가 있는 스트림이 대체 오디오 트랙인 경우 TVSDK는 `AUDIO_TRACK_ERROR` 오류 알림을 생성합니다.

비디오 엔진이 지속적으로 세그먼트를 가져올 수 없는 경우 연속 세그먼트는 5로 건너뛰고 재생이 중지되고 TVSDK가 코드 5와 함께 `NATIVE_ERROR`을(를) 발행합니다.

>[!NOTE]
>
>장애 조치(failover)가 발생할 때 ABR(응용 비트 전송률) 제어 매개 변수는 고려하지 않습니다. 이는 장애 조치 메커니즘이 비트 전송률 프로필에 관계없이 현재 사용 가능한 재생 목록을 백업 스트림으로 사용하도록 설계되었기 때문입니다.
>
>장애 조치(failover) 작업 중에 프로필 스위치가 있을 수 있습니다. 재생 목록 세그먼트 중 하나를 다운로드하는 동안 오류가 발생하는 경우 ABR 제어 매개 변수(예: 최소/최대 허용 비트 전송률)는 무시됩니다.

