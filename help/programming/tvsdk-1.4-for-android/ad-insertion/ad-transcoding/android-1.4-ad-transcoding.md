---
description: 일부 타사 광고(또는 광고 크리에이티브)는 비디오 형식이 HLS와 호환되지 않으므로 HTTP 라이브 스트리밍(HLS) 콘텐츠 스트림에 결합할 수 없습니다. Primetime 광고 삽입 및 TVSDK는 선택적으로 호환되지 않는 광고를 호환되는 M3U8 비디오로 다시 패키징하려고 시도할 수 있습니다.
title: Adobe 크리에이티브 리패키징 서비스를 사용하여 호환되지 않는 광고 리패키지
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Adobe 크리에이티브 리패키징 서비스를 사용하여 호환되지 않는 광고 리패키지 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

일부 타사 광고(또는 광고 크리에이티브)는 비디오 형식이 HLS와 호환되지 않으므로 HTTP 라이브 스트리밍(HLS) 콘텐츠 스트림에 결합할 수 없습니다. Primetime 광고 삽입 및 TVSDK는 선택적으로 호환되지 않는 광고를 호환되는 M3U8 비디오로 다시 패키징하려고 시도할 수 있습니다.

에이전시 광고 서버, 인벤토리 파트너 또는 광고 네트워크와 같은 다양한 타사에서 제공하는 광고는 종종 점진적 다운로드 MP4와 같은 호환되지 않는 형식으로 전달됩니다.

TVSDK에 호환되지 않는 광고가 처음 발생하면 플레이어는 광고를 무시하고 Primetime 광고 삽입 백 엔드의 일부인 CRS(Creative Repackaging Service)에 광고를 호환되는 형식으로 다시 패키징하라는 요청을 보냅니다. CRS는 광고의 여러 비트 전송률 M3U8 렌디션을 생성하고 이러한 렌디션을 Primetime CDN(Content Delivery Network)에 저장합니다. 다음에 TVSDK가 해당 광고를 가리키는 광고 응답을 받으면 플레이어는 CDN에서 HLS 호환 M3U8 버전을 사용합니다.

이 선택적 기능을 활성화하려면 Adobe 담당자에게 문의하십시오.

CRS에 대한 자세한 내용은 [CRS(Creative Packaging Service)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## CRS 광고 게재에 대한 여러 CDN 지원{#multiple-cdn-support-for-crs-ad-delivery}

기본 CRS(Creative Repackaging Service) 시나리오는 하나의 CDN(Content Data Network)을 사용하는 것이지만, 둘 이상의 CDN에 CRS 에셋을 배포할 수 있습니다.

다음과 같은 이유로 여러 CDN을 사용할 수 있습니다.

* 대규모 보기 이벤트에 대한 확장 요구 사항.
* CRS 에셋의 CDN 소스와 기본 컨텐츠의 CDN 소스를 일치시키기 위한 요구 사항입니다.

TVSDK URL 변환기 API를 사용하여 CRS가 제공하는 기본 URL을 변환할 수 있습니다.

다음은 TVSDK의 API 추가 사항입니다.

* `URLTransformer` TVSDK에서 요청한 CRS 광고 URL을 변환하는 데 필요한 메서드를 설명하는 인터페이스입니다. 애플리케이션은 이 인터페이스를 구현하고 필요한 방법에 대한 구현을 제공할 수 있다.

* `DefaultURLTransformer` TVSDK에서 만들어지고 를 구현하는 기본 URL 변환기 인스턴스 `URLTransformer` 인터페이스. 응용 프로그램은 이 클래스를 재정의하거나 게시물 URL 변환 처리기를 추가할 수 있습니다. 이 처리기는 기본 변환이 적용된 후 응용 프로그램에서 URL 요청을 변경하려고 할 때 유용합니다.

* `NetworkConfiguration.setURLTransformer` 에 제공되는 setter 메서드 `NetworkConfiguration` 을(를) 설정할 메타데이터 인스턴스 `URLTransformer` 구현.

>[!IMPORTANT]
>
>앱 구현은 다음을 확인해야 합니다. `URLTransformerInputType` 열거형이며 유형의 URL만 변환 `URLTransformerInputType.CRSCreative` CRS를 위해서.

다음 코드 샘플은 응용 프로그램에서 기본 호스트 구성 요소를 다른 문자열로 변경하는 방법을 보여 줍니다(예: `cdn.mycrsdomain.com`):

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
