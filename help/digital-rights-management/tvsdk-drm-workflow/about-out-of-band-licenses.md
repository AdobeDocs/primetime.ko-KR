---
seo-title: 대역 외 라이선스 개요
title: 대역 외 라이선스 개요
uuid: 82e4529a-ee1b-4c0c-8885-e0e68319d1a0
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 대역 외 라이선스 {#out-of-band-licenses}

또한 Primetime DRM 라이선스 서버에 연결하지 않고 해당 `storeVoucher()` 방법을 사용하여 디스크 및 메모리에 라이센스를 저장하여 비대역(out-of-band) 라이선스를 얻을 수 있습니다.

Primetime에서 암호화된 비디오를 재생하려면 해당 런타임에서 해당 비디오의 라이선스를 받아야 합니다. 라이선스는 비디오의 암호 해독 키를 포함하며 고객이 배포한 Primetime DRM 라이선스 서버에 의해 생성됩니다.

런타임은 일반적으로 비디오의 DRM 메타데이터( `DRMContentData` 클래스)에 지정된 Primetime DRM 라이선스 서버에 라이선스 요청을 전송하여 이 라이선스를 가져옵니다. 응용 프로그램은 `DRMManager.loadVoucher()` 메서드를 호출하여 이 라이센스 요청을 트리거할 수 있습니다.

`DRMManager.storeVoucher()` 애플리케이션에서 대역 외 라이선스를 전송할 수 있습니다. 그런 다음 런타임은 라이센스 요청 프로세스를 건너뛰고 전달된 라이센스를 사용하여 암호화된 비디오를 재생할 수 있습니다. Primetime DRM 라이선스 서버에서 라이선스를 생성해야만 비대역 인증을 받을 수 있습니다. 그러나 Primetime DRM 라이선스 서버가 아닌 모든 HTTP 서버에서 라이선스를 호스팅할 수 있습니다.

`DRMManager.storeVoucher()` 는 여러 장치 간의 라이센스 공유를 지원하는 데에도 사용됩니다. Primetime DRM 3.0 이후에는 이 기능을 &quot;장치 도메인 지원&quot;이라고 합니다. 배포에서 이 사용 사례를 지원하는 경우 이 `DRMManager.addToDeviceGroup()` 방법을 사용하여 장치 그룹에 여러 컴퓨터를 등록할 수 있습니다. 지정된 컨텐츠에 대해 유효한 도메인 바인딩된 라이센스가 있는 컴퓨터가 있는 경우 해당 `DRMVoucher.toByteArray()` 방법을 사용하여 일련 번호가 할당된 라이센스를 추출할 수 있고 다른 시스템에서 해당 `DRMManager.storeVoucher()` 방법을 사용하여 라이센스를 가져올 수 있습니다.

## 장치 등록 정보 {#about-device-registration}

모든 Primetime DRM 라이선스는 제작 시 최종 엔티티에 구속되어야 합니다. 바인딩은 특정 엔티티에 라이센스를 사용할 수 있는 권한만 허용하는 암호화 프로세스입니다. 이는 임의의 장치에서 사용할 수 있는 &quot;부동 라이선스&quot;를 방지하기 위해 필요합니다. Primetime DRM에서 &quot;사전 생성&quot; 라이선스를 이용하려면 미리 생성된 라이선스의 &quot;대상&quot;이 미리 알려져야 합니다. Primetime DRM 파섹

## 장치 등록 {#register-a-device}

다음과 같은 작업을 수행했다고 가정합니다.

* Primetime DRM Server SDK를 설정했습니다.
* 사전 생성된 라이선스 발급을 위한 HTTP 서버를 설정했습니다.
* 보호된 콘텐츠를 보기 위해 Primetime 애플리케이션을 만들었습니다.

 장치 등록 단계에는 다음 작업이 포함됩니다.

1. 응용 프로그램에서 임의로 생성된 ID를 만듭니다.
1. 응용 프로그램에서 `DRMManager.authenticate()` 메서드를 호출합니다. 응용 프로그램은 임의로 생성된 ID를 인증 요청에 포함해야 합니다. 예를 들어 사용자 이름 필드에 ID를 포함시킵니다.
1. 2단계에서 언급한 작업을 통해 Primetime DRM이 고객의 서버에 인증 요청을 전송합니다. 이 요청에는 장치 인증서가 포함되어 있습니다.
   1. 서버는 요청 및 저장소에서 장치 인증서와 생성된 ID를 추출합니다.
   1. 고객 하위 시스템은 이 디바이스 인증서에 대한 라이선스를 미리 생성하여 저장하고 생성된 ID와 연결할 수 있도록 해당 디바이스 인증서에 대한 액세스 권한을 부여합니다..
1. 서버가 &quot;성공&quot; 메시지와 함께 요청에 응답합니다.
1. 생성된 ID가 응용 프로그램에 저장됩니다.

장치 등록 후 응용 프로그램은 이전 구성표에서 장치 ID를 사용한 것과 동일한 방법으로 생성된 ID를 사용합니다.
1. 애플리케이션에서 생성된 ID를 찾으려고 시도합니다.
1. 생성된 ID 파섹 이 애플리케이션은 해당 `DRMManager.storeVoucher()` 방법을 사용하여 사용을 위해 Primetime DRM 클라이언트에 라이선스를 전송합니다..
1. 생성된 ID를 찾을 수 없는 경우 애플리케이션은 장치 등록 절차를 거칩니다.

## DRM 팩토리 재설정 {#drm-factory-reset}

장치 사용자가 DRM 팩토리 재설정 옵션을 불러오면 장치 인증서가 삭제됩니다. 보호된 내용을 계속 재생하려면 응용 프로그램이 장치 등록 절차를 다시 거쳐야 합니다. 애플리케이션이 오래된 사전 생성 라이선스를 전송하는 경우 이전 디바이스 ID에 대해 라이센스가 암호화되었기 때문에 Primetime DRM 클라이언트는 이를 거부합니다.

* Flash API:DRMManager [.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (복구할 수 없는 특정 DRM 오류 코드에 대한 응답으로만 호출할 수 있습니다.)
* iOS API:DRMManager [resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* Android API:DRMManager [.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))