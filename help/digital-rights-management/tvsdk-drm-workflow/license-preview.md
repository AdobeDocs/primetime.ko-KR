---
title: 라이선스 미리 보기
description: 라이선스 미리 보기
copied-description: true
exl-id: 53a57610-86a8-4c5d-9494-679ede35abf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 라이선스 미리 보기 {#license-preview}

장치가 Primetime DRM 라이선스를 소비하고 완전히 적용할 수 있는지 여부에 대한 질문이 있는 경우 라이선스 미리 보기 기능을 사용할 수 있습니다. 미리보기 라이선스는 최종 라이선스에 정의된 모든 제한 및 제한과 완전히 일치하지만 보호된 콘텐츠를 해독하는 데 필요한 콘텐츠 암호화 키(CEK)는 포함하지 않습니다. 이 기능은 콘텐츠 배포자가 클라이언트에 특정 라이선스를 제공하기로 결정하기 전에 클라이언트가 라이선스를 실제로 사용할 수 있는지 확인하는 데 유용합니다. 예를 들어, 고객은 HD 콘텐츠를 시청하고 싶지만 콘텐츠 배포자는 디바이스가 HDCP를 완전히 감지하고 사용할 수 있는지 확인하려고 합니다. 이 경우 클라이언트는 `DRMManager.loadPreviewVoucher()`. 다음과 같은 경우 `DRMStatusEvent` 가 대신 수신됨 `DRMErrorEvent`그런 다음 클라이언트는 라이센스에서 출력 보호 제한을 완전히 적용할 수 있으며 컨텐츠 배포자는 이 유형의 라이센스를 클라이언트에게 자유롭게 제공할 수 있습니다.

[iOS acquirePreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
