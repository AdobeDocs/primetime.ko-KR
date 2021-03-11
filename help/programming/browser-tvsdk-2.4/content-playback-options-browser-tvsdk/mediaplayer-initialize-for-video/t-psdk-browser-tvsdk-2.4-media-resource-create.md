---
description: MediaResource 클래스는 MediaPlayer 인스턴스에서 로드할 내용을 나타냅니다.
title: 미디어 리소스 만들기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# 미디어 리소스 {#create-a-media-resource} 만들기

MediaResource 클래스는 MediaPlayer 인스턴스에서 로드할 내용을 나타냅니다.

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
    <td colname="col2"> <p>미디어 매니페스트/재생 목록의 URL을 나타내는 문자열. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>지정된 파일 유형에 해당하는 <span class="codeph"> MediaResource.Type </span> 열거형의 다음 멤버 중 하나: </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4  </span> - ISO 기본 미디어 파일 형식(MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS  </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> 대시  </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>메타데이터 </p> </td> 
    <td colname="col2"> <p>로드할 콘텐츠에 대한 사용자 정의 정보를 포함할 수 있는 <span class="codeph"> 메타데이터 </span> 클래스의 인스턴스입니다. 컨텐츠의 예는 기본 컨텐츠 내에 배치할 대체 컨텐츠나 광고 컨텐츠입니다. 광고를 사용하는 경우 이 생성자를 사용하기 전에 <span class="codeph"> AuditudeSettings </span>를 설정하십시오. 자세한 내용은 <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">광고 삽입-메타데이터</a>를 참조하십시오. </p> <p>팁: 미디어 리소스를 만들 때 <span class="codeph"> forceFlash </span> 매개 변수를 사용하여 필요한 경우 Flash 폴백을 강제 적용할 수 있습니다. 현재 모든 기능(예: 라이브 광고 워크플로우)이 브라우저 TV SDK에서 지원되지 않으므로 유용할 수 있습니다. Flash 폴백은 비디오 컨텐츠를 재생하는 데 사용됩니다. </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >브라우저 TVSDK는 특정 유형의 컨텐츠에 대해서만 재생을 지원합니다. 다른 유형의 콘텐트를 로드하려고 하면 Browser TVSDK에서 오류 이벤트를 전달합니다.

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

1. MediaPlayer 인스턴스를 로드합니다. 자세한 내용은 MediaPlayer](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md)에서 미디어 리소스 로드를 참조하십시오.[
