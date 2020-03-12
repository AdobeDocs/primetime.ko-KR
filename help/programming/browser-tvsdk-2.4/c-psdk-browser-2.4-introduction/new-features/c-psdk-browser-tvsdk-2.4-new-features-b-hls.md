---
description: Browser TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 HLS 기능을 지원합니다.
seo-description: Browser TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 HLS 기능을 지원합니다.
seo-title: 지원되는 HLS 기능
title: 지원되는 HLS 기능
uuid: 033d81f8-cea4-4687-b2fb-1524d9164d39
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 지원되는 HLS 기능 {#supported-hls-features}

Browser TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 HLS 기능을 지원합니다.

* [HLS Core 재생](#hls-core-playback)
* [HLS 고급 재생 기능](#hls-advanced-playback)
* [HLS 컨텐츠 보호 기능](#hls-content-protection)
* [HLS 코어 광고 삽입 기능](#hls-core-ad-insertion)
* [HLS 고급 광고 삽입 기능](#hls-advanced-ad-insertion)
* [HLS 통합](#hls-integrations)

>[!TIP]
>
>아래 기능 매트릭스 표에서 ![지원되는 아이콘은](assets/supported15.png) 현재 릴리스에서 기능이 지원됨을 의미합니다.

>[!TIP]
>
>Safari 열 &quot;플랫폼 제한&quot;은 해당 플랫폼에서 지원 구현을 허용하지 않으므로 사용 사례가 지원되지 않음을 의미합니다. 삽입의 경우 SSSAI를 사용합니다. 중요한 재생 제한 사항이 있는 경우 플랫폼이 광고 삽입 사용 사례를 지원할 때까지 Safari에서 Flash로 강제 폴백하십시오.

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

지원되는 기능은 다음과 같습니다.

<!-- 

Removed Nielsen row 
<table id="table_D9E2D82992554905A0A551CC71AFA189"> 
 <title>HLS integrations</title> 
 <tgroup cols="6"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col4" colwidth="*" /> 
  <colspec colnum="5" colname="col5" colwidth="*" /> 
  <colspec colnum="6" colname="col7" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" morerows="1" class="entry"> Category </th> 
    <th colname="col2" morerows="1" class="entry"> Content type </th> 
    <th colname="col3" morerows="1" class="entry"> Feature </th> 
    <th colname="col4" morerows="1" class="entry"> Flash </th> 
    <th namest="col5" nameend="col7" class="entry"> HTML5 </th> 
   </tr> 
   <tr> 
    <th colname="col5" class="entry"> FF, IE, Chrome, Android Chrome </th> 
    <th colname="col7" class="entry"> Safari, iOS Safari </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## HLS 통합 {#hls-integrations}

| 카테고리 | 컨텐츠 유형 | 기능 | Flash | HTML5:FF, IE, Chrome, Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 통합 | VOD + 라이브 | Adobe Analytics VHL 통합 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |

## HLS 고급 광고 삽입 기능(CSAI) {#hls-advanced-ad-insertion}

| 카테고리 | 컨텐츠 유형 | 기능 | Flash | HTML5:FF, IE, Chrome, Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 광고 삽입 | VOD | 광고 전용 | 지원되지 않음 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 광고 삽입 | VOD + 라이브 | 타깃팅 매개 변수 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 광고 삽입 | VOD + 라이브 | 맞춤형 광고 정책 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 광고 삽입 | VOD + 라이브 | 레이지 광고 로딩 | ![지원되는 아이콘](assets/supported15.png) | 지원되지 않음 | 플랫폼 제한 |
| 광고 삽입 | VOD | 컴패니언 광고, 배너 광고 및 클릭 가능한 광고 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 광고 삽입 | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## HLS 핵심 광고 삽입 기능(CSAI) {#hls-core-ad-insertion}

| 카테고리 | 컨텐츠 유형 | 기능 | Flash | HTML5:FF, IE, Chrome, Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 광고 삽입 | VOD + 라이브 | 프리롤 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 광고 삽입 | VOD + 라이브 | 중롤 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 광고 삽입 | VOD + 라이브 | 포스트롤 | VOD만 | VOD만 | VOD만 |
| 광고 삽입 | FER VOD | 광고 해상도 및 비헤이비어 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 광고 삽입 | VOD + 라이브 | 기본 광고 정책 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 광고 삽입 | VOD + 라이브 | VAST 2.0/3.0 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 광고 삽입 | VOD + 라이브 | VMAP 1.0 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 광고 삽입 | VOD + 라이브 | CRS v3.1 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |

## HLS 컨텐츠 보호 기능 {#hls-content-protection}

| 카테고리 | 컨텐츠 유형 | 기능 | Flash | HTML5:FF, IE, Chrome, Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 컨텐츠 보호 | VOD + 라이브 | AES-128 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 컨텐츠 보호 | VOD + 라이브 | 샘플-AES | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 컨텐츠 보호 | VOD | DRM | Adobe Access | 지원되지 않음 | FairPlay |

## HLS 고급 재생 기능 {#hls-advanced-playback}

| 카테고리 | 컨텐츠 유형 | 기능 | Flash | HTML5:FF, IE, Chrome, Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 재생 | VOD | 오프셋 재생 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | VOD | 오디오 전용 재생 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | VOD | 트릭 플레이 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | VOD | 매끄러운 트릭 재생 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 재생 | VOD + 라이브 | ID3 구문 분석 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 지원되지 않음 |
| 재생 | VOD + 라이브 | 비연속성 마커 지원 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | VOD + 라이브 | 토큰화된 스트림 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 재생 | VOD + 라이브 | 청구 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | VOD + 라이브 | 검색 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |

## HLS 코어 재생 {#hls-core-playback}

| 카테고리 | 컨텐츠 유형 | 기능 | Flash | HTML5:FF, IE, Chrome, Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 재생 | VOD + 라이브 | 일반 재생(재생, 일시 중지, 검색) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | FER VOD | 일반 재생(재생, 일시 중지, 검색) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | VOD + 라이브 | 적응형 비트 전송률 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | VOD + 라이브 | 608/708 캡션 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | VOD + 라이브 | WebVTT | ![지원되는 아이콘](assets/supported15.png) | VOD만 | VOD만 |
| 재생 | VOD + 라이브 | 매니페스트 장애 조치(Manifest Failover) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) |
| 재생 | VOD + 라이브 | 고급 장애 조치 | ![지원되는 아이콘](assets/supported15.png) | VOD만 | 플랫폼 제한 |
| 재생 | VOD + 라이브 | QoS 및 플레이어 알림 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 제한된 QoS 지원 |
| 재생 | VOD + 라이브 | 쿠키 헤더 지원 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 재생 | VOD + 라이브 | 버퍼 컨트롤 매개 변수 설정 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 재생 | VOD + 라이브 | 적응형 비트 전송률 컨트롤 설정 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 재생 | VOD + 라이브 | 사용자 지정 태그 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 재생 | VOD + 라이브 | 지연 바인딩 오디오 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |
| 재생 | VOD + 라이브 | 302 리디렉션 | ![지원되는 아이콘](assets/supported15.png) | ![지원되는 아이콘](assets/supported15.png) | 플랫폼 제한 |