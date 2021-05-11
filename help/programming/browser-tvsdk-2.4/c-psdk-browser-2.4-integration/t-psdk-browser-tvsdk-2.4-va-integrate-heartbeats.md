---
description: 비디오 사용을 추적 및 분석하도록 플레이어를 구성할 수 있습니다.
title: 비디오 분석 초기화 및 구성
exl-id: e0bf461b-a431-4fba-bd3d-c38be307a92f
translation-type: tm+mt
source-git-commit: d884836a2a585bd3540b085de1098cf6ae3de46b
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# 비디오 분석 초기화 및 구성 {#initialize-and-configure-video-analytics}

비디오 사용을 추적 및 분석하도록 플레이어를 구성할 수 있습니다.

비디오 추적(비디오 하트비트)을 활성화하기 전에 다음 내용이 있는지 확인합니다.

* 구성/브라우저 TVSDK 초기화 정보 - 특정 비디오 추적 계정 정보는 Adobe 담당자에게 문의하십시오.

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
  <tr>
   <td colname="col1"> AppMeasurement 추적 서버 끝점 </td>
   <td colname="col2"> Adobe Analytics(이전 SiteCatalyst) 백엔드 컬렉션 끝점의 URL. </td>
  </tr>
  <tr>
   <td colname="col1"> 비디오 분석 추적 서버 끝점 </td>
   <td colname="col2"> 비디오 분석 백엔드 컬렉션 끝점의 URL. 모든 비디오 하트비트 추적 호출이 전송되는 곳입니다. <p>팁: 방문자 추적 서버의 URL은 분석 추적 서버의 URL과 동일합니다. 방문자 ID 서비스 구현에 대한 자세한 내용은 <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> ID 서비스 구현 </a>을 참조하십시오. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> 계정 이름 </td>
   <td colname="col2"> 보고서 세트 ID(RSID)라고도 합니다. </td>
  </tr>
  <tr>
   <td colname="col1"> Marketing Cloud 조직 ID </td>
   <td colname="col2"> 방문자 구성 요소를 인스턴스화하는 데 필요한 문자열 값입니다. </td>
  </tr>
  <tr>
   <td colname="col1"> 방문자 추적 서버 끝점 </td>
   <td colname="col2"> 현재 비디오 뷰어에 대한 고유 식별자를 제공하는 백엔드 끝점의 URL입니다. </td>
  </tr>
  <tr>
   <td colname="col1"> 게시자 </td>
   <td colname="col2"> Adobe 담당자가 고객에게 제공하는 게시자 ID입니다. <p>팁: 이 ID는 브랜드/TV 이름을 가진 문자열만이 아닙니다. </p> </td>
  </tr>
 </tbody>
</table>

플레이어에서 비디오 추적을 구성하려면:

