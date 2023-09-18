---
description: Flash 런타임 TVSDK에는 애플리케이션이 있는 도메인에서 TVSDK API를 호출할 권한이 있는지 확인하기 위해 서명된 토큰이 필요합니다.
title: 서명된 토큰 로드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 서명된 토큰 로드 {#load-your-signed-token}

Flash 런타임 TVSDK에는 애플리케이션이 있는 도메인에서 TVSDK API를 호출할 권한이 있는지 확인하기 위해 서명된 토큰이 필요합니다.

1. 각 도메인(각 도메인이 특정 도메인 또는 와일드카드 도메인일 수 있음)에 대해 Adobe 담당자로부터 서명된 토큰을 받습니다.

       토큰을 얻으려면 애플리케이션이 저장되거나 로드될 도메인 또는 가급적 SHA256 해시로 도메인을 Adobe에 제공하십시오. 그 대신, Adobe은 각 도메인에 대해 서명된 토큰을 제공합니다. 이러한 토큰은 다음 양식 중 하나를 사용합니다.
   
   * An [!DNL .xml] 단일 도메인 또는 와일드카드 도메인의 토큰 역할을 하는 파일입니다.

     >[!NOTE]
     >
     >와일드카드 도메인의 토큰은 해당 도메인과 모든 하위 도메인을 포함합니다. 예를 들어 도메인에 대한 와일드카드 토큰 [!DNL mycompany.com] 다음의 것도 포함한다. [!DNL vids.mycompany.com] 및 [!DNL private.vids.mycompany.com]; 와일드카드 토큰 [!DNL vids.mycompany.com] 다음의 것도 포함한다. [!DNL private.vids.mycompany.com]. *와일드카드 도메인 토큰은 특정 Flash Player 버전에 대해서만 지원됩니다.*

   * A [!DNL .swf] 애플리케이션이 동적으로 로드할 수 있는 여러 도메인(와일드카드 제외)(단일 또는 와일드카드)에 대한 토큰 정보가 포함된 파일.

1. 토큰 파일을 응용 프로그램과 동일한 위치 또는 도메인에 저장합니다.

   기본적으로 TVSDK는 이 위치에서 토큰을 찾습니다. 또는 다음에서 토큰의 이름과 위치를 지정할 수 있습니다. `flash_vars` HTML 파일에서 참조할 수 있습니다.
1. 토큰 파일이 단일 XML 파일인 경우:
   1. 사용 `utils.AuthorizedFeaturesHelper.loadFrom` 지정된 URL(토큰 파일)에 저장된 데이터를 다운로드하고 `authorizedFeatures` 정보.

      이 단계는 다를 수 있습니다. 예를 들어 애플리케이션을 시작하기 전에 인증을 수행하거나 CMS(콘텐츠 관리 시스템)에서 직접 토큰을 받을 수 있습니다.

   1. TVSDK에서 `COMPLETED` 이벤트(로드가 성공하거나 `FAILED` 그렇지 않은 경우. 두 이벤트 중 하나를 감지하면 적절한 조치를 취하십시오.

      애플리케이션이 필수 항목을 제공하려면 이 작업이 성공해야 합니다. `authorizedFeatures` 의 형식으로 TVSDK에 개체 `MediaPlayerContext`.

   이 예에서는 단일 토큰을 사용하는 방법을 보여 줍니다 [!DNL .xml] 파일.

   ```
   private function loadDirectTokenURL():void { 
       var url:String = constructAuthorizedFeatureTokenURL(); 
       _logger.debug("#onApplicationComplete Loading token from [{0}].", url); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE,  
           onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR,  
           onFeatureError); 
        _authorizedFeatureHelper.loadFrom(url); 
    }
   ```

1. 토큰이 [!DNL .swf] 파일:
   1. 정의 `Loader` 클래스를 사용하여 동적으로 [!DNL .swf] 파일.
   1. 설정 `LoaderContext` 을(를) 통해 로드가 현재 애플리케이션 도메인에 있도록 지정하여 TVSDK가 내에서 올바른 토큰을 선택할 수 있도록 합니다. [!DNL .swf] 파일. If `LoaderContext` 이(가) 지정되지 않았습니다. 기본 작업: `Loader.load` 는 현재 도메인의 자식 도메인에 .swf를 로드합니다.
   1. 로드가 성공하면 TVSDK에서 전달하는 COMPLETE 이벤트를 수신합니다.

      또한 ERROR 이벤트를 수신하고 적절한 조치를 취합니다.
   1. 로드가 성공하면 `AuthorizedFeaturesHelper` 을(를) 받으려면 `ByteArray` PCKS-7로 인코딩된 보안 데이터가 포함됩니다.

      이 데이터는 AVE V11 API를 통해 Flash 런타임 플레이어에서 인증 승인을 받는 데 사용됩니다. 바이트 배열에 콘텐츠가 없는 경우 대신 프로시저를 사용하여 단일 도메인 토큰 파일을 찾습니다.
   1. 사용 `AuthorizedFeatureHelper.loadFeatureFromData` 바이트 배열에서 필요한 데이터를 가져옵니다.
   1. 언로드 [!DNL .swf] 파일.

   다음 예는 여러 토큰을 사용할 수 있는 방법을 보여 줍니다 [!DNL .swf] 파일.

   **다중 토큰 예 1:**

   ```
   private function onApplicationComplete(event:FlexEvent):void { 
       var url:String = constructAuthorizedFeatureTokenURLFromSwf();   
       _loader = new Loader(); 
       var swfUrl:URLRequest = new URLRequest(url); 
       var loaderContext:LoaderContext =  
           new LoaderContext(false, ApplicationDomain.currentDomain, null); 
       _loader.contentLoaderInfo.addEventListener(Event.COMPLETE,  
           modEventHandler); 
       _loader.contentLoaderInfo.addEventListener(IOErrorEvent.IO_ERROR,  
           errEventHandler); 
       _loader.contentLoaderInfo.addEventListener(ProgressEvent.PROGRESS,  
           onProgressHandler); 
       _loader.uncaughtErrorEvents.addEventListener(UncaughtErrorEvent. 
           UNCAUGHT_ERROR, uncaughtEventHandler); 
       _logger.debug("# Loading token swf with context from [{0}].", url); 
       _loader.load(swfUrl, loaderContext); 
   } 
   
   private function modEventHandler(e:Event):void { 
       _logger.debug("loadSWF with domainID {0}",  
       SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
           loader.contentLoaderInfo.applicationDomain. 
           getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray = myTokens. 
           FetchToken(SecurityDomain.currentDomain.domainID); 
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           _logger.debug("token bytearry size {0}", byteArray.length); 
           _authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   ```

   **다중 토큰 예 2:**

   ```
   private function tokenSwfLoadedHandler(e:Event):void { 
       trace("loadSWF with domainID {0}", SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
         loader.contentLoaderInfo.applicationDomain. 
         getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray =  
           myTokens.FetchToken(SecurityDomain.currentDomain.domainID); 
       var myDomains:Array = ["domain.com"]; 
       if (byteArray == null || byteArray.length == 0) { 
           // check for wildcard tokens 
           if (myTokens.hasOwnProperty("FetchWildCardToken") == true) { 
               // contains wildcard domains 
               for each (var domain:String in myDomains) { 
                   byteArray = myTokens.FetchWildCardToken(domain); 
                   if (byteArray != null && byteArray.length != 0) { 
                       break; 
                   } 
               }; 
           } 
       } 
   
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           trace("token bytearry size {0}", byteArray.length); 
           authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   
   private function loadDirectTokenURL():void { 
       trace("#onApplicationComplete Loading token from [{0}].", tokenUrl); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       authorizedFeatureHelper.loadFrom(tokenUrl); 
   }
   ```
