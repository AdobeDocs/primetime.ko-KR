---
description: 매니페스트 서버는 제안된 HTTP 라이브 스트리밍 표준을 준수하며 M3U8 형식의 마스터 재생 목록을 반환합니다. 이것은 서로 다른 비트 전송률 및 형식에 대해 동일한 컨텐츠의 변환을 포함하는 다양한 TS(Variant Transport Streams) 세트로 구성됩니다. Adobe Primetime 광고 삽입은 클라이언트 비디오 플레이어에서 해석할 수 있도록 EXT-X-MARKER 지시문 태그를 추가합니다.
title: EXT-X-MARKER 지시문
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# EXT-X-MARKER 지시문 {#ext-x-marker-directive}

매니페스트 서버는 제안된 HTTP 라이브 스트리밍 표준을 준수하며 M3U8 형식의 마스터 재생 목록을 반환합니다. 이것은 서로 다른 비트 전송률 및 형식에 대해 동일한 컨텐츠의 변환을 포함하는 다양한 TS(Variant Transport Streams) 세트로 구성됩니다. Adobe Primetime 광고 삽입은 클라이언트 비디오 플레이어에서 해석할 수 있도록 EXT-X-MARKER 지시문 태그를 추가합니다.

EXT-X-MARKER 태그에 대한 자세한 내용은 [Adobe Primetime HTTP 라이브 스트리밍 프로필](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf)을 참조하십시오.

>[!NOTE]
>
>이 기능은 부트스트랩 매니페스트 서버 URL에 `pttrackingmode` 매개 변수가 없는 경우에만 사용할 수 있습니다.

>[!NOTE]
>
>EXT-X-MARKER 태그는 컨텐츠 세그먼트가 아니라 광고 세그먼트에 추가됩니다.

[HTTP 라이브 스트리밍](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23)의 초안 표준은 변형 재생 목록의 내용과 형식을 설명합니다. EXT-X-MARKER 태그는 클라이언트가 콜백을 호출하도록 지시합니다. 여기에는 다음 구성 요소가 포함됩니다.

* **프로그램** 스트림의 컨텍스트 내에서 이 콜백 이벤트에 대한 IDUnique 식별자(문자열)입니다.

* **콜백** 이벤트의 TYPEype(문자열):PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd 또는 AdBegin

* **지시어가 유효한 태그로** 지정된 세그먼트 시작(초)부터 시간의 길이(초)입니다.

* **** 선택 사항. 콜백을 호출해야 하는 경우 세그먼트 재생 시작을 기준으로 하는 오프셋(초)입니다.

   * `PodBegin` 를  `PrerollPodBegin` 사용하여 DATA 속성에 비콘 정보를 포함하고 세그먼트 시작 시 실행됩니다. 따라서 `OFFSET` 태그는 여기에서 사용할 수 없습니다.

   * `AdBegin` 에 DATA 속성에 비콘 정보가 들어 있으며 해당 세그먼트 시작 시 노출 태그가 실행됩니다. 따라서 `OFFSET` 태그도 여기에서 사용할 수 없습니다.

   * `PodEnd` 및 `PrerollPodEnd` 는 DATA 속성에 비콘 정보를 포함하지만 이 태그는 창에서 마지막 광고의 마지막 세그먼트 끝에 실행되어야 하므로 현재 세그먼트의 끝에 실행됩니다. 이 경우, `OFFSET`은(는) `<duration of segment>`로 설정되어 비콘이 현재 세그먼트의 끝에서 시작되도록 지정합니다.

* **콜백** 을 호출할 때 응용 프로그램에 전달할 데이터를 포함하는 큰 따옴표로 묶은 DATABase64 인코딩 문자열입니다. 여기에는 VMAP1.0 및 VAST3.0 사양을 준수하는 광고 추적 정보가 포함되어 있습니다.

* **광고** 중단에 포함할 광고의 수입니다.

   TYPE 구성 요소가 PodBegin 또는 PrerollPodBegin으로 설정된 경우에만 해당됩니다.

* **** 채워진 광고 분리의 총 지속 시간(초)입니다.

   TYPE 구성 요소가 PodBegin 또는 PrerollPodBegin으로 설정된 경우에만 해당됩니다.

콜백을 구성할 때 EXT-X-MARKER 구성 요소를 다음과 같이 해석하십시오.

* 태그에 `OFFSET`이 포함되어 있으면 해당 세그먼트에서 컨텐츠 재생의 시작을 기준으로 지정된 오프셋에서 콜백을 시작합니다. 그렇지 않은 경우 해당 세그먼트의 콘텐츠가 재생을 시작하는 즉시 콜백을 시작합니다.
* 광고 컨텐츠의 진행 상태를 추적하고 이벤트를 추적하기 위해 URL을 요청하려면 `DURATION`을 사용합니다.
* 콜백에 `ID`, `TYPE` 및 `DATA`를 전달합니다.

라이브/선형 스트림에서 먼저 재생할 TS 세그먼트를 결정하려면 `PrerollPodBegin` 및 `PrerollPodEnd` 값을 사용합니다.`TYPE`

>[!NOTE]
>
>`PrerollPodBegin` 및 `PrerollPodEnd` 값은 프리롤 광고가 라이브 스트림에 삽입되는 경우에만 사용할 수 있습니다.

매니페스트 서버에는 다음 세그먼트에 EXT-X-MARKER 태그가 포함됩니다.

* 광고 분할의 첫 번째 세그먼트로, 광고 창의 시작을 추적합니다.
* 광고 창의 첫 번째 세그먼트로, 광고 창 내의 개별 광고의 시작/완료/진행 상태를 추적합니다.
* 광고 분할의 마지막 세그먼트로, 광고 창의 끝을 추적합니다.

