---
description: 비디오 형식이 HLS와 호환되지 않으므로 일부 타사 광고(또는 크리에이티브)를 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오에 선택적으로 재패키징할 수 있습니다.
title: Adobe Creative Repackaging Service를 사용하여 호환되지 않는 광고 재패키지
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}를 사용하여 호환되지 않는 광고를 재패키징합니다.

비디오 형식이 HLS와 호환되지 않으므로 일부 타사 광고(또는 크리에이티브)를 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오에 선택적으로 재패키징할 수 있습니다.

광고 대행사 광고 서버, 인벤토리 파트너 또는 광고 네트워크 등 다양한 제3자로부터 제공되는 광고는 종종 점진적 다운로드 MP4와 같은 호환되지 않는 형식으로 제공됩니다.

TVSDK에서 처음에 호환되지 않는 광고가 발생하면 플레이어는 광고를 무시하고 Primetime 광고 삽입 백 엔드의 일부인 CRS(Creative Repackaging Service)에 광고를 재패키징하여 호환되는 포맷으로 재패키징할 것을 요청합니다. CRS는 광고의 다중 비트 전송률 M3U8 변환을 생성하고 이러한 변환을 Primetime CDN(Content Delivery Network)에 저장하려고 합니다. 다음 번에 TVSDK가 해당 광고를 가리키는 광고 응답을 받으면, 플레이어는 CDN의 HLS 호환 M3U8 버전을 사용합니다.

이 선택 기능을 활성화하려면 Adobe 담당자에게 문의하십시오.

CRS에 대한 자세한 내용은 [CRS(Creative Packaging Service)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf)을 참조하십시오.

## CRS 광고 전달에 대한 다중 CDN 지원{#multiple-cdn-support-for-crs-ad-delivery}

기본 CRS(Creative Repackaging Service) 시나리오는 하나의 CDN(Content Data Network)을 사용하는 것이지만, 두 개 이상의 CDN에 CRS 자산을 배포할 수 있습니다.

다음과 같은 이유로 여러 CDN을 사용할 수 있습니다.

* 큰 보기 이벤트에 대해 크기를 확대해야 하는 요구 사항입니다.
* CRS 자산의 CDN 소스를 기본 컨텐츠의 CDN 소스와 일치시키는 요구 사항입니다.

TVSDK URL Transformer API를 사용하여 CRS에서 제공하는 기본 URL을 변환할 수 있습니다.

TVSDK에 추가된 API는 다음과 같습니다.

* `URLTransformer` TVSDK에서 요청한 CRS 광고 URL을 변형하는 데 필요한 메서드를 설명하는 인터페이스입니다. 애플리케이션은 이 인터페이스를 구현하고 필요한 메서드에 대한 구현을 제공할 수 있습니다.

* `DefaultURLTransformer` TVSDK에서 생성되어 인터페이스를 구현하는 기본 URL 변환기  `URLTransformer` 인스턴스입니다. 응용 프로그램은 이 클래스를 재정의하거나 게시물 URL 변환 핸들러를 추가할 수 있습니다. 이 핸들러는 기본 변환이 적용된 후 응용 프로그램에서 URL 요청을 변경할 때 유용합니다.

* `NetworkConfiguration.setURLTransformer` 구현을 설정하기 위해  `NetworkConfiguration` 메타데이터 인스턴스에 제공되는 setter  `URLTransformer` 메서드입니다.

>[!IMPORTANT]
>
>앱 구현은 `URLTransformerInputType` 열거형을 확인하고 CRS에 대해 `URLTransformerInputType.CRSCreative` 유형의 URL만 변환해야 합니다.

다음 코드 샘플은 응용 프로그램에서 기본 호스트 구성 요소를 다른 문자열(예: `cdn.mycrsdomain.com`)로 변경할 수 있는 방법을 보여 줍니다.

```java
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
DefaultURLTransformer urlTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(new DefaultURLTransformer.URLTransformHandler() { 
    @Override 
    public String call(String url, URLTransformerInputType type) { 
        if (type == URLTransformerInputType.CRSCreative) { 
            try { 
                return url.replaceAll(new java.net.URI(url).getHost(), "cdn.mycrsdomain.com"); 
            } catch (URISyntaxException e) { 
            } 
        } 
        return url; 
    } 
}); 
   
networkConfiguration.setURLTransformer(urlTransformer); 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(), networkConfiguration);
```
