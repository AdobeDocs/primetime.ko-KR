---
description: MediaResource 클래스는 MediaPlayer 인스턴스가 로드하는 콘텐츠를 나타냅니다.
title: 미디어 리소스 만들기
exl-id: d9693ee5-c192-4ac5-925a-d64e629920b4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 미디어 리소스 만들기 {#create-a-media-resource}

각 새 비디오 콘텐츠에 대해 비디오 콘텐츠에 대한 정보로 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다.

MediaResource 클래스는 MediaPlayer 인스턴스가 로드하는 콘텐츠를 나타냅니다.

1. 만들기 `MediaResource` 미디어에 대한 정보를 `MediaResource` 생성자입니다.

   다음 `MediaResource` 생성자에는 다음 매개 변수가 필요합니다.

   <table id="table_22886D6770FB45E99D35D0B90E6CC302"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 생성자 매개 변수 </th> 
      <th colname="col2" class="entry"> 설명 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> <span class="codeph"> url </span> </td> 
      <td colname="col2"> 미디어의 매니페스트/재생 목록의 URL을 나타내는 문자열입니다. </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> 유형 </span> </td> 
      <td colname="col2"> 다음 멤버 중 하나 <span class="codeph"> MediaResource.Type </span> 표시된 파일 형식에 해당하는 enum: 
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282"> 
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li> 
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - ISO 기본 미디어 파일 형식(MP4) </li> 
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> 대시 </span> - MPEG-DASH 미디어 프레젠테이션 설명(MPD) </li> 
      </ul> </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> 메타데이터 </span> </td> 
      <td colname="col2"> 의 인스턴스 <span class="codeph"> 메타데이터 </span> 기본 컨텐츠 내에 배치할 대체 컨텐츠나 광고 컨텐츠와 같이 로드하려는 컨텐츠에 대한 추가 정보를 포함할 수 있는 클래스(사전과 유사한 구조). 광고를 사용하는 경우 설정 <span class="codeph"> Auditude 설정 </span> 이 생성자를 사용하기 전에 <a href="/help/programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-insertion-metadata/android-3x-ad-insertion-metadata.md"> 광고 삽입 메타데이터 </a>. </td> 
   </tr> 
   </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK는 특정 유형의 콘텐츠에 대해서만 재생을 지원합니다. 다른 유형의 콘텐츠를 로드하려고 하면 TVSDK가 오류 이벤트를 전달합니다.
   >
   >MP4 VOD(video-on-demand) 컨텐츠의 경우 TVSDK는 트릭 플레이, ABR(Adaptive Bit Rate) 스트리밍, 광고 삽입, 폐쇄 캡션 또는 DRM을 지원하지 않습니다.

   다음 코드는 `MediaResource` 인스턴스: >

   ```java
   // To do: Create metadata here 
   MediaResource res = new MediaResource( 
     "https://www.example.com/video/some-video.m3u8",  
   MediaResource.Type.HLS, 
     metadata); 
   ```

   이 단계 후에 언제든지 을 사용할 수 있습니다. `MediaResource` 접근자(getter)를 사용하여 리소스의 유형, URL 및 메타데이터를 검사합니다.

1. 다음 옵션 중 하나를 사용하여 미디어 리소스를 로드합니다.

   * MediaPlayer 인스턴스.
   * `MediaPlayerItemLoader` 자세한 내용은 [MediaPlayerItemLoader를 사용하여 미디어 리소스 로드](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >백그라운드 스레드에 미디어 리소스를 로드하지 마십시오. 대부분의 TVSDK 작업은 기본 스레드에서 실행되어야 하며 백그라운드 스레드에서 실행되면 작업에서 오류가 발생하여 종료됩니다.
