---
title: DRMContentData를 사용하여 라이센스 미리 로드
description: DRMContentData를 사용하여 라이센스 미리 로드
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# DRMContentData를 사용하여 라이센스 미리 로드{#using-drmcontentdata-to-pre-load-licenses}

다음 절차에서는 를 사용하여 보호된 미디어 파일에 대한 라이센스를 미리 로드하는 워크플로를 설명합니다. `DRMContentData` 개체.

1. 패키지된 콘텐츠에 대한 바이너리 DRM 메타데이터를 가져옵니다.

   Primetime DRM Java Reference Implementations Packager를 사용하는 경우 이 메타데이터 파일은 [!DNL .metadata] 확장명. 예를 들어 다음을 사용하여 이 메타데이터를 다운로드할 수 있습니다. `URLLoader` 클래스. HLS 또는 HDS 콘텐츠를 사용하는 경우 콘텐츠 매니페스트 파일( )에서 메타데이터가 참조됩니다. [!DNL .m3u8] 또는 [!DNL .f4m]) 또는 포함됨 *다음 범위 내* 매니페스트 파일을 Base64로 인코딩된 문자열(소비하기 전에 Base64로 디코딩해야 함)로 지정합니다.
1. 만들기 `DRMContentData` 개체, 메타데이터를 생성자 함수에 전달:

   ```
   var drmData:DRMContentData = new DRMContentData( metadata );
   ```

1. 나머지 단계는에 설명된 워크플로와 동일합니다 *콘텐츠 보호 프로세스 세부 정보*.

<!--<a id="example_EBEDA8E10F6344CABA4DE31DC342B8F8"></a>-->

```
import flash.events.DRMAuthenticationCompleteEvent; 
import flash.events.DRMAuthenticationErrorEvent; 
import flash.events.DRMErrorEvent; 
import flash.events.DRMStatusEvent; 
import flash.events.NetStatusEvent; 
import flash.net.NetConnection; 
import flash.net.Primetime; 
import flash.net.PrimetimePlayOptions; 
import flash.net.drm.AuthenticationMethod; 
import flash.net.drm.DRMContentData; 
import flash.net.drm.DRMManager; 
import flash.net.drm.LoadVoucherSetting; 
  
public class DRMPreloader extends Sprite  { 
    private var videoURL:String = "app-storage:/video.flv"; 
    private var userName:String = "user"; 
    private var password:String = "password"; 
    private var preloadConnection:NetConnection; 
    private var preloadStream:Primetime; 
    private var drmManager:DRMManager = DRMManager.getDRMManager(); 
 
    private var drmContentData:DRMContentData; 
 
    public function DRMPreloader():void { 
        drmManager.addEventListener(  
          DRMAuthenticationCompleteEvent.AUTHENTICATION_COMPLETE,  
          onAuthenticationComplete 
        ); 
        drmManager.addEventListener( 
          DRMAuthenticationErrorEvent.AUTHENTICATION_ERROR,  
          onAuthenticationError 
        ); 
        drmManager.addEventListener( 
          DRMStatusEvent.DRM_STATUS, onDRMStatus); 
        drmManager.addEventListener( 
          DRMErrorEvent.DRM_ERROR, onDRMError); 
        preloadConnection = new NetConnection(); 
        preloadConnection.addEventListener( 
          NetStatusEvent.NET_STATUS, onConnect); 
        preloadConnection.connect(null);  
    } 
 
    private function onConnect( event:NetStatusEvent ):void {  
        preloadMetadata(); 
    } 
 
    private function preloadMetadata():void {  
        preloadStream = new Primetime( preloadConnection ); 
        preloadStream.client = this; 
        var options:PrimetimePlayOptions = new PrimetimePlayOptions(); 
        options.streamName = videoURL; 
        preloadStream.preloadEmbeddedData( options );  
    }  
 
    public function onDRMContentData( drmMetadata:DRMContentData ):void {  
        drmContentData = drmMetadata; 
        if ( drmMetadata.authenticationMethod ==  
               AuthenticationMethod.USERNAME_AND_PASSWORD ) {  
            authenticateUser(); 
        } 
        else {  
            getVoucher(); 
        } 
    } 
 
    private function getVoucher():void {  
        drmManager.loadVoucher(  
          drmContentData,  
          LoadVoucherSetting.ALLOW_SERVER  
        ); 
    } 
 
    private function authenticateUser():void {  
        drmManager.authenticate(  
          drmContentData.serverURL,  
          drmContentData.domain,  
          userName,  
          password  
        ); 
    } 
 
    private function onAuthenticationError(  
      event:DRMAuthenticationErrorEvent ):void {  
        trace( "Authentication error: " +  
               event.errorID + ", " +  
               event.subErrorID ); 
    } 
 
    private function onAuthenticationComplete(  
      event:DRMAuthenticationCompleteEvent ):void {  
        trace( "Authenticated to: " +  
               event.serverURL + ",  
               domain: " +  
               event.domain ); 
        getVoucher(); 
    } 
 
    private function onDRMStatus( event:DRMStatusEvent ):void { 
        trace( "DRM Status: " + event.detail); 
        trace("--License allows offline playback = " +  
              event.isAvailableOffline ); 
        trace("--License already cached = " +  
              event.isLocal ); 
        trace("--License required authentication = " +  
              !event.isAnonymous ); 
    } 
 
    private function onDRMError( event:DRMErrorEvent ):void { 
        trace( "DRM error event: " +  
               event.errorID + ", " +  
               event.subErrorID + ", " +  
               event.text ); 
    } 
 
    public function onPlayStatus( info:Object ):void { 
        preloadStream.close(); 
    }  
} 
```

