---
description: 비디오 사용을 추적하고 분석하도록 플레이어를 구성할 수 있습니다.
title: 비디오 분석 초기화 및 구성
exl-id: 58d560d1-f668-4e1d-a817-b2e02008fdbe
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# 비디오 분석 초기화 및 구성{#initialize-and-configure-video-analytics}

비디오 사용을 추적하고 분석하도록 플레이어를 구성할 수 있습니다.

비디오 추적(비디오 하트비트)을 활성화하기 전에 다음 사항이 있는지 확인하십시오.

* 데스크탑 HLS용 TVSDK
* 구성/초기화 정보 - 특정 비디오 추적 계정 정보는 Adobe 담당자에게 문의하십시오.

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> AppMeasurement 추적 서버 엔드포인트 </td> 
   <td colname="col2"> Adobe Analytics(이전 SiteCatalyst) 백엔드 컬렉션 엔드포인트의 URL입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Video Analytics 추적 서버 끝점 </td> 
   <td colname="col2"> 비디오 분석 백엔드 컬렉션 엔드포인트의 URL입니다. 여기서 모든 비디오 하트비트 추적 호출이 전송됩니다. <p>팁: 방문자 추적 서버의 URL은 Analytics 추적 서버의 URL과 동일합니다. 방문자 ID 서비스 구현에 대한 정보는 다음을 참조하십시오. <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> ID 서비스 구현 </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 계정 이름 </td> 
   <td colname="col2"> RSID(보고서 세트 ID)라고도 합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud 조직 ID </td> 
   <td colname="col2"> 방문자 구성 요소를 인스턴스화하는 데 필요한 문자열 값입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 방문자 추적 서버 엔드포인트 </td> 
   <td colname="col2"> 현재 비디오 뷰어에 대한 고유 식별자를 제공하는 백엔드 엔드포인트의 URL입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 게시자 </td> 
   <td colname="col2"> Adobe 담당자가 고객에게 제공하는 게시자 ID입니다. <p>팁: 이 ID는 브랜드/TV 이름을 사용하는 문자열일 뿐만 아닙니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

플레이어에서 비디오 추적을 구성하려면:

