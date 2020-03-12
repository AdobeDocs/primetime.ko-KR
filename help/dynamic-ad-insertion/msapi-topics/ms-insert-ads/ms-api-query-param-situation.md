---
description: 기본 쿼리 매개 변수 외에도 선택적 쿼리 매개 변수를 사용하면 매니페스트 서버가 다른 클라이언트와 상황에서 작동할 수 있습니다.
seo-description: 기본 쿼리 매개 변수 외에도 선택적 쿼리 매개 변수를 사용하면 매니페스트 서버가 다른 클라이언트와 상황에서 작동할 수 있습니다.
seo-title: 클라이언트 및 상황별 선택적 쿼리 매개 변수
title: 클라이언트 및 상황별 선택적 쿼리 매개 변수
uuid: e3fae41e-9f7d-4f01-9a01-52a1d5f5dad5
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 클라이언트 및 상황별 선택적 쿼리 매개 변수 {#optional-query-parameters-by-client-and-situation}

기본 쿼리 매개 변수 외에도 선택적 쿼리 매개 변수를 사용하면 매니페스트 서버가 다른 클라이언트와 상황에서 작동할 수 있습니다.

## Akamai Ad Scaler를 사용한 광고 삽입 {#section_120FEC75C34D4F4587B77D842166D68A}

Akamai 컨텐츠 전달 네트워크(CDN)에서 Akamai Edge Server는 클라이언트와 매니페스트 서버 간의 중간 역할을 합니다. 또한 광고 스케일을 사용하는 경우 `ptassetid` 및 `live` 쿼리 매개 변수는 Akamai Edge에 필요한 정보를 제공합니다.

매개 `ptassetid` 변수는 해당 자산의 게시자 ID입니다. Akamai는 요청 URL의 일부로 제공하는 base64 인코딩 URL이 아닌 이것을 사용하여 광고 삽입을 위해 매니페스트 서버에 제공할 재생 목록을 식별합니다.

이 `live` 매개 변수는 라이브 컨텐츠와 VOD(Video On Demand)를 구분합니다. 매니페스트 서버는 Akamai와의 간소화된 인터페이스를 지원하기 위해 이 정보가 필요합니다.

다음은 Akamai와 관련된 매개 변수를 보여주는 샘플 URL입니다.

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Xbox에서 TVSDK를 통한 광고 삽입 {#section_5DB405F4647240A0B83E72DE35D5EC80}

Xbox에서 Primetime TVSDK를 기반으로 하는 플레이어는 기본 쿼리 매개 변수 외에 추가 쿼리 매개 변수를 제공하지 않아도 됩니다.

## iOS에서 Safari를 사용하여 TVSDK에서 광고 삽입 {#section_250E493A125E4F82940D19C7DA2AAB2E}

Safari 브라우저를 사용하는 iOS의 Primetime TVSDK 기반의 플레이어는 기본 쿼리 매개 변수 외에 `ptplayer` 및 `live` 매개 변수를 지정해야 합니다.

매니페스트 서버는 `ptplayer` 값을 인식하여 반환된 `ios-mobileweb` 광고 스티칭된 매니페스트에서 프리롤을 제거합니다.

이 `live` 매개 변수는 매니페스트 서버에 실시간 또는 VOD 콘텐츠를 반환할지 여부를 알려줍니다.

다음은 Safari와 함께 iOS와 관련된 매개 변수를 보여주는 샘플 URL입니다.

```
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## 사용자 정의 광고 큐 형식을 사용한 광고 삽입 {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe는 Primetime 패키지에서 직접 지원하지 않는 광고 큐 포맷의 이름을 제공합니다. 이러한 형식을 사용하려면 Adobe 제공 이름을 `ptcueformat` 매개 변수의 값으로 입력합니다.

다음은 사용자 지정 광고 큐 형식을 지정하는 샘플 URL입니다.

```
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## 광고 큐를 사용하여 VOD용 FreeWheel 타임라인 생성 {#section_E0D830F5EEE24639819B975B90F6999F}

광고 큐를 구문 분석하여 FreeWheel 광고 요청에 포함할 VOD 컨텐츠의 경우 `ptcueformat` 매개 변수의 값을 로 `DPIsimple`설정합니다.

다음은 VOD용 FreeWheel 타임라인을 사용하여 지정하는 샘플 URL입니다.

```
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## VOD용 사용자 정의 타임라인을 사용한 광고 삽입 {#section_F398F7659164463FA886A4CC787C7B5A}

매니페스트 서버에 사용자가 제공하는 타임라인에 따라 VOD 컨텐츠에 광고를 삽입하도록 요청하려면 매개 변수의 값을 타임라인을 지정하는 문자열로 `pttimeline` 설정합니다. VOD [타임라인 포맷 보기](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)

다음은 VOD용 사용자 정의 타임라인을 사용하는 샘플 URL입니다.

```
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

최대 2개의 광고를 포함한 1분간의 초기 휴식 시간, 2분간의 컨텐츠 세그먼트, 최대 2개의 광고를 포함하는 30초간의 휴식 시간, 그리고 5분 컨텐츠 세그먼트를 지정합니다.

VOD 컨텐츠에 대한 사용자 정의 컨텐츠 타임라인에 대한 광고 스티칭은 다음과 같이 작동합니다.

* 광고는 광고 서버에 의해 지정된 광고 배치 시간 이후 가장 가까운 분리 경계에 표시됩니다.
* 세그먼트는 최소 2초 길이입니다.

## TS 세그먼트 인증 {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe는 Akamai CDN에 대해서만 이 기능을 지원합니다. HLS(HTTP 라이브 스트리밍)는 스트림 수준 M3U8 재생 목록을 사용하여 TS(전송 스트림) 세그먼트를 제공합니다. 변형 M3U8 재생 목록에서 여러 스트림 수준 재생 목록이 클라이언트에 제공됩니다. 클라이언트는 변형 목록에서 하나의 재생 목록 스트림을 선택한 다음 해당 스트림 수준 재생 목록의 TS 세그먼트를 하나씩 다운로드합니다. 정상적인 작업에서 요청된 컨텐츠는 백그라운드에서 보이지 않게 처리되는 쿠키 승인이 필요할 수 있습니다. Raw 내용에서 쿠키를 추출하고 선택한 재생 목록 스트림을 요청하는 데 사용할 적절한 토큰을 URL에 추가합니다.

Bootstrap URL 쿼리 매개 변수가 포함되어 `pttoken=true`있으면 발행자는 전체 스트림에 한 번만 사용되는 것이 아니라 각 TS 세그먼트를 요청하는 데 쿠키를 사용해야 합니다. 매니페스트 서버는 이 쿠키를 쿼리 매개 변수로 스트림 재생 목록에 있는 각 TS 세그먼트 URL에 추가합니다.
