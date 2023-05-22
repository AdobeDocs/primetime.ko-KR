---
description: 이 Multi-DRM 워크플로우는 Widevine 및 PlayReady로 암호화된 DASH 콘텐츠의 설정, 패키징, 라이센싱 및 재생을 안내합니다.
title: Widevine 및 PlayReady용 다중 DRM 워크플로
exl-id: 97adfa69-52ef-470b-903a-eff1f075b7be
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Widevine 및 PlayReady용 다중 DRM 워크플로 {#multi-drm-workflow-for-widevine-and-playready}

이 Multi-DRM 워크플로우는 Widevine 및 PlayReady로 암호화된 DASH 콘텐츠의 설정, 패키징, 라이센싱 및 재생을 안내합니다.

Primetime TVSDK는 TVSDK 버전 2.X에서만 Android와 HTML 5에서 Widevine 암호화 또는 PlayReady 암호화 DASH 콘텐츠 재생을 지원합니다. DASH 콘텐츠 암호화는 일반 암호화 사양에 따라 정의되며, 전체 세부 정보는 이 문서의 범위를 벗어납니다. 이 섹션에서는 DASH 형식 및 암호화 사양에 대한 관련 세부 정보와 지원되는 콘텐츠를 생성하는 데 사용할 수 있는 도구에 대한 정보를 제공합니다.

>[!NOTE]
>
>Android TVSDK 1.X에 Widevine 암호화 DASH 콘텐츠 재생을 백포트하는 계획은 없습니다.

## DASH 콘텐츠 및 공통 암호화 개요 {#section_33A881158F724835B4B89AAE97302B17}

대시 콘텐츠는 비디오 및 오디오 파일을 재생하도록 지정하는 xml로 작성된 기본 매니페스트로 구성됩니다. 아래 예에서 DASH 매니페스트는 매니페스트의 URL에 상대적인 비디오 URL, video/1080_30.mp4 및 오디오 URL, audio/1080_30.mp4를 가리킵니다.

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

다음은 일반 암호화가 적용된 예제 매니페스트입니다. Widevine 콘텐츠 보호 XML 요소( `<ContentProtection>` manifest에 base64 인코딩 pssh(Protection System Specific Header) 상자가 있습니다. pssh 상자에는 콘텐츠 암호 해독을 초기화하는 데 필요한 데이터가 포함되어 있습니다. 이 데이터는 매니페스트가 참조하는 비디오/오디오 콘텐츠에도 포함됩니다. DASH 컨텐츠는 복수의 컨텐츠 보호 요소를 가질 수 있다, 예를 들어, PlayReady에 대한 1 및 Widevine에 대한 1.

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

위의 첫 번째 예는 각 스트림에 대해서만 하나의 파일을 참조하고, 두 번째 예는 일련의 작은 콘텐츠 조각을 참조합니다. 조각을 명시적으로 참조하는 대신 다음과 같은 조각 템플릿을 정의할 수도 있습니다.

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

이 경우 콘텐츠 파서(TVSDK)는 Jigo0.m4s, Jigo1.m4s, Jigo2.m4s 등에서 비디오 콘텐츠를 찾을 수 있습니다. 이 기능은 주로 라이브 스트리밍에 사용되며 클라이언트가 매니페스트를 때때로 다시 다운로드할 필요가 없다는 장점이 있습니다.
