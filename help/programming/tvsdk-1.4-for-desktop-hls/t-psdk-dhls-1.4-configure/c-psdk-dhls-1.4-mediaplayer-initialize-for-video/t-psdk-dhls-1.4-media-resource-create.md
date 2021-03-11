---
description: MediaResource 클래스는 MediaPlayer 인스턴스에서 로드할 내용을 나타냅니다.
title: 미디어 리소스 만들기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# 미디어 리소스 {#create-a-media-resource} 만들기

새로운 각 비디오 컨텐츠에 대해 비디오 컨텐츠에 대한 정보를 사용하여 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다.

MediaResource 클래스는 MediaPlayer 인스턴스에서 로드할 내용을 나타냅니다.

1. 미디어에 대한 정보를 `MediaResource` 생성자에게 전달하여 `MediaResource`을 만듭니다.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 생성자 매개 변수 </th> 
      <th colname="col2" class="entry"> 설명 </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>미디어 매니페스트/재생 목록의 URL을 나타내는 문자열. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>지정된 파일 유형에 해당하는 다음 문자열 값 중 하나: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span>  - ISO 기본 미디어 파일 형식(MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> 메타데이터</span> </td> 
      <td colname="col2"> <p>로드할 콘텐츠에 대한 사용자 정의 정보를 포함할 수 있는 <span class="codeph"> Metadata</span> 클래스의 인스턴스입니다. </p> <p>컨텐츠의 예는 기본 컨텐츠 내에 배치할 대체 컨텐츠나 광고 컨텐츠입니다. 광고를 사용하는 경우 이 생성자를 사용하기 전에 <span class="codeph"> AuditudeSettings</span>를 설정하십시오. 자세한 내용은 <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Ad Insertion 메타데이터</a>를 참조하십시오. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK는 특정 유형의 컨텐츠에 대해서만 재생을 지원합니다. 다른 유형의 콘텐트를 로드하려고 하면 TVSDK에서 오류 이벤트를 전달합니다.
   >
   >MP4 VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 트릭 재생, 적응형 비트 전송률(ABR) 스트리밍, 광고 삽입, 자막 또는 DRM을 지원하지 않습니다.

   다음 코드는 `MediaResource` 인스턴스를 만듭니다.

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >이때 `MediaResource` 접근자(getter)를 사용하여 리소스의 유형, URL 및 메타데이터를 검사할 수 있습니다.

1. 다음 중 하나를 사용하여 미디어 리소스를 로드합니다.

   * MediaPlayer 인스턴스.

      자세한 내용은 Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md)에서 미디어 리소스 로드를 참조하십시오.[
   * `MediaPlayerItemLoader` 자세한 내용은 Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md)에서 미디어 리소스 로드를 참조하십시오.[

