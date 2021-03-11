---
title: 라이선스 미리 보기
description: 라이선스 미리 보기
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# 라이선스 미리 보기 {#license-preview}

장치가 Primetime DRM 라이선스를 소비하고 완전히 적용할 수 있는지 여부에 대한 질문이 있는 경우 라이선스 미리 보기 기능을 사용할 수 있습니다. 미리 보기 라이선스는 최종 라이선스에 정의된 모든 제한 및 제한 사항과 완전히 일치하지만 보호된 내용을 해독하는 데 필요한 CEK(Content Encryption Key)는 포함하지 않습니다. 이 기능은 컨텐트 배포자가 클라이언트에 특정 라이센스를 제공하기로 결정하기 전에 클라이언트가 실제로 라이센스를 사용할 수 있는지 여부를 결정하는 데 유용합니다. 예를 들어, 고객이 HD 컨텐츠를 시청하려고 하지만, 컨텐트 배포자는 장치가 HDCP를 완전히 감지하고 참여를 유도할 수 있도록 하려고 합니다. 이 경우 클라이언트는 `DRMManager.loadPreviewVoucher()`을(를) 호출할 수 있습니다. `DRMErrorEvent` 대신 `DRMStatusEvent`이 수신되면 클라이언트가 라이센스에 출력 보호 제한 사항을 완전히 적용할 수 있으며, 컨텐트 배포자는 이러한 유형의 라이센스를 클라이언트에 자유롭게 제공할 수 있습니다.

[iOS acquirePreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
