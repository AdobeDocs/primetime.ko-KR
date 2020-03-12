---
description: 광고 삽입 기능은 VOD(Video-On-Demand), 실시간 스트리밍, 광고 추적 및 광고 재생을 통한 선형 스트리밍을 위한 광고를 해결합니다. TVSDK는 광고 서버에 필요한 요청을 수행하고, 지정된 컨텐츠에 대한 광고에 대한 정보를 수신하며, 광고를 순차적으로 컨텐츠에 배치합니다.
seo-description: 광고 삽입 기능은 VOD(Video-On-Demand), 실시간 스트리밍, 광고 추적 및 광고 재생을 통한 선형 스트리밍을 위한 광고를 해결합니다. TVSDK는 광고 서버에 필요한 요청을 수행하고, 지정된 컨텐츠에 대한 광고에 대한 정보를 수신하며, 광고를 순차적으로 컨텐츠에 배치합니다.
seo-title: 광고 삽입
title: 광고 삽입
uuid: 6e31cae5-7363-454f-82dd-e03c1e34cd3f
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 광고 삽입 {#insert-ads}

광고 삽입 기능은 VOD(Video-On-Demand), 실시간 스트리밍, 광고 추적 및 광고 재생을 통한 선형 스트리밍을 위한 광고를 해결합니다. TVSDK는 광고 서버에 필요한 요청을 수행하고, 지정된 컨텐츠에 대한 광고에 대한 정보를 수신하며, 광고를 순차적으로 컨텐츠에 배치합니다.

시퀀스에서 재생되는 하나 이상의 광고가 *`ad break`* 포함되어 있습니다. TVSDK는 광고를 하나 이상의 광고 중단의 멤버로 기본 컨텐츠에 삽입합니다.

>[!TIP]
>
>광고에 오류가 있는 경우 TVSDK는 광고를 무시합니다.

## VOD 광고 해결 및 삽입 {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK 파섹

* 콘텐츠 시작 부분에 광고가 삽입되는 프리롤 광고 삽입
* 중간 롤 광고 삽입 - 컨텐츠 가운데에 하나 이상의 광고가 삽입됩니다.
* 컨텐츠 끝에 하나 이상의 광고가 추가되는 포스트롤 광고 삽입.

TVSDK는 광고를 확인하고 광고 서버가 정의한 위치에 광고를 삽입하며 재생이 시작되기 전에 가상 타임라인을 계산합니다. 재생이 시작되면 삽입되거나 삽입되는 광고와 같은 변경 사항이 발생하지 않습니다.

## 라이브 광고 및 선형 광고 확인 및 삽입 {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK는 라이브 및 선형 광고 확인 및 삽입 시 몇 가지 사용 사례를 지원합니다.

* 컨텐츠 시작 부분에 하나 이상의 광고가 삽입되는 프리롤 광고 삽입.
* 중간 롤 광고 삽입 - 컨텐츠 가운데에 하나 이상의 광고가 삽입됩니다.

TVSDK 파섹 기본적으로 TVSDK는 광고를 확인하고 배치할 때 다음 큐를 유효한 광고 마커로 지원합니다.

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

이러한 마커는 메타데이터 필드의 초 `DURATION` 단위 및 큐의 고유 ID가 필요합니다. 예:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

추가 신호에 대한 자세한 내용은 사용자 [정의 태그에](../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-custom-tags-subscribe.md)가입을 참조하십시오.

## 클라이언트 광고 추적 {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK 파섹

알림은 광고가 시작되는 시기와 광고가 끝나는 시기에 대한 정보를 포함하여 광고의 진행 상황을 애플리케이션에 알리는 데 사용됩니다.

## 조기 광고 중단 반환 구현 {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

라이브 스트림 광고 삽입의 경우 중단에 있는 모든 광고가 완료되기 전에 광고 중단에서 종료해야 할 수 있습니다.

다음은 초기 광고 브레이크 반품에 대한 몇 가지 예입니다.

* 특정 스포츠 이벤트의 광고 중단 기간입니다.

   기본 기간이 제공되지만, 중단이 끝나기 전에 게임이 재개되는 경우 광고 중단이 종료되어야 합니다.
* 라이브 스트림에서 광고 중단 중 긴급 신호입니다.

일찍 광고 중단에서 나가는 기능은 스플라이스 인 또는 큐 인 태그로 알려진 매니페스트의 사용자 지정 태그를 통해 식별됩니다. TVSDK를 사용하면 애플리케이션에서 이러한 스플라이스(splice-in) 태그에 가입할 수 있으므로 특별한 기회를 얻을 수 있습니다.

* 이 `#EXT-X-CUE-IN` 태그를 스플라이스 인 기회로 사용하고 조기 광고 중단 반환을 구현하려면

   1. 태그에 가입합니다.

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. 큐 인 기회 해결 프로그램을 추가합니다.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* 스플라이아웃 및 스플라이인에 대해 동일한 태그를 공유하려면:

1. 애플리케이션에서 큐 아웃/스플라이스 아웃 및 큐 인/스플리스를 나타내기 위해 동일한 큐를 공유하는 `PTDefaultAdOpportunityResolver` 경우 해당 `preparePlacementOpportunity` 메서드를 확장 및 구현합니다.

   [!TIP]

   다음 코드에서는 앱에 `isCueInOpportunity` 메서드에 대한 구현이 있다고 가정합니다.

```
   - (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
   { 
         if ([self isCueInOpportunity:timedMetadata]) 
         { 
               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
           } 
           else 
           { 
               return [super preparePlacementOpportunity:timedMetadata]; 
         } 
   }
```

1. 인스턴스에 확장 기회 해결 프로그램을 `PTDefaultMediaPlayerClientFactory` 등록합니다.

```
   // self.player is the PTMediaPlayer instance created for content and ad playback 
       PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
             
   // Clear existing resolver and register the new opportunity resolver 
   [clientFactory clearOpportunityResolvers]; 
   [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
```