1. VisitorAPI 라이브러리를 인스턴스화하고 구성합니다.

       다음 정보를 염두에 두십시오.
   
   * 인스턴스화에는 Adobe에서 제공하는 Marketing Cloud 조직 ID 입력 매개 변수가 필요합니다.

      문자열 값입니다.
   * VisitorAPI 라이브러리에 대한 유일한 구성 옵션은 현재 사용자의 고유 식별자를 제공하는 백엔드 끝점의 URL입니다.
   * 방문자 추적 서버의 URL은 Analytics 추적 서버의 URL과 동일합니다.

      방문자 ID 서비스 구현에 대한 내용은 방문자 ID 서비스 구현 을 참조하십시오.

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
   ```

1. AppMeasurement 구성 요소를 인스턴스화하고 구성합니다.

   AppMeasurement 인스턴스에는 많은 구성 옵션이 있습니다. 자세한 내용은 [Adobe Analytics 개발자](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) 설명서를 참조하십시오. 다음 샘플 코드의 옵션( `account`, `visitorNamespace`, 및 `trackingServer`)는 필수이며, 값은 Adobe에서 제공합니다.

   >[!IMPORTANT]
   >
   >종속성 체인이 올바르게 설정되었는지 확인해야 합니다. AppMeasurement 인스턴스는 방문자 API 구성 요소를 집계(종속됨)합니다.

   ```
   // Instantiate and configure AppMeasurement 
   
   // Instantiate AppMeasurement instance only once! 
   if (_appMeasurementObject == null) {  
       _appMeasurementObject = new AppMeasurement(); 
   } 
   
   with (_appMeasurementObject) { 
       account = "ACCOUNT_NAME"; // Also known as RSID 
       trackingServer = "URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER"; 
   
       // Use the same value here as for the Visitor API component 
       visitorNamespace = "MARKETING_CLOUD_ORG_ID"; 
   
       // Attach the Visitor API to the AppMeasurement instance. 
       visitor = _visitor;  
       pageName = "pageName"; 
       charSet = "UTF-8"; 
       currencyCode = "USD"; 
   } 
   ```

   >[!IMPORTANT]
   >
   >응용 프로그램에서 다음을 확인합니다. `appMeasurementObject.visitor` 는 비디오 분석 흐름을 시작하기 전에 채워집니다. 그렇지 않으면 추적 결과를 얻지 못할 수 있습니다. 이러한 결과는 로그의 메시지로 표시됩니다. 빈 추적 호출( )을 추가할 수 있습니다. `appMeasurementObject.track`), 다음을 폴링합니다. `visitor` 속성이 채워질 때까지 속성을 확인하고 비디오 분석을 시작합니다.

1. 비디오 하트비트 추적 메타데이터를 초기화하고 구성합니다.

   >[!IMPORTANT]
   >
   >Video Analytics 모듈 미드스트림을 중지하고 필요에 따라 다시 초기화할 수 있습니다. 모듈이 다시 초기화되기 전에 비디오 분석 메타데이터도 올바른 콘텐츠 메타데이터로 업데이트되었는지 확인하십시오. 메타데이터를 다시 생성하려면 하위 단계 1과 2를 반복합니다.

   1. Video Analytics 메타데이터의 인스턴스를 만듭니다.

      이 인스턴스에는 비디오 하트비트 추적을 활성화하는 데 필요한 모든 구성 정보가 포함되어 있습니다. 예:

      ```
      private function getVideoAnalyticsTrackingMetadata():VideoAnalyticsMetadata {     
          // Initialize visitor id service and appMeasurement      
          [...] // as shown in the previous steps     
      
          var vaMetadata:VideoAnalyticsMetadata = new VideoAnalyticsMetadata(); 
      
          with (vaMetadata) { 
              trackingServer = "hbTrackingServer"; 
              publisher = "hbPublisher"; 
              channel = "hbChannel";  
              playerName = "hbPlayerName"; 
      
              // this overwrites the ContextData variable a.media.friendlyName 
              videoName = "hbFriendlyName";  
      
              // this will overwrite the ContextData variable a.media.name 
              videoId = "hbName"; 
      
              enableChapterTracking = true; 
      
              // Set these to false for production deployment 
              debugLogging = true;  
              quietMode = false; 
      
          } 
      } 
      ```

   1. 전역 메타데이터 인스턴스에 Video Analytics 메타데이터를 추가합니다.

      준비가 되면 미디어 리소스 또는 미디어 플레이어 항목에서 전역 메타데이터 인스턴스를 설정합니다.

      ```
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```

   1. Video Analytics 추적기를 초기화합니다.

      미디어 플레이어 인스턴스를 만든 후에는 Video Analytics 추적기 인스턴스를 만들고 미디어 플레이어 인스턴스에 대한 참조를 제공해야 합니다.

      >[!TIP]
      >
      >미디어 플레이어 인스턴스를 분리한 후 항상 각 컨텐츠 재생 세션에 대한 새 추적기 인스턴스를 만들고 이전 참조를 제거합니다.

      ```
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. Video Analytics 추적기를 제거합니다.

      새 컨텐츠 재생 세션을 시작하기 전에 비디오 추적기의 이전 인스턴스를 제거합니다. 콘텐츠 완료 이벤트(또는 알림)를 받은 후 비디오 추적기 인스턴스를 제거하기 전에 몇 분 정도 기다리십시오. 인스턴스를 즉시 제거하면 비디오 전체 Ping을 전송하는 Video Analytics 추적기의 기능에 방해가 될 수 있습니다.

      ```
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```

   1. 라이브/선형 스트림을 완료된 것으로 수동으로 표시합니다.

      하나의 라이브 스트림에 다양한 에피소드가 있는 경우 전체 API를 사용하여 에피소드를 완료로 수동으로 표시할 수 있습니다. 이렇게 하면 현재 비디오 에피소드에 대한 비디오 추적 세션이 종료되며 다음 에피소드에 대한 새 추적 세션을 시작할 수 있습니다.

      >[!TIP]
      >
      >이 API는 선택 사항이며 VOD 비디오 추적에 필요하지 않습니다.
