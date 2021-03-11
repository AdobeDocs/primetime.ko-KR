---
description: 브라우저 TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 DASH 기능을 지원합니다.
title: 지원되는 대시 기능
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---


# 지원되는 대시 기능{#supported-dash-features}

브라우저 TVSDK는 비디오 애플리케이션에 기능을 추가하기 위해 구현할 수 있는 다양한 DASH 기능을 지원합니다.

* [DASH Core 재생 기능](#dash-core-playback)
* [DASH 고급 재생 기능](#dash-advanced-playback)
* [DASH 컨텐츠 보호 기능](#dash-content-protection)
* [DASH 코어 광고 삽입 기능](#dash-core-ad-insertion)
* [대시 고급 광고 삽입 기능](#dash-advanced-insertion-features)
* [대시 통합](#dash-integrations)

>[!TIP]
>
>아래 기능 매트릭스 표에서 ![](assets/supported15.png)
>는 현재 릴리스에서 기능이 지원됨을 의미합니다.

지원되는 기능은 다음과 같습니다.

<!-- 

<table id="table_lrb_p2g_xx"> 
 <title>DASH integrations</title> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col6" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Category </th> 
    <th colname="col2" class="entry"> Content type </th> 
    <th colname="col3" class="entry"> Feature </th> 
    <th colname="col6" align="center" class="entry"> 
     <lines>
       HTML5 FF, IE, Chrome, Android Chrome
     </lines> </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_14D9248BD1D8410E83AD27DB4AB3B6ED" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_EFA853CB763446B3B37F2CF6BCC53EE1" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Billing </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_B3A4E5937CEC4052977C08767219BC2B" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Browserify </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_3330E81B86C84AD391AEBFDFE911A47F" /> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## 대시 통합 {#dash-integrations}

| 카테고리 | 컨텐츠 유형 | 기능 | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| 통합 | VOD + 라이브 | Adobe Analytics VHL 통합 | ![](assets/supported15.png) |
| 통합 | VOD + 라이브 | 청구 | ![](assets/supported15.png) |
| 통합 | VOD + 라이브 | 검색 | ![](assets/supported15.png) |

## DASH 고급 광고 삽입 기능(CSAI) {#dash-advanced-insertion-features}

| 카테고리 | 컨텐츠 유형 | 기능 | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD | 광고 전용 | 지원되지 않음 |
| Ad Insertion | VOD | 타깃팅 매개 변수 | VOD만 |
| Ad Insertion | VOD | 사용자 지정 매개 변수 | VOD만 |
| Ad Insertion | VOD + 라이브 | 맞춤형 광고 정책 | 지원되지 않음 |
| Ad Insertion | VOD + 라이브 | 레이지 광고 로딩 | 지원되지 않음 |
| Ad Insertion | VOD | 컴패니언 광고, 배너 광고 및 클릭 가능한 광고 | 지원되지 않음 |
| Ad Insertion | VOD | VPAID 2.0 | 지원되지 않음 |

## DASH 코어 광고 삽입 기능(CSAI) {#dash-core-ad-insertion}

| 카테고리 | 컨텐츠 유형 | 기능 | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD + 라이브 | 프리롤 | VOD만 |
| Ad Insertion | VOD + 라이브 | 중롤 | VOD만 |
| Ad Insertion | VOD + 라이브 | 포스트롤 | VOD만 |
| Ad Insertion | FER VOD | 광고 해상도 및 행동 | 지원되지 않음 |
| Ad Insertion | VOD + 라이브 | 기본 광고 정책 | VOD만 |
| Ad Insertion | VOD + 라이브 | VAST 2.0/3.0 | VOD만 |
| Ad Insertion | VOD + 라이브 | VMAP 1.0 | VOD만 |
| Ad Insertion | VOD + 라이브 | CRS v3.1 | VOD만 |

## DASH 컨텐츠 보호 기능 {#dash-content-protection}

<table id="table_hrb_p2g_xx">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 카테고리 </th> 
   <th colname="col2" class="entry"> 컨텐츠 유형 </th> 
   <th colname="col3" class="entry"> 기능 </th> 
   <th colname="col6" class="entry"> HTML5 FF, IE, Chrome, Android Chrome</th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 컨텐츠 보호 </td> 
   <td colname="col2"> VOD + 라이브 </td> 
   <td colname="col3"> AES-128 </td> 
   <td colname="col6"> 지원되지 않음 </td>
  </tr> 
  <tr> 
   <td colname="col1"> 컨텐츠 보호 </td> 
   <td colname="col2"> VOD + 라이브 </td> 
   <td colname="col3"> 샘플-AES </td> 
   <td colname="col6"> 지원되지 않음 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 컨텐츠 보호 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3"> DRM </td> 
   <td colname="col6"> 
    <ul id="ul_irb_p2g_xx"> 
     <li id="li_C4643F2978BC4C8ABDB3E6C72C75A468">Widevin on 
      <ul id="ul_7047EA49AA3F40FE8F90E0ED6C028D83"> 
       <li id="li_B575735388D74D789D56BF373A470A6D">Chrome </li> 
       <li id="li_855146E4AC3A48E69B65F0022E1C0156">Firefox 47+ </li> 
       <li id="li_BC06B0A6EAAC4FC991C713775A8BB4DA">Chromecast </li> 
      </ul> </li> 
     <li id="li_D48B51C2208F423CB85D08886C2E1C66">Windows 8.1 및 Edge의 Internet Explorer에서 재생 </li> 
     <li id="li_2786AC19387241A296E015EE6FD07F2D">Windows Firefox용 Adobe 액세스(비디오 전용) </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## DASH 고급 재생 기능 {#dash-advanced-playback}

| 카테고리 | 컨텐츠 유형 | 기능 | HTML5, FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| 재생 | VOD | 오프셋 시 재생 | ![](assets/supported15.png) |
| 재생 | VOD | 오디오 전용 재생 | ![](assets/supported15.png) |
| 재생 | VOD | 트릭 플레이 | ![](assets/supported15.png) |
| 재생 | VOD | 부드러운 트릭 재생 | ![](assets/supported15.png) |
| 재생 | VOD + 라이브 | ID3 구문 분석 | 지원되지 않음 |
| 재생 | VOD | 다중 기간 지원 | VOD만 |
| 재생 | VOD + 라이브 | 토큰화된 스트림 | 지원되지 않음 |
| 재생 | VOD + 라이브 | 청구 | ![](assets/supported15.png) |
| 재생 | VOD + 라이브 | 검색 | ![](assets/supported15.png) |

## DASH 코어 재생 기능 {#dash-core-playback}

| 카테고리 | 컨텐츠 유형 | 기능 | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| 재생 | VOD + 라이브 | 일반 재생(재생, 일시 정지, 검색) | ![](assets/supported15.png) |
| 재생 | FER VOD | 일반 재생(재생, 일시 정지, 검색) | 지원되지 않음 |
| 재생 | VOD + 라이브 | 적응형 비트 전송률 | ![](assets/supported15.png) |
| 재생 | VOD + 라이브 | 608/708 캡션 | ![](assets/supported15.png) |
| 재생 | VOD + 라이브 | WebVTT | VOD만 |
| 재생 | VOD + 라이브 | 페일오버 | VOD만 |
| 재생 | VOD + 라이브 | QoS 및 플레이어 알림 | ![](assets/supported15.png) |
| 재생 | VOD + 라이브 | 쿠키 헤더 지원 | ![](assets/supported15.png) |
| 재생 | VOD + 라이브 | 버퍼 컨트롤 매개 변수 설정 | ![](assets/supported15.png) |
| 재생 | VOD + 라이브 | 적응형 비트 전송률 컨트롤 설정 | ![](assets/supported15.png) |
| 재생 | VOD + 라이브 | 사용자 지정 태그(EventStream) | VOD 전용(인라인) |
| 재생 | VOD + 라이브 | 지연 바인딩 오디오 | VOD만 |
| 재생 | VOD + 라이브 | 302 리디렉션 | VOD만 |