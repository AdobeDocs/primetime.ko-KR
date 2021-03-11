---
description: Flash 런타임 TV는 애플리케이션이 있는 도메인에서 TVSDK API를 호출할 권한이 있는지 확인하기 위해 서명된 토큰이 필요합니다.
title: 서명한 토큰 로드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# 서명한 토큰 {#load-your-signed-token} 로드

Flash 런타임 TV는 애플리케이션이 있는 도메인에서 TVSDK API를 호출할 권한이 있는지 확인하기 위해 서명된 토큰이 필요합니다.

1. 각 도메인(각 도메인이 특정 도메인 또는 와일드카드 도메인일 수 있음)에 대해 Adobe 담당자로부터 서명된 토큰을 가져옵니다.

       토큰을 가져오려면 응용 프로그램을 저장 또는 로드할 도메인을 Adobe에 제공하거나, 원하는 경우 도메인을 SHA256 해시로 입력하십시오. 그 대신 Adobe은 각 도메인에 대해 서명된 토큰을 제공합니다. 이러한 토큰은 다음 양식 중 하나를 사용합니다:
   
   * 단일 도메인 또는 와일드카드 도메인의 토큰으로 작동하는 [!DNL .xml] 파일.

      >[!NOTE]
      >
      >와일드카드 도메인의 토큰은 해당 도메인과 모든 하위 도메인을 포함합니다. 예를 들어 도메인 [!DNL mycompany.com]에 대한 와일드카드 토큰은 [!DNL vids.mycompany.com] 및 [!DNL private.vids.mycompany.com];도 덮습니다.[!DNL vids.mycompany.com]의 와일드카드 토큰도 [!DNL private.vids.mycompany.com]에 포함됩니다. *와일드카드 도메인 토큰은 특정 Flash Player 버전에만 지원됩니다.*

   * 응용 프로그램이 동적으로 로드될 수 있는 다중 도메인(와일드카드를 포함하지 않음)(단일 또는 와일드카드)에 대한 토큰 정보를 포함하는 [!DNL .swf] 파일.

1. 토큰 파일을 응용 프로그램과 동일한 위치 또는 도메인에 저장합니다.

   기본적으로 TVSDK는 이 위치에서 토큰을 찾습니다. 또는 HTML 파일의 `flash_vars`에서 토큰의 이름과 위치를 지정할 수 있습니다.
1. 토큰 파일이 단일 XML 파일인 경우:
   1. `utils.AuthorizedFeaturesHelper.loadFrom`을(를) 사용하여 지정된 URL(토큰 파일)에 저장된 데이터를 다운로드하고 해당 정보에서 `authorizedFeatures` 정보를 추출합니다.

      이 단계는 다를 수 있습니다. 예를 들어 응용 프로그램을 시작하기 전에 인증을 수행하거나 CMS(Content Management System)로부터 직접 토큰을 받을 수 있습니다.

   1. TVSDK는 로드가 성공한 경우 `COMPLETED` 이벤트를 전달하거나 그렇지 않은 경우 `FAILED` 이벤트를 전달합니다. 두 이벤트 중 하나를 감지할 때 적절한 작업을 수행합니다.

      응용 프로그램에서 `MediaPlayerContext` 형식으로 필수 `authorizedFeatures` 개체를 TVSDK에 제공하려면 이 작업을 성공적으로 수행해야 합니다.
   이 예는 단일 토큰 [!DNL .xml] 파일을 사용하는 방법을 보여줍니다.

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

1. 토큰이 [!DNL .swf] 파일인 경우:
   1. `Loader` 클래스를 정의하여 [!DNL .swf] 파일을 동적으로 로드합니다.
   1. `LoaderContext`을(를) 설정하여 현재 응용 프로그램 도메인에 로드할 내용을 지정합니다. 이렇게 하면 TVSDK가 [!DNL .swf] 파일 내에서 올바른 토큰을 선택할 수 있습니다. `LoaderContext`이(가) 지정되지 않은 경우 `Loader.load`의 기본 작업은 현재 도메인의 하위 도메인에 .swf를 로드하는 것입니다.
   1. COMPLETE 이벤트를 수신합니다. TVSDK는 로드가 성공적으로 완료될 때 전달합니다.

      또한 ERROR 이벤트를 수신하고 적절한 작업을 수행합니다.
   1. 로드가 성공하면 `AuthorizedFeaturesHelper`을 사용하여 PCKS-7 인코딩 보안 데이터가 포함된 `ByteArray`을(를) 가져옵니다.

      이 데이터는 AVE V11 API를 통해 Flash 런타임 플레이어에서 인증 승인을 얻는 데 사용됩니다. 바이트 배열에 내용이 없으면 이 절차를 사용하여 단일 도메인 토큰 파일을 찾습니다.
   1. 바이트 배열에서 필요한 데이터를 가져오려면 `AuthorizedFeatureHelper.loadFeatureFromData`을 사용합니다.
   1. [!DNL .swf] 파일을 언로드합니다.

   다음 예는 다중 토큰 [!DNL .swf] 파일을 사용할 수 있는 방법을 보여줍니다.

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

