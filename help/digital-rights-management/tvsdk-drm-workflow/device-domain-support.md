---
description: 일반적으로 모든 Primetime DRM 라이선스는 생성 시 고유한 디바이스에 바인딩됩니다. 이 바인딩은 사용자가 권한 부여 없이 서로 다른 장치 간에 라이선스를 공유하는 것을 방지합니다. Primetime DRM은 디바이스별 바인딩 외에 디바이스 도메인 또는 디바이스 그룹에 라이센스를 바인딩하는 기능을 제공합니다.
title: 도메인 지원을 사용하여 암호화된 콘텐츠 재생
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 장치 도메인 지원 {#device-domain-support}

일반적으로 모든 Primetime DRM 라이선스는 생성 시 고유한 디바이스에 바인딩됩니다. 이 바인딩은 사용자가 권한 부여 없이 서로 다른 장치 간에 라이선스를 공유하는 것을 방지합니다. Primetime DRM은 디바이스별 바인딩 외에 디바이스 도메인 또는 디바이스 그룹에 라이센스를 바인딩하는 기능을 제공합니다.

콘텐츠 메타데이터가 디바이스 도메인 등록이 필요하다고 지정하는 경우 애플리케이션은 API를 호출하여 디바이스 그룹에 가입할 수 있습니다. 이 작업을 수행하면 도메인 등록 요청이 도메인 서버로 전송되게 트리거됩니다. 장치 그룹에 라이선스를 발급하면 라이선스를 내보내고 장치 그룹에 가입한 다른 장치와 공유할 수 있습니다.

그런 다음 장치 그룹 정보가 `DRMContentData` `VoucherAccessInfo` 개체를 가져와야 합니다. 이 개체는 라이선스를 성공적으로 검색하고 사용하는 데 필요한 정보를 표시하는 데 사용됩니다.

## 도메인 지원을 사용하여 암호화된 콘텐츠 재생 {#play-encrypted-content-using-domain-support}

Primetime DRM을 사용하여 암호화된 콘텐츠를 재생하려면 다음 단계를 수행하십시오.

1. 사용 `VoucherAccessInfo.deviceGroup`, 장치 그룹 등록이 필요한지 확인하십시오.
1. 인증이 필요한 경우:
   1. 사용 `DeviceGroupInfo.authenticationMethod` 속성이 인증이 필요한지 확인합니다.
   1. 인증이 필요한 경우 다음 단계 중 하나를 수행하여 사용자를 인증합니다.

      * 사용자의 사용자 이름 및 암호 가져오기 및 호출 `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * 캐시된/미리 생성된 인증 토큰을 가져오고 를 호출합니다. `DRMManager.setAuthenticationToken()`.
   1. 호출 `DRMManager.addToDeviceGroup()`
1. 다음 작업 중 하나를 수행하여 콘텐츠에 대한 라이선스를 가져옵니다.
   1. 사용 `DRMManager.loadVoucher()` 메서드를 사용합니다.
   1. 동일한 장치 그룹에 등록된 다른 장치에서 라이센스를 얻은 다음 `DRMManager` 다음을 통해 `DRMManager.storeVoucher()` 메서드를 사용합니다.
1. 다음을 사용하여 암호화된 콘텐츠 재생 `Primetime.play()` 메서드를 사용합니다.
콘텐츠에 대한 라이선스를 내보내려면 모든 장치는 를 사용하여 라이선스의 원시 바이트를 제공할 수 있습니다. `DRMVoucher.toByteArray()` primetime DRM 라이센스 서버에서 라이센스를 얻은 후 메서드. 콘텐츠 공급자는 일반적으로 장치 그룹의 장치 수를 제한합니다. 제한에 도달하면 을 호출해야 할 수 있습니다. `DRMManager.removeFromDeviceGroup()` 현재 장치를 등록하기 전에 사용하지 않은 장치의 메서드.
