---
description: MediaResource 클래스는 MediaPlayer 인스턴스에서 로드할 내용을 나타냅니다.
title: 미디어 리소스 만들기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 미디어 리소스 {#create-a-media-resource} 만들기

새로운 각 비디오 컨텐츠에 대해 비디오 컨텐츠에 대한 정보를 사용하여 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다.

MediaResource 클래스는 MediaPlayer 인스턴스에서 로드할 내용을 나타냅니다.

1. 미디어에 대한 정보를 `MediaResource` 생성자에게 전달하여 `MediaResource`을 만듭니다.

   `MediaResource` 생성자에는 다음 매개 변수가 필요합니다.

   <table id="table_22886D6770FB45E99D35D0B90E6CC302"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 생성자 매개 변수 </th> 
      <th colname="col2" class="entry"> 설명 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> <span class="codeph"> url  </span> </td> 
      <td colname="col2"> 미디어 매니페스트/재생 목록의 URL을 나타내는 문자열. </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> type  </span> </td> 
      <td colname="col2"> 지정된 파일 형식에 해당하는 <span class="codeph"> MediaResource.Type </span> 열거형의 다음 멤버 중 하나: 
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282"> 
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS  </span> - M3U8 </li> 
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF  </span> - ISO 기본 미디어 파일 형식(MP4) </li> 
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> 대시  </span> - MPEG-대시 미디어 프레젠테이션 설명(MPD) </li> 
      </ul> </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> 메타데이터  </span> </td> 
      <td colname="col2"> 기본 컨텐츠 내에 배치할 대체 컨텐츠 또는 광고 내용과 같이, 로드하려는 컨텐츠에 대한 추가 정보를 포함할 수 있는 <span class="codeph"> 메타데이터 </span> 클래스(사전과 같은 구조)의 인스턴스입니다. 광고를 사용하는 경우 이 생성자 <a href="/help/programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-insertion-metadata/android-3x-ad-insertion-metadata.md"> 광고 삽입 메타데이터 </a>을(를) 사용하기 전에 <span class="codeph"> AuditudeSettings </span>를 설정하십시오. </td> 
   </tr> 
   </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK는 특정 유형의 컨텐츠에 대해서만 재생을 지원합니다. 다른 유형의 콘텐트를 로드하려고 하면 TVSDK에서 오류 이벤트를 전달합니다.
   >
   >MP4 VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 트릭 재생, 적응형 비트 전송률(ABR) 스트리밍, 광고 삽입, 자막 또는 DRM을 지원하지 않습니다.

   다음 코드는 `MediaResource` 인스턴스를 만듭니다.        >

   ```java
   // To do: Create metadata here 
   MediaResource res = new MediaResource( 
     "https://www.example.com/video/some-video.m3u8",  
   MediaResource.Type.HLS, 
     metadata); 
   ```

   이 단계 이후 언제든지 `MediaResource` 접근자(getter)를 사용하여 리소스의 유형, URL 및 메타데이터를 검사할 수 있습니다.

1. 다음 옵션 중 하나를 사용하여 미디어 리소스를 로드합니다.

   * MediaPlayer 인스턴스입니다.
   * `MediaPlayerItemLoader` 자세한 내용은 MediaPlayerItemLoader [를 사용하여 미디어 리소스 로드를 참조하십시오](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >배경 스레드에 미디어 리소스를 로드하지 마십시오. 대부분의 TVSDK 작업은 기본 스레드에서 실행되어야 하며 백그라운드 스레드에서 실행되면 작업이 오류를 throw하고 종료됩니다.
