---
description: MediaResource 클래스는 MediaPlayer 인스턴스가 로드하는 콘텐츠를 나타냅니다.
title: 미디어 리소스 만들기
exl-id: ab66255d-7848-479a-a8cd-c6113cdd7749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 미디어 리소스 만들기 {#create-a-media-resource}

MediaResource 클래스는 MediaPlayer 인스턴스가 로드하는 콘텐츠를 나타냅니다.

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
    <td colname="col2"> <p>다음 멤버 중 하나 <span class="codeph"> MediaResource.Type </span> 표시된 파일 형식에 해당하는 열거형: </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - ISO 기본 미디어 파일 형식(MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> 대시 </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>메타데이터 </p> </td> 
    <td colname="col2"> <p>의 인스턴스 <span class="codeph"> 메타데이터 </span> 클래스로, 로드할 컨텐츠에 대한 사용자 지정 정보가 포함될 수 있습니다. 컨텐츠의 예로는 기본 컨텐츠 내에 배치할 대체 컨텐츠 또는 광고 컨텐츠가 있습니다. 광고를 사용하는 경우 설정 <span class="codeph"> Auditude 설정 </span> 이 생성자를 사용하기 전에. 자세한 내용은 <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">광고 삽입 메타데이터</a>. </p> <p>팁: 필요한 경우 다음을 사용하여 Flash 폴백을 강제 적용할 수 있습니다. <span class="codeph"> forceFlash </span> 미디어 리소스를 만들 때 매개 변수를 사용합니다. 이 기능은 현재 일부 기능(예: 라이브 광고 워크플로)만 브라우저 TVSDK에서 지원되므로 유용할 수 있습니다. Flash 폴백은 비디오 콘텐츠를 재생하는 데 사용됩니다. </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >브라우저 TVSDK는 특정 유형의 콘텐츠에 대해서만 재생을 지원합니다. 다른 유형의 콘텐츠를 로드하려고 하면 Browser TVSDK에서 오류 이벤트를 전달합니다.

   다음 코드는 `MediaResource` 인스턴스:

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
   >이 작업 후 언제든지 을 사용할 수 있습니다 `MediaResource` 접근자(getter)를 사용하여 리소스의 유형, URL 및 메타데이터를 검사합니다.

1. MediaPlayer 인스턴스를 로드합니다. 자세한 내용은 [MediaPlayer에서 미디어 리소스 로드](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
