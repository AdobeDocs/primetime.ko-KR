---
seo-title: 인증 UI 만들기
title: 인증 UI 만들기
uuid: 4744bac0-c36e-4b0a-b3fb-d81c7f2e7617
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 인증 UI 만들기 {#create-an-authentication-ui}

1. 사용자 인증 자격 증명을 검색할 사용자 인터페이스를 만듭니다.

   다음은 사용자 자격 증명을 검색하기 위한 간단한 유저 인터페이스의 Flex 예입니다. 이 패널은 각 사용자 이름과 암호 자격 증명에 대해 하나씩, 두 개의 `TextInput` 개체가 포함된 패널 개체로 구성됩니다. 패널에는 `credentials()` 메서드를 실행하는 단추도 포함되어 있습니다.

   ```xml
   <mx:Panel x="236.5"  
             y="113"  
             width="325"  
             height="204"  
             layout="absolute"  
             title="Login">  
       <mx:TextInput x="110"  
                     y="46"  
                     id="uName"/>  
       <mx:TextInput x="110"  
                     y="76"  
                     id="pWord"  
                     displayAsPassword="true"/>  
       <mx:Text x="35"  
                y="48"  
                text="Username:"/>  
       <mx:Text x="35"  
                y="78"  
                text="Password:"/>  
       <mx:Button x="120"  
                  y="115"  
                  label="Login"  
                  click="credentials()"/>  
   </mx:Panel>  
   ```

1. 사용자 제공 인증 값을 처리하는 `credentials()` 방법을 작성합니다.

   이 `credentials()` 메서드는 사용자 이름과 암호 값을 `setDRMAuthenticationCredentials()` 메서드에 전달하는 사용자 정의 메서드입니다. 값이 전달되면 `credentials()` 메서드는 `TextInput` 객체의 값을 재설정합니다.

   ```
   <mx:Script> 
       <![CDATA[ 
         public function credentials():void { 
             videoStream.setDRMAuthenticationCredentials(uName, pWord, "drm"); 
             uName.text = ""; 
             pWord.text = ""; 
   } ]]> 
   </mx:Script> 
   ```

   이러한 유형의 간단한 인터페이스를 구현하는 한 가지 방법은 패널을 새 상태의 일부로 포함하는 것입니다. 새 상태는 `DRMAuthenticateEvent` 개체가 throw될 때 기본 상태에서 만들어집니다. 다음 예에는 보호된 비디오 파일을 가리키는 소스 특성이 있는 `VideoDisplay` 개체가 포함되어 있습니다. 이 경우 `credentials()` 메서드가 응용 프로그램을 기본 상태로 반환하도록 수정되었습니다. 이 메서드는 사용자 자격 증명을 전달하고 TextInput 개체 값을 재설정한 후에 사용됩니다.

   ```xml
   <?xml version="1.0" encoding="utf-8"?> 
   <mx:WindowedApplication xmlns:mx="https://www.adobe.com/2006/mxml" 
       layout="absolute" 
       width="800" 
       height="500" 
       title="DRM FLV Player" 
       creationComplete="initApp()" > 
       <mx:states> 
           <mx:State name="LOGIN"> 
               <mx:AddChild position="lastChild"> 
                       <mx:Panel x="236.5"  
                                 y="113"  
                                 width="325"  
                                 height="204"  
                                 layout="absolute"  
                                 title="Login"> 
                       <mx:TextInput x="110"  
                                     y="46"  
                                     id="uName"/> 
                       <mx:TextInput x="110"  
                                     y="76"  
                                     id="pWord"  
                                     displayAsPassword="true"/> 
                       <mx:Text x="35"  
                                y="48"  
                                text="Username:"/> 
                       <mx:Text x="35"  
                                y="78"  
                                text="Password:"/> 
                       <mx:Button x="120"  
                                  y="115"  
                                  label="Login"  
                                  click="credentials()"/> 
                       <mx:Button x="193"  
                                  y="115"  
                                  label="Reset"  
                                  click="uName.text=''; 
               </mx:Panel> 
           </mx:AddChild> 
       </mx:State> 
   </mx:states> 
   pWord.text='';"/> 
   
   <mx:Script> 
       <![CDATA[ 
           import flash.events.DRMAuthenticateEvent; 
           private function initApp():void { 
               videoStream.addEventListener(DRMAuthenticateEvent.DRM_AUTHENTICATE, 
                                            drmAuthenticateEventHandler); 
           } 
           public function credentials():void { 
               videoStream.setDRMAuthenticationCredentials(uName, pWord, "drm"); 
               uName.text = ""; 
               pWord.text = ""; 
               currentState=''; 
           } 
           private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void { 
               currentState='LOGIN'; 
           } 
       ]]> 
   </mx:Script> 
   <mx:VideoDisplay id="video"  
                    x="50"  
                    y="25"  
                    width="700"  
                    height="350" 
                    autoPlay="true" 
                    bufferTime="10.0" 
                    source="https://www.example.com/flv/Video.flv" /> 
   </mx:WindowedApplication> 
   ```

