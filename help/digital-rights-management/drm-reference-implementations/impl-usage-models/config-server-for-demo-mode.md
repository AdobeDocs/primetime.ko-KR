---
description: 'null'
seo-description: 'null'
seo-title: 사용 모델 데모 모드 구성
title: 사용 모델 데모 모드 구성
uuid: f818c7fc-e88f-4fa4-926e-08a1337b28d3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 사용 모델 데모 모드 구성{#configure-usage-model-demo-mode}

참조 구현 서버가 사용 모델 데모용 라이센스를 발급하려면 먼저 서버를 구성하여 4개의 사용 모델 각각에 대해 라이센스가 생성되는 방식을 지정해야 합니다. 따라서 각 사용 모델에 대해 DRM 정책을 지정해야 합니다. 참조 구현에는 [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] 디렉토리에 다음과 같은 샘플 DRM 정책이 포함됩니다.

* `dto-policy.pol` - (직접 다운로드)
* `vod-policy.pol` - (대여/Video-On-Demand)
* `sub-policy.pol` - (구독)
* `ad-policy.pol` - (광고 지원)

>[!NOTE]
>
>이러한 샘플 정책을 자체 DRM 정책으로 대체할 수 있습니다.

1. 다음 속성을 [!DNL flashaccess-refimpl.properties]에서 설정하여 각 사용 모델에 적용할 DRM 정책을 지정합니다.

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

1. 샘플 정책 파일을 [!DNL flashaccess-refimpl.properties]의 `config.resourcesDirectory` 속성에서 지정한 디렉토리로 복사합니다.