매니페스트 서버는 각 광고 분리의 시작과 끝을 추적하기 위해 `VMAP1.0-conformant` XML 문서를 보냅니다. 광고 서버에서 반환된 실제 VMAP1.0 응답의 필터링된 버전이며, 주로 여기에 표시된 추적 이벤트를 포함합니다.

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<vmap:VMAP xmlns:vmap="https://www.iab.net/vmap-1.0" version="1.0"> 
    <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start"> 
        <vmap:TrackingEvents> 
            <vmap:Tracking event="breakStart"> 
                https://MyServer.com/breakstart.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="breakEnd"> 
                https://MyServer.com/breakend.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="error"> 
                https://MyServer.com/error.gif 
            </vmap:Tracking> 
        </vmap:TrackingEvents> 
    </vmap:AdBreak> 
</vmap:VMAP> 
</AdTrackingFragment> 
</AdTrackingFragments>
```

매니페스트 서버가 프로그램 콘텐츠에 삽입하는 각 광고의 경우 해당 광고를 추적하기 위해 VAST3.0 준수 XML 문서를 전송합니다. 각 XML 문서에는 삽입된 선형 광고 크리에이티브를 설명하는 `<InLine>` 요소 또는 래퍼 광고(즉, 링크되거나 리디렉션된 광고)의 경우 `<Wrapper>` 요소 및 관련 부록 광고 및 확장이 포함됩니다. VAST 응답에 광고 창의 일부인 경우와 같이 시퀀스 속성이 포함된 경우 문서에 해당 속성이 포함됩니다. 다음은 개별 광고를 추적하기 위한 샘플 VAST3.0 준수 XML 문서입니다.

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<VAST xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"  
      version="3.0"  
      xsi:noNamespaceSchemaLocation="https://service.videoplaza.com/schema/iab/vast-3.0.xsd"> 
<Ad id="903395"> 
    <InLine> 
      <AdSystem version="1.0">Auditude</AdSystem> 
      <AdTitle/> 
      <Error>https://ad.qa.auditude.com/adserver/?ErrAd1=[ERRORCODE]</Error> 
      <Impression id="urn:aeid:903395">https://ad.qa.auditude.com/adserver/e?type=adimp&amp; 
                 cid=127860991&amp; 
                 z=50183&amp; 
                 a=903395&amp; 
                 s=ef8c51dc&amp; 
                 t=1355309735&amp; 
                 w=100000&amp; 
                 uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                 l=1355280906&amp; 
                 u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                 br=1&amp; 
                 sq=1&amp; 
                 pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                 ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                               ?Cashcash=[CACHEBUSTING] 
                               ?Asset=[ASSETURI] 
      </Impression> 
      <Creatives> 
        <Creative> 
          <Linear> 
            <Duration>00:00:15</Duration> 
            <TrackingEvents> 
              ... 
              <Tracking event="firstQuartile"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=25&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking>                
              <Tracking event="midpoint"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=50&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="firstQuartile"> 
                https://www.Tweeeen.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                       ?Cashcash=[CACHEBUSTING] 
                                       ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="midpoint"> 
                https://www.Fiftyyyy.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                        ?Cashcash=[CACHEBUSTING] 
                                        ?Asset=[ASSETURI] 
              </Tracking> 
              ... 
            </TrackingEvents> 
            <VideoClicks> 
              <ClickTracking> 
                https://www.MP4-Vid-ClickTrack.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                                  ?Cashcash=[CACHEBUSTING] 
                                                  ?Asset=[ASSETURI] 
              </ClickTracking> 
              <ClickThrough> 
                https://www.cnn.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                   ?Cashcash=[CACHEBUSTING] 
                                   ?Asset=[ASSETURI] 
              </ClickThrough> 
              ... 
            </VideoClicks> 
            <AdParameters>campaign_id=7012</AdParameters> 
            <MediaFiles> 
              ...            
            </MediaFiles> 
          </Linear> 
        </Creative> 
        <Creative> 
          <CompanionAds> 
            <Companion id="103" width="300" height="250"> 
              <StaticResource creativeType="image/jpeg"> 
                https://ad.qa.auditude.com/adserver/c/z=50183; 
                  l=1355280906; 
                  u=956c3cd141086a1da44dcae8ea4ed14a; 
                  uid=_CxLm0b1SeKD8KXco__5TQ; 
                  cid=127860991; 
                  s=ef8c51dc; 
                  t=1355309735; 
                  br=1; 
                  sq=1; 
                  pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur 
                    %3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8; 
                  ax=0%2c0%2c1720%2c0; 
                  w=100000; 
                  a=903395; 
                  a1=103/c300x250.jpeg 
              </StaticResource> 
              <CompanionClickThrough> 
                https://ad.qa.auditude.com/adserver/l/a=903395%3Ba1=103 
                  %3Ba2=1%3Bz=50183%3Bl=1355280906%3Bu=956c3cd141086a1da44dcae8ea4ed14a 
                  %3Bcid=127860991%3Bs=ef8c51dc%3Buid=_CxLm0b1SeKD8KXco__5TQ 
                  %3Bt=1355309735%3Bbr=1%3Bsq=1%3Bpod=id%3a1%2cctype%3al%2cptype 
                  %3ap%2cdur%3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8 
                  %3Bax=0%2c0%2c1720%2c0 
              </CompanionClickThrough> 
              <AdParameters>campaign_id=7012</AdParameters> 
            </Companion> 
          </CompanionAds> 
        </Creative> 
        ... 
      </Creatives> 
      <Extensions> 
        <Extension type="Behavior"> 
          ... 
        </Extension> 
      </Extensions> 
    </InLine> 
  </Ad> 
  </VAST> 
</AdTrackingFragment> 
</AdTrackingFragments> 
```
