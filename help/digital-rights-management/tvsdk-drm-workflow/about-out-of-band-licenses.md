---
title: 대역 외 라이선스 개요
description: 대역 외 라이선스 개요
copied-description: true
exl-id: 31a9f097-74e8-41d0-9b9a-1c2a08d3e63a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 대역 외 라이선스 {#out-of-band-licenses}

또한 라이센스를 디스크 및 메모리에 저장하여 대역 외(Primetime DRM 라이센스 서버에 연결하지 않고) 라이센스를 얻을 수 있습니다. `storeVoucher()` 메서드를 사용합니다.

Primetime에서 암호화된 비디오를 재생하려면 각 런타임에서 해당 비디오에 대한 라이선스를 받아야 합니다. 이 라이센스는 비디오의 암호 해독 키를 포함하며, 고객이 배포한 Primetime DRM 라이센스 서버에서 생성됩니다.

런타임은 일반적으로 비디오의 DRM 메타데이터에 지정된 Primetime DRM 라이센스 서버에 라이센스 요청을 전송하여 이 라이센스를 가져옵니다( `DRMContentData` class). 응용 프로그램은 다음을 호출하여 이 라이선스 요청을 트리거할 수 있습니다. `DRMManager.loadVoucher()` 메서드를 사용합니다.

`DRMManager.storeVoucher()` 응용 프로그램에서 대역 외 라이선스를 가져올 수 있습니다. 그런 다음 런타임에서는 라이선스 요청 프로세스를 건너뛰고 암호화된 비디오를 재생하기 위해 전달된 라이선스를 사용할 수 있습니다. Primetime DRM 라이선스 서버에서 라이선스를 생성해야 대역 외로 가져올 수 있습니다. 그러나 Primetime DRM 라이센스 서버 대신 모든 HTTP 서버에서 라이센스를 호스팅할 수 있는 옵션이 있습니다.

`DRMManager.storeVoucher()` 여러 장치 간의 라이선스 공유를 지원하는 데에도 사용됩니다. Primetime DRM 3.0 이후 이 기능을 &quot;장치 도메인 지원&quot;이라고 합니다. 배포가 이 사용 사례를 지원하는 경우 `DRMManager.addToDeviceGroup()` 메서드를 사용합니다. 지정된 콘텐츠에 대해 유효한 도메인 바인딩 라이선스가 있는 시스템이 있는 경우 응용 프로그램은 다음을 사용하여 직렬화된 라이선스를 추출할 수 있습니다. `DRMVoucher.toByteArray()` 메서드 및 다른 컴퓨터에서 `DRMManager.storeVoucher()` 메서드를 사용합니다.

## 장치 등록 정보 {#about-device-registration}

생성 시 모든 Primetime DRM 라이센스는 최종 엔티티에 바인딩되어야 합니다. 바인딩은 특정 엔터티에서만 라이선스를 사용할 수 있도록 하는 암호화 프로세스입니다. 이는 임의의 장치에서 사용할 수 있는 &quot;유동 라이선스&quot;를 방지하기 위해 필요합니다. Primetime DRM이 라이선스를 &quot;사전 생성&quot;하려면 이러한 사전 생성된 라이선스의 &quot;대상&quot;을 미리 알고 있어야 합니다. Primetime DRM은 이를 &quot;장치 등록&quot;이라고 합니다.

## 장치 등록 {#register-a-device}

사용자가 다음 작업을 수행했다고 가정해 보겠습니다.

* Primetime DRM 서버 SDK를 설정했습니다.
* 미리 생성된 라이선스를 발급할 HTTP 서버를 설정했습니다.
* 보호된 콘텐츠를 보기 위한 Primetime 애플리케이션을 만들었습니다.

 장치 등록 단계에는 다음 작업이 포함됩니다.

1. 애플리케이션은 임의로 생성된 ID를 생성합니다.
1. 애플리케이션이 `DRMManager.authenticate()` 메서드를 사용합니다. 애플리케이션은 인증 요청에 임의로 생성된 ID를 포함해야 합니다. 예를 들어 사용자 이름 필드에 ID를 포함합니다.
1. 2단계에서 언급된 작업은 Primetime DRM이 고객의 서버에 인증 요청을 보내게 됩니다. 이 요청에는 장치 인증서가 포함됩니다.
   1. 서버는 요청으로부터 디바이스 인증서 및 생성된 ID를 추출하여 저장한다.
   1. 고객 하위 시스템은 이 장치 인증서에 대한 라이선스를 미리 생성하고 저장하고, 생성된 ID와 연결하는 방식으로 해당 라이선스에 대한 액세스 권한을 부여합니다. .
1. 서버가 &quot;성공&quot; 메시지로 요청에 응답합니다.
1. 애플리케이션은 생성된 ID를 저장합니다.

디바이스 등록 후 애플리케이션은 이전 스키마에서 디바이스 ID를 사용했을 때와 동일한 방식으로 생성된 ID를 사용합니다.
1. 애플리케이션은 생성된 ID를 찾으려고 합니다.
1. 생성된 ID를 찾으면 애플리케이션은 사전 생성된 라이선스를 다운로드하는 동안 생성된 ID를 사용하게 됩니다. 애플리케이션은 를 사용하여 소비하기 위해 Primetime DRM 클라이언트에 라이센스를 전송합니다. `DRMManager.storeVoucher()` 메서드를 사용합니다. .
1. 생성된 ID를 찾을 수 없는 경우, 애플리케이션은 디바이스 등록 절차를 거치게 된다.

## DRM 팩토리 재설정 {#drm-factory-reset}

장치 사용자가 DRM 초기 설정 옵션을 호출하면 장치 인증서가 삭제됩니다. 보호된 콘텐츠를 계속 재생하려면 애플리케이션은 디바이스 등록 절차를 다시 거쳐야 한다. 애플리케이션이 오래된 사전 생성된 라이센스를 전송하는 경우 라이센스가 이전 장치 ID에 대해 암호화되었으므로 Primetime DRM 클라이언트는 해당 라이센스를 거부합니다.

* Flash API: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (복구할 수 없는 특정 DRM 오류 코드에 대한 응답으로만 호출할 수 있습니다.)
* iOS API: [DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* Android API: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))
