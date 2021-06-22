---
description: 일반적으로 모든 Primetime DRM 라이센스는 생성 시 고유한 장치에 바인딩됩니다. 이 바인딩은 사용자가 권한 부여 없이 여러 장치에서 라이센스를 공유하지 못하도록 합니다. Primetime DRM은 장치 간 바인딩 외에도 장치 도메인 또는 장치 그룹에 라이선스를 바인딩할 수 있는 기능을 제공합니다.
title: 도메인 지원을 사용하여 암호화된 컨텐츠 재생
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 장치 도메인 지원 {#device-domain-support}

일반적으로 모든 Primetime DRM 라이센스는 생성 시 고유한 장치에 바인딩됩니다. 이 바인딩은 사용자가 권한 부여 없이 여러 장치에서 라이센스를 공유하지 못하도록 합니다. Primetime DRM은 장치 간 바인딩 외에도 장치 도메인 또는 장치 그룹에 라이선스를 바인딩할 수 있는 기능을 제공합니다.

컨텐츠 메타데이터가 장치 도메인 등록이 필요하다고 지정하는 경우 애플리케이션에서 API를 호출하여 장치 그룹에 가입할 수 있습니다. 이 작업은 도메인 서버로 전송될 도메인 등록 요청을 트리거합니다. 라이센스가 장치 그룹에 발급되면 라이센스를 내보내고 장치 그룹에 가입한 다른 장치와 공유할 수 있습니다.

그런 다음 장치 그룹 정보를 `DRMContentData` `VoucherAccessInfo` 개체에 사용하여 라이센스를 성공적으로 검색하고 사용하는 데 필요한 정보를 제공합니다.

## 도메인 지원 {#play-encrypted-content-using-domain-support}을(를) 사용하여 암호화된 컨텐츠 재생

Primetime DRM을 사용하여 암호화된 콘텐츠를 재생하려면 다음 단계를 수행하십시오.

1. `VoucherAccessInfo.deviceGroup`을 사용하여 장치 그룹 등록이 필요한지 확인합니다.
1. 인증이 필요한 경우:
   1. `DeviceGroupInfo.authenticationMethod` 속성을 사용하여 인증이 필요한지 확인합니다.
   1. 인증이 필요한 경우 다음 단계 중 하나를 수행하여 사용자를 인증합니다.

      * 사용자 이름과 암호를 얻고 `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)` 을 호출합니다.
      * 캐시/사전 생성된 인증 토큰을 가져오고 `DRMManager.setAuthenticationToken()`을 호출합니다.
   1. `DRMManager.addToDeviceGroup()` 호출
1. 다음 작업 중 하나를 수행하여 컨텐츠에 대한 라이센스를 얻습니다.
   1. `DRMManager.loadVoucher()` 메서드를 사용합니다.
   1. 동일한 장치 그룹에 등록된 다른 장치에서 라이센스를 얻은 다음 `DRMManager.storeVoucher()` 메서드를 통해 `DRMManager` 의 라이센스를 제공합니다.
1. `Primetime.play()` 메서드를 사용하여 암호화된 콘텐츠를 재생합니다.
컨텐츠에 대한 라이센스를 내보내려면 Primetime DRM 라이센스 서버에서 라이센스를 얻은 후 모든 장치가 `DRMVoucher.toByteArray()` 메서드를 사용하여 라이센스의 원시 바이트를 제공할 수 있습니다. 컨텐츠 공급자는 일반적으로 장치 그룹의 장치 수를 제한합니다. 한도에 도달하면 현재 장치를 등록하기 전에 사용하지 않는 장치에서 `DRMManager.removeFromDeviceGroup()` 메서드를 호출해야 할 수 있습니다.
