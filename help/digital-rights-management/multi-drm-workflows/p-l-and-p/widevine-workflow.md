---
description: 이 멀티 DRM 워크플로우에서는 Widine 및 PlayReady를 사용하여 암호화된 DASH 컨텐츠의 설정, 패키징, 라이선스 및 재생을 수행할 수 있습니다.
title: Widevine 및 PlayReady를 위한 멀티 DRM 워크플로우
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Widevine 및 PlayReady {#multi-drm-workflow-for-widevine-and-playready}에 대한 다중 DRM 작업 과정

이 멀티 DRM 워크플로우에서는 Widine 및 PlayReady를 사용하여 암호화된 DASH 컨텐츠의 설정, 패키징, 라이선스 및 재생을 수행할 수 있습니다.

Primetime TVSDK는 TVSDK 버전 2.X에서만 HTML5 및 Android에서 Widevine으로 암호화된 또는 PlayReady로 암호화된 DASH 컨텐츠를 재생할 수 있습니다.DASH 컨텐츠 암호화는 일반 암호화 사양에 의해 정의되며, 전체 세부 사항은 이 문서의 범위를 벗어납니다. 이 섹션에서는 DASH 형식 및 암호화 사양의 관련 세부 정보와 지원되는 컨텐츠를 생성하는 데 사용할 수 있는 일부 도구에 대한 정보를 제공합니다.

>[!NOTE]
>
>Android TVSDK 1.X로 Widevine으로 암호화된 DASH 컨텐츠를 재생할 계획이 없습니다.

## 대시 내용 및 공통 암호화 개요 {#section_33A881158F724835B4B89AAE97302B17}

대시 컨텐츠는 xml로 작성된 기본 매니페스트로 이루어져 재생되는 비디오 및 오디오 파일을 가리킵니다. 아래 예에서 DASH 매니페스트는 매니페스트 URL에 상대적인 비디오 URL, video/1080_30.mp4 및 오디오 URL audio/1080_30.mp4를 가리킵니다.

```
<MPD xmlns="urn:mpeg:DASH:schema:MPD:2011" xmlns:cenc="urn:mpeg:cenc:2013" xmlns:scte35="urn:scte:scte35:2013" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"mediaPresentationDuration="PT30S" minBufferTime="PT8S" profiles="urn:mpeg:dash:profile:isoff-on-demand:2011" type="static" xsi:schemaLocation="urn:mpeg:DASH:schema:MPD:2011 DASH-MPD.xsd">
    <Period id="1" start="PT0S">
        <AdaptationSet bitstreamSwitching="true" contentType="video" id="1" segmentAlignment="true" startWithSAP="2">
            <Representation bandwidth="4215100" codecs="avc1.4d4029" height="1080" id="1" mimeType="video/mp4" width="1920">
                <BaseURL>video/1080_30.mp4</BaseURL>
                <CueInfo schemeIdUri="urn:adobe:mpeg:dash:cueinfo:2012"/>
            </Representation>
        </AdaptationSet>
 
        <AdaptationSet bitstreamSwitching="true" contentType="audio" id="2" segmentAlignment="1" startWithSAP="1">
            <Representation bandwidth="320600" codecs="mp4a.40.02" id="1" mimeType="audio/mp4">
                <BaseURL>audio/1080_30.mp4</BaseURL>
                <CueInfo schemeIdUri="urn:adobe:mpeg:dash:cueinfo:2012"/>
            </Representation>
        </AdaptationSet>
    </Period>
</MPD>
```

다음은 공통 암호화를 적용한 매니페스트 예입니다. 매니페스트의 Widevine 내용 보호 XML 요소(`<ContentProtection>` 블록)에는 base64 인코딩된 pssh(Protection System 특정 헤더) 상자가 포함되어 있습니다. pssh 상자에는 컨텐츠 암호 해독을 초기화하는 데 필요한 데이터가 포함되어 있습니다. 이 데이터는 매니페스트가 참조하는 비디오/오디오 컨텐츠에도 포함됩니다. DASH 컨텐츠에는 PlayReady 1과 Widevine 1과 같이 여러 컨텐츠 보호 요소가 있을 수 있습니다.

```
<?xml version="1.0" ?>
<MPD mediaPresentationDuration="PT3M35.533S" minBufferTime="PT15.00S" profiles="urn:mpeg:dash:profile:isoff-live:2011" type="static" xmlns="urn:mpeg:dash:schema:mpd:2011" xmlns:cenc="urn:mpeg:cenc:2013">
  <!-- Created with Bento4 mp4-dash.py, VERSION=1.6.0-607 -->
  <Period>
    <!-- Audio -->
    <AdaptationSet mimeType="audio/mp4" segmentAlignment="true" startWithSAP="1">
      <!-- Common Encryption -->
      <ContentProtection cenc:default_KID="9e828b37-842d-9f71-0233-c007fb1d4f5b" schemeIdUri="urn:mpeg:dash:mp4protection:2011" value="cenc"/>
      <!-- Widevine -->
      <ContentProtection schemeIdUri="urn:uuid:edef8ba9-79d6-4ace-a3c8-27dcd51d21ed">
        <cenc:pssh>
        AAAAQ3Bzc2gAAAAA7e+LqXnWSs6jyCfc1R0h7QAAACMIARIQnoKLN4Qtn3ECM8AH+x1PWxoKaW50ZXJ0cnVzdCIBKg==
        </cenc:pssh>
      </ContentProtection>
      <Representation audioSamplingRate="44100" bandwidth="200429" codecs="mp4a.40.2" id="audio/und">
        <AudioChannelConfiguration schemeIdUri="urn:mpeg:dash:23003:3:audio_channel_configuration:2011" value="2"/>
        <SegmentList duration="15000" timescale="1000">
          <Initialization sourceURL="audio/und/init.mp4"/>
          <SegmentURL media="audio/und/seg-1.m4f"/>
          <SegmentURL media="audio/und/seg-2.m4f"/>
          <SegmentURL media="audio/und/seg-3.m4f"/>
          <SegmentURL media="audio/und/seg-4.m4f"/>
          <SegmentURL media="audio/und/seg-5.m4f"/>
          <SegmentURL media="audio/und/seg-6.m4f"/>
          <SegmentURL media="audio/und/seg-7.m4f"/>
          <SegmentURL media="audio/und/seg-8.m4f"/>
          <SegmentURL media="audio/und/seg-9.m4f"/>
          <SegmentURL media="audio/und/seg-10.m4f"/>
          <SegmentURL media="audio/und/seg-11.m4f"/>
          <SegmentURL media="audio/und/seg-12.m4f"/>
          <SegmentURL media="audio/und/seg-13.m4f"/>
          <SegmentURL media="audio/und/seg-14.m4f"/>
          <SegmentURL media="audio/und/seg-15.m4f"/>
          <SegmentURL media="audio/und/seg-16.m4f"/>
        </SegmentList>
      </Representation>
    </AdaptationSet>
 
    <!-- Video -->
    <AdaptationSet maxHeight="720" maxWidth="1280" mimeType="video/mp4" minHeight="720" minWidth="1280" segmentAlignment="true" startWithSAP="1">
      <!-- Common Encryption -->
      <ContentProtection cenc:default_KID="9e828b37-842d-9f71-0233-c007fb1d4f5b" schemeIdUri="urn:mpeg:dash:mp4protection:2011" value="cenc"/>
      <!-- Widevine -->
      <ContentProtection schemeIdUri="urn:uuid:edef8ba9-79d6-4ace-a3c8-27dcd51d21ed">
        <cenc:pssh>
        AAAAQ3Bzc2gAAAAA7e+LqXnWSs6jyCfc1R0h7QAAACMIARIQnoKLN4Qtn3ECM8AH+x1PWxoKaW50ZXJ0cnVzdCIBKg==
        </cenc:pssh>
      </ContentProtection>
 
      <Representation bandwidth="2640920" codecs="avc1.64001F" frameRate="30" height="720" id="video/1" scanType="progressive" width="1280">
        <SegmentList duration="15000" timescale="1000">
          <Initialization sourceURL="video/1/init.mp4"/>
          <SegmentURL media="video/1/seg-1.m4f"/>
          <SegmentURL media="video/1/seg-2.m4f"/>
          <SegmentURL media="video/1/seg-3.m4f"/>
          <SegmentURL media="video/1/seg-4.m4f"/>
          <SegmentURL media="video/1/seg-5.m4f"/>
          <SegmentURL media="video/1/seg-6.m4f"/>
          <SegmentURL media="video/1/seg-7.m4f"/>
          <SegmentURL media="video/1/seg-8.m4f"/>
          <SegmentURL media="video/1/seg-9.m4f"/>
          <SegmentURL media="video/1/seg-10.m4f"/>
          <SegmentURL media="video/1/seg-11.m4f"/>
          <SegmentURL media="video/1/seg-12.m4f"/>
          <SegmentURL media="video/1/seg-13.m4f"/>
          <SegmentURL media="video/1/seg-14.m4f"/>
          <SegmentURL media="video/1/seg-15.m4f"/>
        </SegmentList>
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```

위의 첫 번째 예는 각 스트림에 대해서만 하나의 파일을 참조하지만 두 번째 예제는 일련의 작은 컨텐츠 조각을 나타냅니다. 조각을 명시적으로 참조하는 대신 조각 템플릿을 정의할 수도 있습니다. 예:

```
<Representation bandwidth="348000" codecs="avc1.42c01e" height="360" id="1" width="640">
    <BaseURL>video/</BaseURL>
    <SegmentTemplate initialization="JaigoInit.mp4" media="Jaigo$Number$.m4s" startNumber="0" timescale="1000">
        <SegmentTimeline>
            <S d="4538" t="0"/>
            <S d="4304" t="4538"/>
            <S d="4004" t="8842"/>
            <S d="2102" t="12846"/>
        </SegmentTimeline>
    </SegmentTemplate>
</Representation>
```

이 경우 컨텐츠 파서(TVSDK)는 Jaigo0.m4s, Jaigo1.m4s, Jaigo2.m4s 등에서 비디오 컨텐츠를 찾을 것으로 예상합니다. 이것은 주로 실시간 스트리밍에 사용되며 때때로 클라이언트에서 매니페스트를 다시 다운로드하지 않아도 된다는 이점이 있습니다.
