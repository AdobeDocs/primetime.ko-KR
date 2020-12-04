---
description: 대체 또는 지연 바인딩 오디오를 사용하면 비디오 트랙에 사용할 수 있는 오디오 트랙 간을 전환할 수 있습니다. 이렇게 하면 비디오가 재생될 때 언어 트랙을 선택할 수 있습니다.
seo-description: 대체 또는 지연 바인딩 오디오를 사용하면 비디오 트랙에 사용할 수 있는 오디오 트랙 간을 전환할 수 있습니다. 이렇게 하면 비디오가 재생될 때 언어 트랙을 선택할 수 있습니다.
seo-title: 재생 목록의 대체 오디오 트랙
title: 재생 목록의 대체 오디오 트랙
uuid: 6241d3e4-6e07-44fb-bc0e-5d49d1a76824
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# 재생 목록 {#section_BC8C1C74A5A24A8CA68C1E7E721EE742}의 대체 오디오 트랙

비디오용 재생 목록은 기본 비디오 컨텐츠에 대한 대체 오디오 트랙을 무제한으로 지정할 수 있습니다. 예를 들어 비디오 컨텐츠에 다른 언어를 추가하거나 사용자가 컨텐츠를 재생하는 동안 장치의 다른 트랙 간을 전환할 수 있도록 허용할 수 있습니다.

대체 오디오 트랙 또는 지연 바인딩 오디오를 사용하면 HTTP 비디오 스트림(라이브/리니어 및 VOD)에 대한 여러 언어 트랙 간을 전환할 수 있으며 각 오디오 트랙에 대해 비디오를 수정, 복제 또는 재패키지할 필요가 없습니다. 에셋의 초기 패키징 전 또는 후에 비디오 에셋에 대해 여러 언어 트랙을 제공할 수 있습니다.

>[!TIP]
>
>대체 오디오를 기본 미디어의 비디오 트랙과 혼합하려면 대체 트랙의 타임스탬프가 기본 트랙의 오디오 타임스탬프와 일치해야 합니다.

대체 오디오 트랙을 사용하고 광고를 통합하는 경우 다음 요구 사항이 적용됩니다.

* 기본 컨텐츠에 대체 오디오 트랙이 있는 경우 광고에 하나 이상의 오디오 전용 스트림이 있어야 합니다.
* 광고 오디오 전용 스트림의 각 세그먼트 지속 시간은 광고 비디오 스트림의 세그먼트 지속 시간과 같아야 합니다.

기본 오디오 트랙은 `default` 레이블이 있는 오디오 트랙 컬렉션에 포함됩니다. 대체 오디오 스트림의 메타데이터는 `TYPE=AUDIO`이 있는 `#EXT-X-MEDIA` 태그의 재생 목록에 포함됩니다.

예를 들어, 여러 개의 대체 오디오 스트림을 지정하는 M3U8 매니페스트는 다음과 같이 표시될 수 있습니다.

```
#EXTM3U 
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 1", 
 AUTOSELECT=YES,DEFAULT=YES 
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 2", 
 AUTOSELECT=NO,DEFAULT=NO,URI="alternate_audio_aac/prog_index.m3u8" 
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,FORCED=NO, 
 LANGUAGE="eng",URI="subtitles/eng/prog_index.m3u8" 
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English (Forced)",DEFAULT=YES, 
 AUTOSELECT=YES,FORCED=YES,LANGUAGE="eng",URI="subtitles/eng_forced/prog_index.m3u8" 
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="Français",AUTOSELECT=YES,FORCED=NO, 
 LANGUAGE="fra",URI="subtitles/fra/prog_index.m3u8" 
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=263851,CODECS="mp4a.40.2, avc1.4d400d", 
 RESOLUTION=416x234,AUDIO="bipbop_audio",SUBTITLES="subs"  
gear1/prog_index.m3u8 
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=577610,CODECS="mp4a.40.2, avc1.4d401e", 
 RESOLUTION=640x360,AUDIO="bipbop_audio",SUBTITLES="subs" 
gear2/prog_index.m3u8 
... 
```
