---
description: 비디오용 재생 목록은 기본 비디오 콘텐츠에 대한 대체 오디오 트랙을 무제한으로 지정할 수 있습니다. 예를 들어, 비디오 콘텐츠에 다른 언어를 추가하거나 콘텐츠가 재생되는 동안 사용자가 장치의 다른 트랙 간을 전환하도록 허용할 수 있습니다.
title: 재생 목록의 대체 오디오 트랙
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 재생 목록의 대체 오디오 트랙 {#alternate-audio-tracks-in-the-playlist}

비디오용 재생 목록은 기본 비디오 콘텐츠에 대한 대체 오디오 트랙을 무제한으로 지정할 수 있습니다. 예를 들어, 비디오 콘텐츠에 다른 언어를 추가하거나 콘텐츠가 재생되는 동안 사용자가 장치의 다른 트랙 간을 전환하도록 허용할 수 있습니다.

대체 오디오 트랙을 사용하면 HTTP 비디오 스트림(실시간/선형 및 VOD)에 대한 여러 언어 트랙 간을 전환할 수 있으며, 각 오디오 트랙에 대해 비디오를 수정, 복제 또는 다시 패키징할 필요가 없습니다. 에셋의 초기 패키징 전이나 후에 비디오 에셋에 여러 언어 트랙을 제공할 수 있습니다.

>[!IMPORTANT]
>
>대체 오디오를 기본 미디어의 비디오 트랙과 혼합하려면 대체 트랙의 타임스탬프가 기본 트랙의 오디오 타임스탬프와 일치해야 합니다.

기본 오디오 트랙은 오디오 트랙 컬렉션에 포함되어 있습니다. `default` 레이블. 대체 오디오 스트림에 대한 메타데이터는 의 재생 목록에 포함됩니다. `#EXT-X-MEDIA` 태그 포함 `TYPE=AUDIO`.

예를 들어, 여러 대체 오디오 스트림을 지정하는 M3U8 매니페스트는 다음과 같을 수 있습니다.

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
