---
description: 'null'
seo-description: 'null'
seo-title: 비디오 분석 초기화 및 구성
title: 비디오 분석 초기화 및 구성
uuid: 98017a20-4997-42f7-9b03-fd9c4b6ccd92
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# 비디오 분석 시작 및 구성 {#initialize-and-configure-video-analytics}

비디오 사용을 추적 및 분석하도록 플레이어를 구성할 수 있습니다.
비디오 추적(비디오 하트비트)을 활성화하기 전에 다음 사항을 확인하십시오.

* Android용 TVSDK 2.5
* 구성/초기화 정보

   특정 비디오 추적 계정 정보는 Adobe 담당자에게 문의하십시오.

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>중요: 이 JSON 구성 파일 이름은 <span class="filepath"> ADBMobileConfig.json </span>으로 유지되어야 합니다. 이 구성 파일의 이름과 경로는 변경할 수 없습니다. 이 파일의 경로는 <span class="filepath"> &lt;source root&gt;/assets </span>이어야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AppMeasurement 추적 서버 끝점 </td> 
   <td colname="col2"> Adobe Analytics(이전 SiteCatalyst) 백엔드 컬렉션 끝점의 URL입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 비디오 분석 추적 서버 끝점 </td> 
   <td colname="col2"> 비디오 분석 백엔드 컬렉션 끝점의 URL. 이 위치에서 모든 비디오 하트비트 추적 호출이 전송됩니다. <p>팁: 방문자 추적 서버의 URL은 분석 추적 서버의 URL과 동일합니다. 방문자 ID 서비스 구현에 대한 자세한 내용은 <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> ID 서비스 구현 </a>을 참조하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 계정 이름 </td> 
   <td colname="col2"> 보고서 세트 ID(RSID)라고도 합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud 조직 ID </td> 
   <td colname="col2"> 방문자 구성 요소를 인스턴스화하는 데 필요한 문자열 값입니다. </td> 
  </tr> 
 </tbody> 
</table>

플레이어에서 비디오 추적을 구성하려면:

1. `ADBMobileConfig.json` 리소스 파일의 로드 시간 옵션이 올바른지 확인합니다.

   ```
   { 
       "version" : "1.1", 
       "analytics" : { 
           "rsids" : "adobedevelopment", 
           "server" : "10.131.129.149:3000", 
           "charset" : "UTF-8", 
           "ssl" : false, 
           "offlineEnabled" : false, 
           "lifecycleTimeout" : 5, 
           "batchLimit" : 50, 
           "privacyDefault" : "optedin", 
           "poi" : [] 
       }, 
       "marketingCloud": { 
           "org": "ADOBE PROVIDED VALUE"  
       }, 
       "target" : { 
           "clientCode" : "", 
           "timeout" : 5 
       }, 
       "audienceManager" : { 
           "server" : "" 
       } 
   }
   ```

   이 JSON 형식 구성 파일은 TVSDK가 포함된 리소스로 번들로 제공됩니다. 플레이어는 로드 시간에만 이러한 값을 읽고 응용 프로그램이 실행되는 동안 값은 일정하게 유지됩니다.

   로드 시간 옵션을 구성하려면:


   1. `ADBMobileConfig.json` 파일에 적절한 값(Adobe에서 제공)이 포함되어 있는지 확인합니다.
   1. 이 파일이 `assets/` 폴더에 있는지 확인합니다.

      이 폴더는 응용 프로그램 소스 트리의 루트에 있어야 합니다.

   1. 애플리케이션을 컴파일하고 구축할 수 있습니다.
   1. 번들 애플리케이션을 배포 및 실행합니다.

      이러한 AppMeasurement 설정에 대한 자세한 내용은 [Adobe Analytics에서 비디오 측정](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/)을 참조하십시오.

1. 비디오 하트비트 추적 메타데이터를 초기화하고 구성합니다.

   >[!IMPORTANT]
   >
   >비디오 분석 모듈 중간 스트림을 중지하고 필요에 따라 다시 초기화할 수 있습니다. 모듈이 다시 초기화되기 전에 비디오 분석 메타데이터도 올바른 컨텐츠 메타데이터로 업데이트되었는지 확인하십시오. 메타데이터를 다시 만들려면 아래의 처음 두 단계를 반복합니다(하위 단계 **a** 및 **b**).

   1. 비디오 분석 메타데이터의 인스턴스를 만듭니다.

      이 인스턴스는 비디오 하트비트 추적을 활성화하는 데 필요한 모든 구성 정보를 포함합니다. 예:

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. 비디오 분석 공급자를 초기화합니다.

      미디어 플레이어 인스턴스를 만든 후 비디오 분석 공급자 인스턴스를 만들고 여기에 애플리케이션 컨텍스트를 제공해야 합니다.

      >[!TIP]
      >
      >미디어 플레이어 인스턴스를 분리한 후에는 항상 각 컨텐츠 재생 세션에 대해 새 공급자 인스턴스를 만들고 이전 참조를 제거합니다.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. `videoAnalyticsProvider` 인스턴스에서 비디오 분석 메타데이터를 설정합니다.

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. 미디어 플레이어 인스턴스를 `videoAnalyticsProvider` 인스턴스에 첨부:

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. 비디오 분석 공급자를 제거합니다.

      새로운 컨텐츠 재생 세션을 시작하기 전에 비디오 공급자의 이전 인스턴스를 파기하십시오. 컨텐츠 완료 이벤트(또는 알림)를 받은 후 비디오 분석 공급자 인스턴스를 제거하기 전에 몇 분 정도 기다립니다. 인스턴스를 즉시 제거하면 &quot;비디오 완료&quot; ping을 전송하는 비디오 분석 공급자의 기능이 충돌할 수 있습니다.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. 라이브/선형 스트림을 완료로 수동으로 표시합니다.

      하나의 라이브 스트림에 다양한 에피소드가 있는 경우 전체 API를 사용하여 에피소드를 완료로 수동으로 표시할 수 있습니다. 현재 비디오 에피소드에 대한 비디오 추적 세션이 종료되며 다음 에피소드에 대해 새 추적 세션을 시작할 수 있습니다.

      >[!TIP]
      >
      >이 API는 선택 사항이며 VOD 비디오 추적에는 작동하지 않습니다.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```

