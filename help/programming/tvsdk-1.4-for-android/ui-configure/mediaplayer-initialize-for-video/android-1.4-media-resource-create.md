---
description: 각 새 비디오 콘텐츠에 대해 비디오 콘텐츠에 대한 정보로 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다. MediaResource 클래스는 MediaPlayer 인스턴스가 로드하는 콘텐츠를 나타냅니다.
title: 미디어 리소스 만들기
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 미디어 리소스 만들기 {#create-a-media-resource}

각 새 비디오 콘텐츠에 대해 비디오 콘텐츠에 대한 정보로 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다. MediaResource 클래스는 MediaPlayer 인스턴스가 로드하는 콘텐츠를 나타냅니다.

1. 만들기 `MediaResource` 미디어에 대한 정보를 `MediaResource` 생성자입니다.

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
    <td colname="col2"> <p>미디어의 매니페스트/재생 목록의 URL을 나타내는 문자열입니다. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>유형 </p> </td> 
    <td colname="col2"> <p>다음 멤버 중 하나 <span class="codeph"> MediaResource.Type </span> 표시된 파일 형식에 해당하는 열거형: 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>메타데이터 </p> </td> 
    <td colname="col2"> <p>의 인스턴스 <span class="codeph"> 메타데이터 </span> 클래스로, 로드할 컨텐츠에 대한 사용자 지정 정보가 포함될 수 있습니다. </p> <p>컨텐츠의 예로는 기본 컨텐츠 내에 배치할 대체 컨텐츠 또는 광고 컨텐츠가 있습니다. 광고를 사용하는 경우 설정 <span class="codeph"> Auditude 설정 </span>. 자세한 내용은 <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Ad Insertion 메타데이터 </a>. </p> </td> 
    </tr> 
    </tbody> 
    </table>

   >[!IMPORTANT]
   >
   >TVSDK는 특정 유형의 콘텐츠에 대해서만 재생을 지원합니다. 다른 유형의 콘텐츠를 로드하려고 하면 TVSDK가 오류 이벤트를 전달합니다.
   >
   >MP4 VOD(video-on-demand) 컨텐츠의 경우 TVSDK는 트릭 플레이, ABR(Adaptive Bit Rate) 스트리밍, 광고 삽입, 폐쇄 캡션 또는 DRM을 지원하지 않습니다.

   다음 코드는 `MediaResource` 인스턴스:

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
   >이때 다음을 사용할 수 있습니다 `MediaResource` 접근자(getter)를 사용하여 리소스의 유형, URL 및 메타데이터를 검사합니다.

1. 다음을 사용하여 미디어 리소스를 로드합니다.

   * MediaPlayer 인스턴스.

     자세한 내용은 [MediaPlayer에서 미디어 리소스 로드](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` 자세한 내용은 [MediaPlayerItemLoader를 사용하여 미디어 리소스 로드](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >백그라운드 스레드에 미디어 리소스를 로드하지 마십시오. 대부분의 TVSDK 작업은 기본 스레드에서 실행되어야 하며 백그라운드 스레드에서 실행되면 작업에서 오류가 발생하여 종료될 수 있습니다.
