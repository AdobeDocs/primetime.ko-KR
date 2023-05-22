---
title: 사용 모델 데모 모드 구성
description: 사용 모델 데모 모드 구성
copied-description: true
exl-id: 593acfbd-fd37-4bab-ac8e-5cb62963fac4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 사용 모델 데모 모드 구성{#configure-usage-model-demo-mode}

참조 구현 서버에서 사용 모델 데모에 대한 라이선스를 발급하려면 먼저 4개의 사용 모델 각각에 대해 라이선스가 생성되는 방법을 지정하도록 서버를 구성해야 합니다. 즉, 각 사용 모델에 대해 DRM 정책을 지정해야 합니다. 참조 구현은에 다음 샘플 DRM 정책을 포함합니다. [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] 디렉터리:

* `dto-policy.pol` - (다운로드 대상)
* `vod-policy.pol` - (대여/주문형 비디오)
* `sub-policy.pol` - (구독)
* `ad-policy.pol` - (Ad-fedded)

>[!NOTE]
>
>이러한 샘플 정책을 고유한 DRM 정책으로 대체할 수 있습니다.

1. 다음 속성을에서 설정합니다. [!DNL flashaccess-refimpl.properties] 각 사용 모델에 적용할 DRM 정책을 지정하려면 다음과 같이 하십시오.

   ```
   # DRM Policy file name for Download To Own usage 
   RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol 
   # DRM Policy file name for Rental usage 
   RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol 
   # DRM Policy file name for Subscription usage 
   RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol 
   # DRM Policy file name for Ad Supported (free) usage 
   RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
   ```

1. 샘플 정책 파일을 `config.resourcesDirectory` 의 속성 [!DNL flashaccess-refimpl.properties].
