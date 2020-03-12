---
description: MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-description: MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-title: 미디어 리소스 만들기
title: 미디어 리소스 만들기
uuid: 3d03d92f-69b3-4da8-9b16-25a264115ae5
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 미디어 리소스 만들기 {#create-a-media-resource}

새로운 각 비디오 컨텐츠에 대해 비디오 컨텐츠에 대한 정보를 사용하여 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다.

MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.

1. 미디어에 `MediaResource` 대한 정보를 생성자에게 전달하여 `MediaResource` 만듭니다.

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
      <td colname="col2"> <p>미디어의 매니페스트/재생 목록의 URL을 나타내는 문자열. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>표시된 파일 유형에 해당하는 다음 문자열 값 중 하나: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - ISO 기본 미디어 파일 포맷(MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> 메타데이터</span> </td> 
      <td colname="col2"> <p>로드할 컨텐츠에 대한 <span class="codeph"> 사용자</span> 지정 정보가 포함될 수 있는 Metadata 클래스의 인스턴스입니다. </p> <p>컨텐츠의 예로는 대체 컨텐츠 또는 기본 컨텐츠 내에 배치할 광고 컨텐츠가 있습니다. 광고를 사용하는 경우 이 생성자를 사용하기 <span class="codeph"> 전에 AuditudeSettings</span> 설정을 설정하십시오. 자세한 내용은 광고 삽입 <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> 메타데이터를 참조하십시오</a>. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK는 특정 유형의 컨텐츠에 대해서만 재생을 지원합니다. 다른 유형의 컨텐츠를 로드하려고 하면 TVSDK가 오류 이벤트를 전달합니다.
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
   >이때 접근자(getter)를 사용하여 리소스의 유형, URL 및 메타데이터를 검사할 수 있습니다. `MediaResource`

1. 다음 중 하나를 사용하여 미디어 리소스를 로드합니다.

   * MediaPlayer 인스턴스.

      자세한 내용은 Mediaplayer [에서 미디어 리소스 로드를 참조하십시오](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` 자세한 내용은 Mediaplayer에서 [미디어 리소스 로드를 참조하십시오](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).

