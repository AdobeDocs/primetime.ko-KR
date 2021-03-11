---
description: TVSDK는 선형 광고를 수반하며 선형 광고가 끝난 후에도 종종 페이지에 유지되는 광고인 컴패니언 배너 광고를 지원합니다. 애플리케이션은 선형 광고와 함께 제공되는 부속 배너를 표시해야 합니다.
title: 컴패니언 배너 광고
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# 부록 배너 광고 {#companion-banner-ads}

TVSDK는 선형 광고를 수반하며 선형 광고가 끝난 후에도 종종 페이지에 유지되는 광고인 컴패니언 배너 광고를 지원합니다. 애플리케이션은 선형 광고와 함께 제공되는 부속 배너를 표시해야 합니다.

부록 광고를 표시할 때는 다음 권장 사항을 따르십시오.

* 플레이어의 레이아웃에 맞게 비디오 광고의 컴패니언 배너 광고를 최대한 표시하려고 합니다.
* 지정된 높이 및 폭과 정확히 일치하는 위치가 있는 경우에만 컴패니언 배너를 표시합니다.

   >[!TIP]
   >
   >배너 크기를 조정하지 마십시오.

* 광고가 시작된 후 가능한 한 빨리 컴패니언 배너를 제공합니다.
* 기본 광고/비디오 컨테이너와 함께 사용할 배너를 오버레이하지 마십시오.
* 광고가 끝난 후에도 계속 함께 배너를 표시합니다.

   이 배너를 대체하기 전까지 표준 배너는 각 컴패니언 배너를 표시합니다.

## 컴패니언 배너 데이터 {#companion-banner-data}

PTAdAsset의 내용은 컴패니언 배너를 설명합니다.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

`PTMediaPlayerAdStartedNotification` 알림은 `companionAssets` 속성(`PtAdAsset`의 배열)이 포함된 `PTAd` 인스턴스를 반환합니다.
각 `PtAdAsset`은 에셋 표시에 대한 정보를 제공합니다.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 사용 가능한 정보 </th> 
   <th colname="col2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 너비 </td> 
   <td colname="col2"> 컴패니언 배너의 폭(픽셀 단위)입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> 컴패니언 배너의 높이(픽셀 단위)입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 리소스 유형 </td> 
   <td colname="col2">이 컴패니언 배너의 리소스 유형: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:데이터는 HTML 코드에 있습니다. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:데이터는 iframe URL(src)입니다. </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">정적:데이터는 이미지에 대한 직접 URL인 staticURL입니다. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 데이터 </td> 
   <td colname="col2"> 이 컴패니언 배너에 대해 <span class="codeph"> resourceType</span>에서 지정한 유형의 데이터입니다. </td> 
  </tr> 
 </tbody> 
</table>

## 배너 광고 표시 {#display-banner-ads}

배너 광고를 표시하려면 배너 인스턴스를 만들고 TVSDK가 광고 관련 이벤트를 수신하도록 허용해야 합니다.

TVSDK는 `PTMediaPlayerAdPlayStartedNotification` 알림 이벤트를 통해 선형 광고와 연관된 컴패니언 배너 광고 목록을 제공합니다.

매니페스트는 다음과 같은 방법으로 컴패니언 배너 광고를 지정할 수 있습니다.

* HTML 조각
* iFrame 페이지의 URL
* 정적 이미지 또는 Adobe Flash SWF 파일의 URL

각 컴패니언 광고에 대해 TVSDK는 애플리케이션에 사용 가능한 유형을 나타냅니다.

1. 페이지의 각 컴패니언 광고 슬롯에 대해 `PTAdBannerView` 인스턴스를 만듭니다.

       다음 정보가 제공되었는지 확인합니다.
   
   * 크기가 다른 컴패니언 광고를 검색할 수 없도록 너비와 높이를 지정하는 배너 인스턴스입니다.
   * 표준 배너 크기.

1. 다음을 수행하는 `PTMediaPlayerAdStartedNotification`의 관찰자를 추가합니다.
   1. 배너 인스턴스에서 기존 광고를 지웁니다.
   1. `Ad.getCompanionAssets` `PTAd.companionAssets`에서 부록 광고 목록을 가져옵니다.
   1. 컴패니언 광고 목록이 비어 있지 않으면 배너 인스턴스 목록을 반복합니다.

      각 배너 인스턴스( `PTAdAsset`)에는 폭, 높이, 리소스 유형(html, iframe 또는 static)과 같은 정보와 함께 사용 가능한 배너를 표시하는 데 필요한 데이터가 포함되어 있습니다.
   1. 비디오 광고에 이와 함께 예약된 부록 광고가 없는 경우 컴패니언 자산 목록에는 해당 비디오 광고에 대한 데이터가 포함되어 있지 않습니다.

      독립 실행형 디스플레이 광고를 표시하려면 해당 배너 인스턴스에 일반 DFP(발행자를 위한 DoubleClick)를 실행하는 논리를 스크립트에 추가합니다.
   1. 배너를 적절한 위치에 표시하는 함수에 배너 정보를 보냅니다.

      일반적으로 `div`이고 사용자의 함수는 `div ID`를 사용하여 배너를 표시합니다. 예:

      ```
      - (void) onMediaPlayerAdPlayStarted:(NSNotification *) notification { 
          _currentAd  = [notification.userInfo  objectForKey:PTMediaPlayerAdKey];  
          if (_currentAd != nil) { 
              [self removeAllBanners]; // remove any existing PTAdBannerView views 
      
              // banners 
              if (_currentAd.companionAssets && _currentAd.companionAssets.count > 0) { 
                  PTAdAsset *bannerAsset = [_currentAd.companionAssets objectAtIndex:0]; 
      
                  PTAdBannerView *bannerView = [[PTAdBannerView alloc] initWithAsset:bannerAsset];  
                  bannerView.player = self.player; 
                  bannerView.delegate = self; 
      
                  bannerView.frame = CGRectMake(0.0, 0.0, bannerAsset.width, bannerAsset.height);  
                  [_adBannerView.bannerView addSubview:bannerView]; 
              } 
          } 
      }
      ```
