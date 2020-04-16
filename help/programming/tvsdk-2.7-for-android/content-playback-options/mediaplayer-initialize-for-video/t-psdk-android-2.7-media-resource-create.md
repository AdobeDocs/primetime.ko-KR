---
description: MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-description: MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-title: 미디어 리소스 만들기
title: 미디어 리소스 만들기
uuid: f34a11a3-dac2-405e-8632-1d9617cc019d
translation-type: tm+mt
source-git-commit: 1b7ec3759561159c55018b4b81f896ecc99a25e8

---


# 미디어 리소스 만들기 {#create-a-media-resource}

새로운 각 비디오 컨텐츠에 대해 비디오 컨텐츠에 대한 정보를 사용하여 MediaResource 인스턴스를 초기화하고 미디어 리소스를 로드합니다.

MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.

1. 미디어에 `MediaResource` 대한 정보를 생성자에게 전달하여 `MediaResource` 만듭니다.

   생성자에는 다음 매개 변수가 필요합니다 `MediaResource` .

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
      <td colname="col2"> 미디어의 매니페스트/재생 목록의 URL을 나타내는 문자열. </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> type </span> </td>
      <td colname="col2"> MediaResource.Type <span class="codeph"> </span> 열거형의 다음 멤버 중 하나, 지정된 파일 형식에 해당합니다.
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - ISO 기본 미디어 파일 포맷(MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> 대시 </span> - MPEG-DASH 미디어 프레젠테이션 설명(MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> 메타데이터 </span> </td>
      <td colname="col2"> Metadata <span class="codeph"> </span> 클래스의 인스턴스(사전 같은 구조)로서, 기본 컨텐츠 내에 배치할 대체 또는 광고 내용과 같이 로드하려는 컨텐츠에 대한 추가 정보가 포함될 수 있습니다. 광고를 사용하는 경우 이 생성자를 <span class="codeph"> 사용하기 </span> 전에 AuditudeSettings를 설정하십시오. </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >TVSDK는 특정 유형의 컨텐츠에 대해서만 재생을 지원합니다. 다른 유형의 컨텐츠를 로드하려고 하면 TVSDK가 오류 이벤트를 전달합니다.
   >
   >MP4 VOD(Video-On-Demand) 컨텐츠의 경우 TVSDK는 트릭 재생, 적응형 비트 전송률(ABR) 스트리밍, 광고 삽입, 자막 또는 DRM을 지원하지 않습니다.

   다음 코드는 `MediaResource` 인스턴스를 만듭니다.

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   이 단계 이후 언제든지 접근자(getter)를 사용하여 리소스의 유형, URL 및 메타데이터를 검사할 수 있습니다. `MediaResource`

1. 다음 옵션 중 하나를 사용하여 미디어 리소스를 로드합니다.

   * MediaPlayer 인스턴스입니다.
   * `MediaPlayerItemLoader` 자세한 내용은 MediaPlayerItemLoader [를 사용하여 미디어 리소스 로드를 참조하십시오](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >백그라운드 스레드에서 미디어 리소스를 로드하지 마십시오. 대부분의 TVSDK 작업은 기본 스레드에서 실행해야 하며 백그라운드 스레드에서 실행하면 작업이 오류를 발생시키고 종료할 수 있습니다.
