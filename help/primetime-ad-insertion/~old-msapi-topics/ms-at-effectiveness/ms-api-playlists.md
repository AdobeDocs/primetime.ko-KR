---
description: 매니페스트 서버는 제안된 HTTP 라이브 스트리밍 표준에 따라 M3U8 형식의 마스터 플레이리스트를 반환합니다. 변형 전송 스트림(TS) 세트로 구성되며, 각각은 서로 다른 비트율 및 형식에 대해 동일한 컨텐츠의 렌디션을 포함합니다. Adobe Primetime ad insertion은 클라이언트 비디오 플레이어에서 해석할 EXT-X-MARKER 지시문 태그를 추가합니다.
title: EXT-X-MARKER 지시문
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# EXT-X-MARKER 지시문 {#ext-x-marker-directive}

매니페스트 서버는 제안된 HTTP 라이브 스트리밍 표준에 따라 M3U8 형식의 마스터 플레이리스트를 반환합니다. 변형 전송 스트림(TS) 세트로 구성되며, 각각은 서로 다른 비트율 및 형식에 대해 동일한 컨텐츠의 렌디션을 포함합니다. Adobe Primetime ad insertion은 클라이언트 비디오 플레이어에서 해석할 EXT-X-MARKER 지시문 태그를 추가합니다.

EXT-X-MARKER 태그에 대한 자세한 내용은 [Adobe Primetime HTTP 라이브 스트리밍 프로필](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>이 기능은 부트스트랩 매니페스트 서버 URL에 `pttrackingmode` 매개 변수.

>[!NOTE]
>
>EXT-X-MARKER 태그는 콘텐츠 세그먼트가 아닌 광고 세그먼트에 추가됩니다.

다음의 초안 표준 [HTTP 라이브 스트리밍](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) 변형 재생 목록의 콘텐츠 및 형식을 설명합니다. EXT-X-MARKER 태그는 클라이언트가 콜백을 호출하도록 지시합니다. 여기에는 다음 구성 요소가 포함됩니다.

* **ID** 프로그램 스트림 컨텍스트 내에서 이 콜백 이벤트에 대한 고유 식별자(문자열).

* **유형** 콜백 이벤트 유형(문자열): PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd 또는 AdBegin

* **기간** 지시문이 유효한 태그를 포함하는 세그먼트 시작까지의 시간(초)입니다.

* **오프셋** 선택 사항입니다. 콜백을 호출해야 하는 경우 세그먼트 재생 시작에 상대적인 오프셋(초)입니다.

   * `PodBegin` 및 `PrerollPodBegin` data 속성에 비콘 정보를 포함하고 세그먼트 시작 시 실행됩니다. 그래서 `OFFSET` 태그는 여기에서 사용할 수 없습니다.

   * `AdBegin` data 속성에 비콘 정보가 포함되어 있으며 노출 태그는 해당 세그먼트의 시작 시 실행됩니다. 그래서 `OFFSET` 태그도 여기에서 사용할 수 없습니다.

   * `PodEnd` 및 `PrerollPodEnd` data 속성에는 비콘 정보가 포함되지만 이러한 태그는 pod에서 마지막 광고의 마지막 세그먼트 끝에서 실행될 것으로 예상되므로 현재 세그먼트 끝에서 실행됩니다. 이 경우, `OFFSET` 이(가) (으)로 설정됨 `<duration of segment>` 비콘이 현재 세그먼트의 끝에서 실행되도록 지정합니다.

* **데이터** 콜백을 호출할 때 응용 프로그램에 전달할 데이터를 포함하는 큰따옴표로 묶인 Base64 인코딩 문자열입니다. 여기에는 VMAP1.0 및 VAST3.0 사양을 준수하는 광고 추적 정보가 포함되어 있습니다.

* **수** 광고 브레이크에서 결합되는 광고 수입니다.

   TYPE 구성 요소가 PodBegin 또는 PrerollPodBegin으로 설정된 경우에만 적용됩니다.

* **분류기** 채워진 광고 브레이크의 총 기간(초)입니다.

   TYPE 구성 요소가 PodBegin 또는 PrerollPodBegin으로 설정된 경우에만 적용됩니다.

콜백을 구성할 때 EXT-X-MARKER 구성 요소를 다음과 같이 해석합니다.

* 태그에 다음 항목이 포함된 경우 `OFFSET`, 해당 세그먼트의 컨텐츠 재생 시작을 기준으로 지정된 오프셋에서 콜백을 실행합니다. 그렇지 않으면 해당 세그먼트의 컨텐츠가 재생을 시작하자마자 콜백을 실행합니다.
* 사용 `DURATION` 광고 콘텐츠의 진행률을 추적하고 이벤트 추적을 위해 URL을 요청합니다.
* 합격 `ID`, `TYPE`, 및 `DATA` 콜백에 연결합니다.

사용 `PrerollPodBegin`, 및 `PrerollPodEnd` 값 `TYPE` 라이브/선형 스트림에서 먼저 재생할 TS 세그먼트를 결정합니다.

>[!NOTE]
>
>다음 `PrerollPodBegin`, 및 `PrerollPodEnd` 값은 프리롤 광고가 라이브 스트림에 삽입되는 경우에만 사용할 수 있습니다.

매니페스트 서버에는 다음 세그먼트에 EXT-X-MARKER 태그가 포함되어 있습니다.

* 광고 Pod의 시작을 추적하는 광고 브레이크의 첫 번째 세그먼트입니다.
* 광고의 첫 번째 세그먼트로, 광고 pod 내의 개별 광고의 시작/완료/진행률을 추적합니다.
* 광고 Pod의 끝을 추적할 광고 브레이크의 마지막 세그먼트입니다.

매니페스트 서버가 `VMAP1.0-conformant` 각 광고 브레이크의 시작과 끝을 추적하는 XML 문서입니다. 광고 서버에서 반환된 실제 VMAP1.0 응답의 필터링된 버전이며, 주로 다음과 같은 추적 이벤트가 포함됩니다.

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

매니페스트 서버가 프로그램 콘텐츠에 삽입하는 각 광고 크리에이티브에 대해 VAST3.0 호환 XML 문서를 전송하여 해당 광고를 추적합니다. 각 XML 문서에는 `<InLine>` 삽입된 선형 광고 문안을 설명하는 요소 또는 `<Wrapper>` 래퍼 광고(즉, 연결되거나 리디렉션된 광고)와 연결된 컴패니언 광고 및 확장의 경우 요소입니다. 광고가 광고 pod의 일부인 경우와 같이 VAST 응답에 시퀀스 속성이 포함된 경우 문서에는 해당 속성이 포함됩니다. 다음은 개별 광고 추적을 위한 샘플 VAST3.0 호환 XML 문서입니다.

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
