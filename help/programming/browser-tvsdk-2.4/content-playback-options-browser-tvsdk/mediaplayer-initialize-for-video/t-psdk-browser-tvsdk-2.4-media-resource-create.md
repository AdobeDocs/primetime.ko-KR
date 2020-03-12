---
description: MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-description: MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.
seo-title: 미디어 리소스 만들기
title: 미디어 리소스 만들기
uuid: c25c037e-e9a0-430c-a150-b75a9ac051b1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 미디어 리소스 만들기 {#create-a-media-resource}

MediaResource 클래스는 MediaPlayer 인스턴스가 로드할 컨텐츠를 나타냅니다.

1. 미디어에 `MediaResource` 대한 정보를 생성자에게 전달하여 `MediaResource` 만듭니다.

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
    <td colname="col2"> <p>MediaResource.Type <span class="codeph"> </span> 열거형의 다음 멤버 중 하나는 표시된 파일 형식에 해당합니다. </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - ISO 기본 미디어 파일 포맷(MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> 대시 </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>메타데이터 </p> </td> 
    <td colname="col2"> <p>로드할 컨텐츠에 대한 <span class="codeph"> 사용자 지정 정보가 포함될 수 있는 Metadata </span> 클래스의 인스턴스입니다. 컨텐츠의 예로는 대체 컨텐츠 또는 기본 컨텐츠 내에 배치할 광고 컨텐츠가 있습니다. 광고를 사용하는 경우 이 생성자를 <span class="codeph"> 사용하기 </span> 전에 AuditudeSettings를 설정하십시오. 자세한 내용은 광고 <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">삽입 메타데이터를</a>참조하십시오. </p> <p>팁: 필요한 경우 미디어 리소스를 만들 때 force Flash <span class="codeph"> 매개 변수를 사용하여 Flash </span> 폴백을 강제 적용할 수 있습니다. 이 기능은 현재 브라우저 TVSDK에서 일부 기능(예: 라이브 광고 워크플로우)이 지원되지 않으므로 유용할 수 있습니다. Flash 폴백은 비디오 컨텐츠를 재생하는 데 사용됩니다. </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >브라우저 TVSDK는 특정 유형의 컨텐츠에 대해서만 재생을 지원합니다. 다른 유형의 콘텐츠를 로드하려고 하면 Browser TVSDK에서 오류 이벤트를 전달합니다.

   다음 코드는 `MediaResource` 인스턴스를 만듭니다.

   ```js
   //create a MediaResource instance pointing to some HLS content 
   Metadata metadata = //TODO: create metadata here 
   mediaResource = new AdobePSDK.MediaResource ( 
         "https://www.example.com/video/some-video.m3u8", 
         AdobePSDK.MediaResourceType.HLS,  
         metadata);
   ```

   >[!TIP]
   >
   >이후에는 언제든지 `MediaResource` 접근자(getter)를 사용하여 리소스의 유형, URL 및 메타데이터를 검사할 수 있습니다.

1. MediaPlayer 인스턴스를 로드합니다. 자세한 내용은 MediaPlayer [에서 미디어 리소스 로드를 참조하십시오](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