1. VisitorAPI 라이브러리를 인스턴스화하고 구성합니다.

       다음 정보를 염두에 두십시오.
   
   * 인스턴스화를 사용하려면 Adobe에서 제공하는 Marketing Cloud 조직 ID 입력 매개 변수가 필요합니다.

      문자열 값입니다.
   * VisitorAPI 라이브러리에 대한 유일한 구성 옵션은 현재 사용자에 대한 고유 식별자를 제공하는 백엔드 끝점의 URL입니다.
   * 방문자 추적 서버의 URL은 분석 추적 서버의 URL과 동일합니다.

      방문자 ID 서비스 구현에 대한 자세한 내용은 [방문자 ID 서비스 구현](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html)을 참조하십시오.

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. AppMeasurement 구성 요소를 인스턴스화하고 구성합니다.

   AppMeasurement 인스턴스에는 많은 구성 옵션이 있습니다. 자세한 내용은 [Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) 설명서를 참조하십시오. 다음 샘플 코드의 옵션( `account`, `visitorNamespace` 및 `trackingServer`)이 필요하며 이 값은 Adobe에서 제공합니다.

   >[!IMPORTANT]
   >
   >종속성 체인이 올바르게 설정되었는지 확인해야 합니다. AppMeasurement 인스턴스는 방문자 API 구성 요소를 집계합니다(종속적).

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = 'URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER';
   appMeasurement.account = 'ACCOUNT_NAME'; // Also known as RSID
   appMeasurement.pageName = 'Sample Page Name';
   appMeasurement.charSet = "UTF-8";
   appMeasurement.visitorID = "test-vid";
   ```

   >[!IMPORTANT]
   >
   >응용 프로그램에서 비디오 분석 흐름을 시작하기 전에 `appMeasurementObject.visitor`이 채워졌는지 확인하거나 추적 결과를 얻지 못할 수 있습니다. 이러한 결과는 로그에 있는 메시지로 표시됩니다. 빈 트랙 호출( `appMeasurementObject.track`)을 추가하고, 채워진 상태로 전환될 때까지 `visitor` 속성을 폴링하고 비디오 분석을 시작할 수 있습니다.

3. 비디오 하트비트 추적 메타데이터를 초기화하고 구성합니다.

   >[!IMPORTANT]
   >
   >비디오 분석 모듈 중간스트림을 중지하고 필요에 따라 다시 초기화할 수 있습니다. 모듈이 다시 초기화되기 전에 비디오 분석 메타데이터도 올바른 컨텐츠 메타데이터로 업데이트되었는지 확인합니다. 메타데이터를 다시 만들려면 하위 단계 1 및 2를 반복합니다.

   1. 비디오 분석 메타데이터의 인스턴스를 만듭니다.
이 인스턴스에는 비디오 하트비트 추적을 활성화하는 데 필요한 모든 구성 정보가 포함되어 있습니다. 예:

      ```js
      function getVideoAnalyticsMetadata() {
          var vaObj = new AdobePSDK.VA.VideoAnalyticsMetadata();
          vaObj.appMeasurement = appMeasurement;
          vaObj.trackingServer = 'hbTrackingServer';
          vaObj.publisher = 'hbPublisher';
          vaObj.channel = 'sample-channel';
          vaObj.playerName = 'TVSDK-HTML';
          vaObj.appVersion = '1.0.0';
          vaObj.videoName = 'hbFriendlyName'; // this will overwrite the ContextData variable a.media.friendlyName
          vaObj.assetDuration = durationInSeconds;
          // use this to override the default asset length of -1 for live streams
          vaObj.debugLogging = false;
          return vaObj;
      }
      ```

   2. 미디어 플레이어 인스턴스를 만든 후 비디오 분석 추적기 인스턴스를 만들고 미디어 플레이어 인스턴스에 대한 참조를 제공합니다.
다음 사항을 기억하십시오.

      * 각 컨텐츠 재생 세션에 대해 항상 새로운 추적기 인스턴스를 만들고 미디어 플레이어 인스턴스를 분리한 후 이전 참조를 제거합니다.
      * 1단계에서 만든 메타데이터는 비디오 분석 추적기의 생성자에 제공해야 합니다.

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. 비디오 분석 추적기를 제거합니다.
새 컨텐츠 재생 세션을 시작하기 전에 비디오 추적기의 이전 인스턴스를 삭제합니다. 컨텐츠 완료 이벤트(또는 알림)를 받은 후 비디오 추적기 인스턴스를 제거하기 전에 몇 분 정도 기다립니다. 인스턴스를 즉시 제거하면 비디오 분석 추적기가 비디오 전체 ping을 전송하는 기능을 방해할 수 있습니다.

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```

   4. 라이브/선형 스트림을 완료로 수동으로 표시합니다.
하나의 라이브 스트림에 다양한 에피소드가 있는 경우 전체 API를 사용하여 에피소드를 완료로 수동으로 표시할 수 있습니다. 이렇게 하면 현재 비디오 에피소드에 대한 비디오 추적 세션이 종료되며 다음 에피소드에 대해 새 추적 세션을 시작할 수 있습니다.
      >[!TIP]
      >
      >이 API는 선택 사항이며 VOD 비디오 추적에는 필요하지 않습니다.

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      }
      ```
