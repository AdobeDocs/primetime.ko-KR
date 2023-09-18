---
description: 광고 삽입은 주문형 비디오(VOD), 라이브 스트리밍, 광고 추적 및 광고 재생을 통한 선형 스트리밍 광고를 해결합니다. TVSDK는 광고 서버에 필요한 요청을 하고, 지정된 컨텐츠에 대한 광고 정보를 수신하고, 단계별로 광고를 컨텐츠에 배치합니다.
title: 광고 삽입
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 광고 삽입{#insert-ads}

광고 삽입은 주문형 비디오(VOD), 라이브 스트리밍, 광고 추적 및 광고 재생을 통한 선형 스트리밍 광고를 해결합니다. TVSDK는 광고 서버에 필요한 요청을 하고, 지정된 컨텐츠에 대한 광고 정보를 수신하고, 단계별로 광고를 컨텐츠에 배치합니다.

An *`ad break`* 에는 차례로 재생되는 하나 이상의 광고가 포함되어 있습니다. TVSDK는 하나 이상의 광고 브레이크의 구성원으로 기본 콘텐츠에 광고를 삽입합니다.

>[!TIP]
>
>광고에 오류가 있으면 TVSDK는 광고를 무시합니다.

## VOD 광고 확인 및 삽입 {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK는 VOD 광고 확인 및 삽입에 대한 여러 사용 사례를 지원합니다.

* 프리롤 광고 삽입. 여기서 광고는 콘텐츠 시작 부분에 삽입됩니다.
* 미드롤 광고 삽입. 콘텐츠의 중간에 하나 이상의 광고가 삽입됩니다.
* 게시물 롤 광고 삽입. 여기서 하나 이상의 광고가 콘텐츠 끝에 추가됩니다.

TVSDK는 광고를 확인하고 광고 서버에서 정의한 위치에 광고를 삽입하며 재생이 시작되기 전에 가상 타임라인을 계산합니다. 재생이 시작된 후에는 광고가 삽입되거나 삽입된 광고가 제거되는 것과 같은 변경 사항이 발생하지 않습니다.

## 라이브 및 선형 광고 확인 및 삽입 {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK는 라이브 및 선형 광고 해결 및 삽입에 대한 여러 사용 사례를 지원합니다.

* 프리롤 광고 삽입 - 콘텐츠의 시작 부분에 하나 이상의 광고가 삽입됩니다.
* 미드롤 광고 삽입. 콘텐츠의 중간에 하나 이상의 광고가 삽입됩니다.

TVSDK는 라이브 또는 선형 스트림에서 큐 포인트가 발견되면 광고를 확인하고 광고를 삽입합니다. 기본적으로 TVSDK는 광고를 해결하고 배치할 때 다음 큐를 유효한 광고 마커로 지원합니다.

* #EXT-X-CUEPOINT
* #EXT-X-AD
* #EXT-X-CUE
* #EXT-X-CUE-OUT

이러한 마커에는 메타데이터 필드의 `DURATION` 초 단위와 큐의 고유 ID. 예:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

추가 단서에 대한 자세한 내용은 [사용자 정의 태그 구독](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md).

## 클라이언트 광고 추적 {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK는 VOD 및 라이브/선형 스트리밍 광고를 자동으로 추적합니다.

알림은 광고가 시작되는 시기와 종료되는 시기에 대한 정보를 포함하여 광고의 진행 상황에 대해 애플리케이션에 알리는 데 사용됩니다.

## 조기 광고 브레이크 반환 구현 {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

라이브 스트림 광고 삽입의 경우, 광고 브레이크의 모든 광고가 완료될 때까지 재생되기 전에 광고 브레이크를 종료해야 할 수 있습니다.

다음은 조기 광고 브레이크 반환에 대한 몇 가지 예입니다.

* 특정 스포츠 이벤트의 광고 브레이크 기간.

  기본 기간이 제공되지만, 휴식기가 완료되기 전에 게임이 재개되는 경우 광고 브레이크를 종료해야 합니다.
* 라이브 스트림에서 광고 브레이크 중에 발생하는 긴급 신호입니다.

광고 브레이크를 조기에 종료하는 기능은 스플라이스 인 또는 큐 인 태그라고 하는 매니페스트의 사용자 지정 태그를 통해 식별됩니다. TVSDK를 사용하면 애플리케이션에서 이러한 스플라이스 인 태그를 구독하여 스플라이스 인 기회를 제공할 수 있습니다.

* 을(를) 사용하려면 `#EXT-X-CUE-IN` 를 스플라이스 인 기회로 태그 지정하고 조기 광고 브레이크 반환을 구현합니다.

   1. 태그에 가입합니다.

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. 큐 인 기회 해결자를 추가합니다.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* 스플라이스-아웃과 스플라이스-인에 대해 동일한 태그를 공유하려면

   1. 응용 프로그램에서 동일한 큐를 공유하여 큐 아웃/스플라이스 아웃과 큐 인/스플라이스 인을 나타내는 경우 를 확장합니다 `PTDefaultAdOpportunityResolver` 및 구현 `preparePlacementOpportunity` 메서드를 사용합니다.

      >[!TIP]
      >
      >다음 코드에서는 앱에 `isCueInOpportunity` 메서드를 사용합니다.
      >
      >```
      >- (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
      >{ 
      >       if ([self isCueInOpportunity:timedMetadata]) 
      >       { 
      >               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
      >       } 
      >       else 
      >       { 
      >               return [super preparePlacementOpportunity:timedMetadata]; 
      >       } 
      >}
      >```
      >

   1. 에서 확장 영업 기회 확인자 등록 `PTDefaultMediaPlayerClientFactory` 인스턴스.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```
