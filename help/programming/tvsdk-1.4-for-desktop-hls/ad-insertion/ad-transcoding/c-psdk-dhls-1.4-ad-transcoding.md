---
description: 일부 타사 광고(또는 크리에이티브)는 HLS와 호환되지 않기 때문에 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TVSDK는 호환이 불가능한 광고를 호환되는 M3U8 비디오로 재패키징할 수도 있습니다.
seo-description: 일부 타사 광고(또는 크리에이티브)는 HLS와 호환되지 않기 때문에 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TVSDK는 호환이 불가능한 광고를 호환되는 M3U8 비디오로 재패키징할 수도 있습니다.
seo-title: Adobe Creative Repackaging Service를 사용하여 호환되지 않는 광고 재패키지
title: Adobe Creative Repackaging Service를 사용하여 호환되지 않는 광고 재패키지
uuid: 3bc24185-6b19-4660-bf78-5ccdaf14787a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Adobe Creative Repackaging Service를 사용하여 호환되지 않는 광고 재패키지 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

일부 타사 광고(또는 크리에이티브)는 HLS와 호환되지 않기 때문에 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TVSDK는 호환이 불가능한 광고를 호환되는 M3U8 비디오로 재패키징할 수도 있습니다.

에이전시 광고 서버, 인벤토리 파트너, 광고 네트워크 등 다양한 타사 업체에서 제공하는 광고는 종종 점진적 다운로드 MP4와 같은 호환되지 않는 형식으로 제공됩니다.

TVSDK가 처음에 호환되지 않는 광고를 발견하면 플레이어는 광고를 무시하고 Primetime 광고 삽입 백엔드의 일부인 CRS(Creative Repackaging Service)에 광고를 다시 패키징하여 호환 가능한 포맷으로 다시 패키징하도록 요청합니다. CRS 파섹 다음 번에 TVSDK에서 해당 광고를 가리키는 광고 응답을 받으면 플레이어는 CDN의 HLS 호환 M3U8 버전을 사용합니다.

이 선택 기능을 활성화하려면 Adobe 담당자에게 문의하십시오.

CRS에 대한 자세한 내용은 CRS( [Creative Packaging Service)를](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf)참조하십시오.

## CRS 광고 전달을 위한 다양한 CDN 지원 {#multiple-cdn-support-for-crs-ad-delivery}

기본 Creative Repackaging Service(CRS) 시나리오는 하나의 CDN(Content Data Network)을 사용하는 것이지만 CDN 자산을 둘 이상의 CDN에 배포할 수 있습니다.

다음과 같은 이유로 여러 CDN을 사용할 수 있습니다.

* 대규모 보기 이벤트에 대해 확장해야 하는 요구 사항입니다.
* CRS 자산의 CDN 소스를 기본 컨텐츠의 CDN 소스와 일치시키는 요구 사항입니다.

TVSDK URL Transformer API를 사용하여 CRS 파섹

다음은 TVSDK에 추가된 API입니다.

* `URLTransformer` TVSDK에서 요청하는 CRS 광고 URL을 변형하는 데 필요한 방법을 설명하는 인터페이스입니다. 애플리케이션은 이 인터페이스를 구현하고 필요한 방법에 대한 구현을 제공할 수 있습니다.

* `DefaultURLTransformer` TVSDK에서 생성되어 `URLTransformer` 인터페이스를 구현하는 기본 URL 변환기 인스턴스입니다. 응용 프로그램은 이 클래스를 재정의하거나 게시물 URL 변환 핸들러를 추가할 수 있습니다. 이 핸들러는 기본 변환이 적용된 후 응용 프로그램이 URL 요청을 변경하려고 할 때 유용합니다.

* `NetworkConfiguration.urlTransformer` 구현을 설정하기 위해 `NetworkConfiguration` 메타데이터 인스턴스에 제공되는 setter 메서드입니다 `URLTransformer` .

>[!IMPORTANT]
>
>앱 구현은 `URLTransformerInputType` 열거형을 확인하고 CRS 유형의 URL만 변환해야 `URLTransformerInputType.CRSCreative` 합니다.

다음 코드 샘플에서는 응용 프로그램이 기본 호스트 구성 요소를 다른 문자열(예: `cdn.mycrsdomain.com`)로 변경하는 방법을 보여 줍니다.

```
var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   
var urlTransformer:DefaultURLTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(function (url:String, type:String) { 
    if (type == URLTransformerInputType.CRSCreative) { 
        return url.replace(URLUtil.getServerName(url), "cdn.mycrsdomain.com"); 
    } 
    return url; 
}); 
  
networkConfiguration.urlTransformer = urlTransformer; 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                     networkConfiguration);
```
