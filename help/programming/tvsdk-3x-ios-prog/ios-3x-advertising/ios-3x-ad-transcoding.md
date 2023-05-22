---
description: 일부 타사 광고(또는 광고 크리에이티브)는 비디오 형식이 HLS와 호환되지 않으므로 HTTP 라이브 스트리밍(HLS) 콘텐츠 스트림에 결합할 수 없습니다. Primetime 광고 삽입 및 TVSDK는 선택적으로 호환되지 않는 광고를 호환되는 M3U8 비디오로 다시 패키징하려고 시도할 수 있습니다.
title: Adobe 크리에이티브 리패키징 서비스를 사용하여 호환되지 않는 광고 리패키지
exl-id: 86a8bd94-4de0-4aba-b6ee-4e0e1ee864c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Adobe 크리에이티브 리패키징 서비스를 사용하여 호환되지 않는 광고 리패키지 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

일부 타사 광고(또는 광고 크리에이티브)는 비디오 형식이 HLS와 호환되지 않으므로 HTTP 라이브 스트리밍(HLS) 콘텐츠 스트림에 결합할 수 없습니다. Primetime 광고 삽입 및 TVSDK는 선택적으로 호환되지 않는 광고를 호환되는 M3U8 비디오로 다시 패키징하려고 시도할 수 있습니다.

에이전시 광고 서버, 인벤토리 파트너 또는 광고 네트워크와 같은 다양한 타사에서 제공하는 광고는 종종 점진적 다운로드 MP4와 같은 호환되지 않는 형식으로 전달됩니다.

TVSDK에 호환되지 않는 광고가 처음 발생하면 플레이어는 광고를 무시하고 Primetime 광고 삽입 백 엔드의 일부인 CRS(Creative Repackaging Service)에 광고를 호환되는 형식으로 다시 패키징하라는 요청을 보냅니다. CRS는 광고의 여러 비트 전송률 M3U8 렌디션을 생성하고 이러한 렌디션을 Primetime CDN(Content Delivery Network)에 저장합니다. 다음에 TVSDK가 해당 광고를 가리키는 광고 응답을 받으면 플레이어는 CDN에서 HLS 호환 M3U8 버전을 사용합니다.

이 선택적 기능을 활성화하려면 Adobe 담당자에게 문의하십시오.

## CRS 광고 게재에 대한 여러 CDN 지원 {#section_900FDDA5454143718F1EB4C9732C8E1C}

기본 CRS(Creative Repackaging Service) 시나리오는 하나의 CDN(Content Data Network)을 사용하는 것이지만, 둘 이상의 CDN에 CRS 에셋을 배포할 수 있습니다.

다음과 같은 이유로 여러 CDN을 사용할 수 있습니다.

* 대규모 보기 이벤트에 대한 확장 요구 사항.
* CRS 에셋의 CDN 소스와 기본 컨텐츠의 CDN 소스를 일치시키기 위한 요구 사항입니다.

TVSDK URL 변환기 API를 사용하여 CRS가 제공하는 기본 URL을 변환할 수 있습니다.

다음은 TVSDK의 API 추가 사항입니다.

* `PTURLTransformer` TVSDK에서 요청한 CRS 광고 URL을 변환하는 데 필요한 메서드를 설명하는 프로토콜입니다. 애플리케이션은 이 프로토콜을 구현하고 필요한 방법에 대한 구현을 제공할 수 있다.

* `PTDefaultURLTransformer` TVSDK에서 만들어지고 를 구현하는 기본 URL 변환기 인스턴스 `PTURLTransformer` 프로토콜. 응용 프로그램은 이 클래스를 재정의하거나 게시물 URL 변환 처리기를 추가할 수 있습니다. 이 처리기는 기본 변환이 적용된 후 응용 프로그램에서 URL 요청을 변경하려고 할 때 유용합니다.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` 에 제공되는 setter 메서드 `PTNetworkConfiguration` 을(를) 설정할 메타데이터 인스턴스 `PTURLTransformer` 구현.

>[!IMPORTANT]
>
>앱 구현은 다음을 확인해야 합니다. `PTURLTransformerInputType` 열거형이며 유형의 URL만 변환 `PTURLTransformerInputTypeCRSCreative` CRS를 위해서.

다음 코드 샘플은 응용 프로그램에서 기본 호스트 구성 요소를 다른 문자열로 변경하는 방법을 보여 줍니다(예: `cdn.mycrsdomain.com`):

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
