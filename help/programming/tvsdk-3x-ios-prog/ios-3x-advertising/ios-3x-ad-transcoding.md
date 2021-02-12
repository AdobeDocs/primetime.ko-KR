---
description: 비디오 형식이 HLS와 호환되지 않으므로 일부 타사 광고(또는 크리에이티브)를 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오에 선택적으로 재패키징할 수 있습니다.
seo-description: 비디오 형식이 HLS와 호환되지 않으므로 일부 타사 광고(또는 크리에이티브)를 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오에 선택적으로 재패키징할 수 있습니다.
seo-title: Adobe Creative Repackaging Service를 사용하여 호환되지 않는 광고 재패키지
title: Adobe Creative Repackaging Service를 사용하여 호환되지 않는 광고 재패키지
uuid: 56a2405d-b395-4fea-820d-343590be7c19
translation-type: tm+mt
source-git-commit: cecc559480b9b52c412fefff4361603d6f14caf7
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}를 사용하여 호환되지 않는 광고를 재패키징합니다.

비디오 형식이 HLS와 호환되지 않으므로 일부 타사 광고(또는 크리에이티브)를 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오에 선택적으로 재패키징할 수 있습니다.

광고 대행사 광고 서버, 인벤토리 파트너 또는 광고 네트워크 등 다양한 제3자로부터 제공되는 광고는 종종 점진적 다운로드 MP4와 같은 호환되지 않는 형식으로 제공됩니다.

TVSDK에서 처음에 호환되지 않는 광고가 발생하면 플레이어는 광고를 무시하고 Primetime 광고 삽입 백 엔드의 일부인 CRS(Creative Repackaging Service)에 광고를 재패키징하여 호환되는 포맷으로 재패키징할 것을 요청합니다. CRS는 광고의 다중 비트 전송률 M3U8 변환을 생성하고 이러한 변환을 Primetime CDN(Content Delivery Network)에 저장하려고 합니다. 다음 번에 TVSDK가 해당 광고를 가리키는 광고 응답을 받으면, 플레이어는 CDN의 HLS 호환 M3U8 버전을 사용합니다.

이 선택 기능을 활성화하려면 Adobe 담당자에게 문의하십시오.

## CRS 광고 전달에 대한 여러 CDN 지원 {#section_900FDDA5454143718F1EB4C9732C8E1C}

기본 CRS(Creative Repackaging Service) 시나리오는 하나의 CDN(Content Data Network)을 사용하는 것이지만, 두 개 이상의 CDN에 CRS 자산을 배포할 수 있습니다.

다음과 같은 이유로 여러 CDN을 사용할 수 있습니다.

* 큰 보기 이벤트에 대해 크기를 확대해야 하는 요구 사항입니다.
* CRS 자산의 CDN 소스를 기본 컨텐츠의 CDN 소스와 일치시키는 요구 사항입니다.

TVSDK URL Transformer API를 사용하여 CRS에서 제공하는 기본 URL을 변환할 수 있습니다.

TVSDK에 추가된 API는 다음과 같습니다.

* `PTURLTransformer` TVSDK에서 요청한 CRS 광고 URL을 변형하는 데 필요한 메서드를 설명하는 프로토콜입니다. 애플리케이션은 이 프로토콜을 구현하고 필요한 메서드에 대한 구현을 제공할 수 있습니다.

* `PTDefaultURLTransformer` TVSDK에서 생성되어 프로토콜을 구현하는 기본 URL  `PTURLTransformer` 변환기 인스턴스입니다. 응용 프로그램은 이 클래스를 재정의하거나 게시물 URL 변환 핸들러를 추가할 수 있습니다. 이 핸들러는 기본 변환이 적용된 후 응용 프로그램에서 URL 요청을 변경할 때 유용합니다.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` 구현을 설정하기 위해  `PTNetworkConfiguration` 메타데이터 인스턴스에 제공되는 setter  `PTURLTransformer` 메서드입니다.

>[!IMPORTANT]
>
>앱 구현은 `PTURLTransformerInputType` 열거형을 확인하고 CRS에 대해 `PTURLTransformerInputTypeCRSCreative` 유형의 URL만 변환해야 합니다.

다음 코드 샘플은 응용 프로그램에서 기본 호스트 구성 요소를 다른 문자열(예: `cdn.mycrsdomain.com`)로 변경할 수 있는 방법을 보여 줍니다.

```
// The sample code below uses Non-ARC code 
PTNetworkConfiguration *networkConfiguration = [[[PTNetworkConfiguration alloc] init] autorelease]; 
   
PTDefaultURLTransformer *defaultTransformer = [[[PTDefaultURLTransformer alloc] init] autorelease]; 
    [defaultTransformer addPostURLTransformHandler:^NSString *(NSString *url, PTURLTransformerInputType type) { 
        if (type == PTURLTransformerInputTypeCRSCreative) { 
            return [url stringByReplacingOccurrencesOfString:[NSURL URLWithString:url].host  
              withString:@"cdn.mycrsdomain.com"]; 
        } 
            return url; 
    }]; 
  
[networkConfiguration setURLTransformer:defaultTransformer]; 
   
// metadata is the PTMetadata instance set on a PTMediaPlayerItem instance. 
[metadata setMetadata:[self getNetworkConfiguration] forKey:PTNetworkConfigurationMetadataKey];
```
