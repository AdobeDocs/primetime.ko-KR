---
description: 새로운 각 비디오 컨텐츠에 대해 비디오 컨텐츠에 대한 정보를 사용하여 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다. MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-description: 새로운 각 비디오 컨텐츠에 대해 비디오 컨텐츠에 대한 정보를 사용하여 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다. MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-title: 미디어 리소스 만들기
title: 미디어 리소스 만들기
uuid: d9fe982a-bedf-445c-b5be-f7918693782a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# 미디어 리소스 {#create-a-media-resource} 만들기

새로운 각 비디오 컨텐츠에 대해 비디오 컨텐츠에 대한 정보를 사용하여 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다. MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.

1. 미디어에 대한 정보를 `MediaResource` 생성자에게 전달하여 `MediaResource`을 만듭니다.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> 생성자 매개 변수 </th> 
    <th colname="col2" class="entry"> 설명 </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>미디어의 매니페스트/재생 목록의 URL을 나타내는 문자열. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>지정된 파일 유형에 해당하는 <span class="codeph"> MediaResource.Type </span> 열거형의 다음 멤버 중 하나: 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS  </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>메타데이터 </p> </td> 
    <td colname="col2"> <p>로드할 컨텐츠에 대한 사용자 지정 정보가 포함될 수 있는 <span class="codeph"> 메타데이터 </span> 클래스의 인스턴스입니다. </p> <p>컨텐츠의 예로는 대체 컨텐츠나 기본 컨텐츠 내에 배치할 광고 컨텐츠가 있습니다. 광고를 사용하는 경우 <span class="codeph"> AuditudeSettings </span>를 설정합니다. 자세한 내용은 <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Ad Insertion 메타데이터 </a>를 참조하십시오. </p> </td> 
    </tr> 
    </tbody> 
    </table>

   >[!IMPORTANT]
   >
   >TVSDK는 특정 유형의 컨텐츠에 대해서만 재생을 지원합니다. 다른 유형의 콘텐트를 로드하려고 하면 TVSDK에서 오류 이벤트를 전달합니다.
   >
   >MP4 VOD(Video-On-Demand) 콘텐츠의 경우 TVSDK는 트릭 플레이, 적응형 비트 전송률(ABR) 스트리밍, 광고 삽입, 자막 또는 DRM을 지원하지 않습니다.

   다음 코드는 `MediaResource` 인스턴스를 만듭니다.

   ```java
   try { 
       // create a MediaResource instance pointing to some HLS content 
       Metadata metadata = //TODO: create metadata  
       MediaResource mediaResource = MediaResource.createFromUrl( 
         "https://www.example.com/video/some-video.m3u8",  
         MediaResource.Type.HLS,  
         metadata); 
   } catch(IllegalArgumentException ex) { 
       // this exception is thrown if the URL does not point  
       // to a valid url. 
   } 
   ```

   >[!TIP]
   >
   >이때 `MediaResource` 접근자(getter)를 사용하여 리소스의 유형, URL 및 메타데이터를 검사할 수 있습니다.

1. 다음을 사용하여 미디어 리소스를 로드합니다.

   * MediaPlayer 인스턴스.

      자세한 내용은 MediaPlayer[에서 미디어 리소스 로드를 참조하십시오.](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md)
   * `MediaPlayerItemLoader` 자세한 내용은 [MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)를 사용하여 미디어 리소스 로드를 참조하십시오.
   >[!IMPORTANT]
   >
   >배경 스레드에 미디어 리소스를 로드하지 마십시오. 대부분의 TVSDK 작업을 주 스레드에서 실행해야 하며 백그라운드 스레드에서 실행하면 작업이 오류를 던지고 종료됩니다.
