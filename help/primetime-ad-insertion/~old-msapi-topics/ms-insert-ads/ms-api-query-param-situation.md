---
description: 기본 쿼리 매개 변수 외에 선택적 쿼리 매개 변수를 사용하면 매니페스트 서버가 다양한 클라이언트 및 상황에서 작업할 수 있습니다.
title: 클라이언트 및 상황별 선택적 쿼리 매개 변수
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# 클라이언트 및 상황별 선택적 쿼리 매개 변수 {#optional-query-parameters-by-client-and-situation}

기본 쿼리 매개 변수 외에 선택적 쿼리 매개 변수를 사용하면 매니페스트 서버가 다양한 클라이언트 및 상황에서 작업할 수 있습니다.

## Akamai Ad Scaler로 광고 삽입 {#section_120FEC75C34D4F4587B77D842166D68A}

Akamai CDN(콘텐츠 전송 네트워크)에서 Akamai Edge 서버는 클라이언트와 매니페스트 서버 간의 중개 역할을 합니다. Ad Scaler도 사용하는 경우 `ptassetid` 및 `live` 쿼리 매개 변수는 Akamai Edge에 필요한 정보를 제공합니다.

다음 `ptassetid` 매개 변수는 자산의 게시자 ID입니다. Akamai는 요청 URL의 일부로 제공하는 base64 인코딩 URL이 아닌 이 URL을 사용하여 광고 삽입을 위해 매니페스트 서버에 제공할 재생 목록을 식별합니다.

다음 `live` 매개 변수는 라이브 콘텐츠와 VOD(video on demand)를 구별합니다. 매니페스트 서버는 Akamai와의 간소화된 인터페이스를 지원하기 위해 이 정보가 필요합니다.

다음은 Akamai와 관련된 매개 변수를 보여주는 샘플 URL입니다.

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Xbox의 TVSDK에서 광고 삽입 {#section_5DB405F4647240A0B83E72DE35D5EC80}

Xbox에서 Primetime TVSDK를 기반으로 하는 플레이어는 기본 쿼리 매개 변수 외에 추가 쿼리 매개 변수를 제공할 필요가 없습니다.

## Safari를 사용하는 iOS의 TVSDK에서 광고 삽입 {#section_250E493A125E4F82940D19C7DA2AAB2E}

Safari 브라우저를 사용하여 iOS에서 Primetime TVSDK를 기반으로 하는 플레이어는 다음을 지정해야 합니다. `ptplayer` 및 `live` 기본 쿼리 매개 변수 이외의 매개 변수입니다.

매니페스트 서버는 `ptplayer` 값 `ios-mobileweb` 및 는 반환되는 광고 결합 매니페스트에서 프리롤을 제거합니다.

다음 `live` 매개 변수는 매니페스트 서버에 라이브 또는 VOD 콘텐츠를 반환할지 여부를 알려줍니다.

다음은 Safari가 있는 iOS과 관련된 매개 변수를 보여주는 샘플 URL입니다.

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## 사용자 지정 광고 큐 형식을 사용한 광고 삽입 {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe은 Primetime 패키지에서 직접 지원하지 않는 광고 큐 형식의 이름을 제공합니다. 이러한 형식을 사용하려면 Adobe이 제공한 이름을 값으로 지정하십시오. `ptcueformat` 매개 변수.

다음은 사용자 지정 광고 큐 형식을 지정하는 샘플 URL입니다.

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## 광고 큐를 사용하여 VOD에 대한 FreeWheel 타임라인을 만드는 광고 삽입 {#section_E0D830F5EEE24639819B975B90F6999F}

광고 큐를 포함하는 VOD 콘텐츠를 구문 분석하고 FreeWheel 광고 요청에 포함하려면 의 값을 설정합니다. `ptcueformat` 매개 변수 `DPIsimple`.

다음은 VOD에 FreeWheel 타임라인을 사용하여 지정하는 샘플 URL입니다.

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## VOD에 대한 사용자 지정 타임라인을 사용한 광고 삽입 {#section_F398F7659164463FA886A4CC787C7B5A}

매니페스트 서버에 제공한 타임라인에 따라 VOD 콘텐츠에 광고를 삽입하도록 요청하려면 의 값을 설정하십시오. `pttimeline` 타임라인을 지정하는 문자열에 대한 매개 변수입니다. 다음을 참조하십시오 [VOD 타임라인 형식](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

다음은 VOD에 사용자 지정 타임라인을 사용하는 샘플 URL입니다.

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

1분에는 최대 2개의 광고를, 그 뒤에는 2분의 콘텐츠 세그먼트를 포함하는 첫 번째 브레이크를 지정하고, 그 뒤에는 최대 2개의 광고를 포함하는 30초 브레이크와 5분의 콘텐츠 세그먼트를 지정합니다.

VOD 콘텐츠에 대한 사용자 지정 콘텐츠 타임라인에 대한 광고 결합은 다음과 같이 작동합니다.

* 광고는 광고 서버에서 지정한 광고 배치 시간 후에 가장 가까운 브레이크 경계에 나타납니다.

* 세그먼트는 최소 2초입니다.

## TS 세그먼트 인증 {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe은 Akamai CDN에 대해서만 이 기능을 지원합니다. HTTP 라이브 스트리밍(HLS)은 스트림 수준 M3U8 재생 목록을 사용하여 전송 스트림(TS) 세그먼트를 전달합니다. 변형 M3U8 재생 목록에서 여러 스트림 수준 재생 목록이 클라이언트에 제공됩니다. 클라이언트는 변형 목록에서 재생 목록 스트림을 하나씩 선택한 다음 해당 스트림 수준 재생 목록의 TS 세그먼트를 하나씩 다운로드합니다. 정상적인 작동에서 요청된 콘텐츠는 쿠키 승인이 필요할 수 있으며, 매니페스트 서버는 백그라운드에서 보이지 않게 처리합니다. 원시 콘텐츠에서 쿠키를 추출하고 선택한 재생 목록 스트림을 요청하는 데 사용할 URL에 적절한 토큰을 추가합니다.

Bootstrap URL 쿼리 매개 변수에 다음이 포함되는 경우 `pttoken=true`, 게시자는 전체 스트림에 대해 한 번만 사용하는 것이 아니라 각 TS 세그먼트를 요청할 때 쿠키를 사용해야 합니다. 매니페스트 서버는 이 쿠키를 쿼리 매개 변수로 스트림 재생 목록의 각 TS 세그먼트 URL에 다시 연결합니다.
