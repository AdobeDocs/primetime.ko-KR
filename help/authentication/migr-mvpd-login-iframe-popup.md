---
title: iFrame에서 팝업으로 MVPD 로그인 페이지를 마이그레이션하는 방법
description: iFrame에서 팝업으로 MVPD 로그인 페이지를 마이그레이션하는 방법
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# iFrame에서 팝업으로 MVPD 로그인 페이지를 마이그레이션하는 방법 {#migr-mvpd-login-iframe-popup}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 팝업과 iFrame 비교 {#popup-vs-iframe}

일부 사용자는 MVPD 로그인 페이지의 iFrame 구현에서 타사 쿠키 문제가 발생했습니다.
<!--These issues are described in the tech notes linked below:

* [Adobe Primetime authentication and Safari login issues](https://tve.helpdocsonline.com/adobe-pass)
* [MVPD iFrame login and 3rd party cookies](https://tve.helpdocsonline.com/mvpd)-->

Adobe Primetime 인증 팀 **팝업/새 창 로그인 페이지를 구현하는 것이 좋습니다.** Firefox와 Safari의 iFrame 버전 대신  그러나 Internet Explorer에 대한 로그인 페이지를 구현하는 경우 팝업 구현에 문제가 발생할 수 있습니다. IE 문제는 사용자가 팝업 창에서 MVPD를 사용하여 인증되면 Adobe Primetime 인증이 상위 페이지 리디렉션을 강제로 수행하며, 이 리디렉션은 Internet Explorer에서 팝업 차단기로 표시됩니다. Adobe Primetime 인증 팀 **internet Explorer용 iFrame 로그인을 구현하는 것이 좋습니다.**.

이 기술 노트에 표시되는 샘플 코드는 iFrame 및 팝업의 하이브리드 구현(Internet Explorer에서 iFrame 열기 및 다른 브라우저에서 팝업)을 사용합니다.

iFrame 구현이 이미 있으므로 기술 노트의 첫 번째 부분은 iFrame 구현에 대한 코드를 나타내며 두 번째 부분에서는 팝업 구현을 기본값으로 수용하기 위한 변경 사항을 제공합니다.


## iFrame에서 로그인 페이지가 있는 MVPD 선택기 {#mvpd-pickr-iframe}

이전 코드 예는 를 포함하는 HTML 페이지를 보여줍니다 &lt;div> 태그를 사용하여 iFrame을 만들 수 있습니다.

```HTML
<body> 
    <div id="mvpddiv">
        <div style="background: red">
            <input type="button" id="btnCloseIframe" value="X" onclick="closeIframeAction();">
        </div>
        <br/>
        <!-- We use the "about:blank" value so that when the iFrame loads
             we do not see the the parent page. -->
        <iframe id="mvpdframe" name="mvpdframe" src="about:blank"></iframe>
    </div> 
</body>
```

다음은 관련 정보입니다 **JavaScript** 코드:

```JavaScript
/*
 * Callback indicating that the AccessEnabler swf has initialized
 */
function swfLoaded() {
    // AccessEnabler is loaded so we can use the API function it provides
    accessEnablerObject.setRequestor(requestorID); 
    accessEnablerObject.checkAuthentication();
} 
/*
* The code the correctly closes the opened IFrame and does not leave the
* AccessEnabler in an undefined state.
*/
function closeIframeAction () {
    accessEnablerObject.setSelectedProvider(null);
    /* We use the "about:blank" value so that when the iFrame loads
     * we do not see the the previous MVPD.
     */
    document.getElementById('mvpdframe').src="about:blank";
    document.getElementById('mvpddiv').style.visibility="hidden";
    document.getElementById('mvpddiv').style.display="none";
}
/*
* Some of the supported MVPDs require their login pages to be displayed within an iFrame.
* In your HTML page, you must include the following <div> tag: "<div id="mvpddiv"></div>".
* Called when the selected MVPD requires an iFrame in which to display its authentication UI.
*/
function createIFrame(inWidth, inHeight) {
     // Create the iFrame to the specified width and height for the auth page
    ifrm = document.createElement("IFRAME");
    ifrm.name = "mvpdframe";
    ...
    document.getElementById('mvpddiv').appendChild(ifrm);
    ...
    // Force the name into the DOM since it is still not refreshed, for IE
    window.frames["mvpdframe"].name = "mvpdframe";
}
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
    /* This is an example how previously the MVPD picker was build and will be replaced. */
}
/* 
* Sending the user selected MVPD of the custom dialog is achieved
* by calling the API function setSelectedProvider(providerID:String).
*/
function setSelectedProvider(providerID) {
    accessEnablerObject.setSelectedProvider(providerID);
}
```


## 팝업 창에서 로그인 페이지가 있는 MVPD 선택기 {#mvpd-pickr-popup}

Adobe에서는 **iFrame** 더 이상 HTML 코드에 iFrame 또는 iFrame을 닫기 위한 버튼이 포함되지 않습니다. 이전에 iFrame을 포함했던 div - **mvpddiv** - 다음 용도로 계속 사용됩니다.

* 팝업 포커스가 손실되면 MVPD 로그인 페이지가 이미 열려 있음을 사용자에게 알립니다
* 팝업에 집중할 수 있는 링크를 제공하려면

```HTML
<body onload="javascript:loadAccessEnabler();"> 
   <div id="aeHolder">
       <div name="contentAccessEnabler" id="contentAccessEnabler"></div>
   </div>
   <div id="mvpddiv">
      <p>
      <strong>No login window?</strong>
      <br/>
      <a href="javascript:mvpdWindow.focus();">Click here to open it.</a>
      <br/>
      Still not working? Check popup blockers!
      </p>
   </div> 
 
   <div id="picker" style="display:none">
      Choose MVPD: <br/>
      <select id="mvpdList" multiple></select>
      <br/>
         <a id="authenticateButton" onclick="javascript:authenticate();">Authenticate</a>
   </div>
</body>
```

MVPD 목록이 div에 표시됩니다. **선택기** 선택 **-mvpdList**.

새 API 콜백이 사용됩니다. **setConfig(configXML)**. 콜백은 setRequestor(requestorID) 함수를 호출한 후 트리거됩니다. 이 콜백은 이전에 설정한 요청자 ID와 통합된 MVPD 목록을 반환합니다. 콜백 메서드에서 들어오는 XML을 구문 분석하고 캐시된 MVPD 목록을 구문 분석합니다. MVPD 선택기도 만들어지지만 표시되지 않습니다.

```JavaScript
var mvpdList;  // The list of cached MVPDs
var mvpdWindow;  // The reference to the popup with the MVPD login page
var cancelTimer = 0;
/* Callback indicating that the AccessEnabler swf has initialized */
function swfLoaded() {
   accessEnablerObject = $('#AccessEnabler').get(0);
   // Using a custom implementation of the MVPD picker
   accessEnablerObject.setProviderDialogURL('none');
   accessEnablerObject.setRequestor(requestorID); 
}

function setConfig(configXML) {
   mvpdList = [];
   $.each($($.parseXML(configXML)).find('mvpd'), function (idx, item) {
      var mvpdId = $(item).find('id').text();
      mvpdList[mvpdId] = {
         displayName: $(item).find('displayName').text(),
         logo: $(item).find('logoUrl').text(),
         popup: $(item).find('iFrameRequired').text() == "true",
         width: $(item).find('iFrameWidth').text(),
         height: $(item).find('iFrameHeight').text()
      };

      $('#mvpdList').append($('<option value="' + mvpdId + '" title="' + mvpdId + '">' + mvpdList[mvpdId].displayName + '</option>'));
   });
   accessEnablerObject.getAuthentication();
}
```

getAuthentication() 또는 getAuthorization() 함수가 호출되면 displayProviderDialog() 콜백이 트리거됩니다. 일반적으로 이 콜백 내에서 MVPD 목록이 만들어지고 표시되었을 수 있습니다. MVPD 선택기가 이미 빌드되었으므로 남은 작업은 사용자에게 표시하는 것입니다.

```JavaScript
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
   $('#picker').show();
}
```

사용자가 선택기에서 MVPD를 선택한 후 팝업을 만들어야 합니다. 일부 브라우저에서는 팝업이 about:blank나 다른 도메인에 있는 페이지로 만들어지는 경우 팝업을 차단할 수 있습니다. 따라서 AccessEnabler가 로드된 호스트 이름에서 팝업을 여는 것이 좋습니다.

iFrame 구현에서 btnCloseIframe 단추 및 JavaScript 함수 closeIframeAction()에 의해 인증 흐름을 재설정했지만, 이제 iFrame을 장식할 수 없습니다. 따라서 팝업이 닫히는 시간(사용자가 확인하거나 인증 흐름을 종료하여)을 확인하여 동일한 동작을 수행합니다. 사용자가 팝업에 집중할 수 없는 경우 도움이 되는 코드 조각도 추가되었습니다.

```HTML
"<a href="javascript:mvpdWindow.focus();">Click here to open it.</a>".
```

createIFrame() 콜백에서 **mvpddiv** div가 표시됩니다.

```JavaScript
function createIFrame(width, height) {
   $('#mvpddiv').show();
   if (useIframeLoginStyle) {
      ...
   }
}

/* Function called when user has selected the MVPD from the picker */
function authenticate() {
   var selectedMvpd = $('#mvpdList').val()[0];
   if (mvpdList[selectedMvpd].popup) {
      mvpdWindow = window.open("http://entitlement.auth-staging.adobe.com", "mvpdframe", "width=" + mvpdList[selectedMvpd].width + ",height=" + mvpdList[selectedMvpd].height, true);
      if (!mvpdWindow) {
         // Message to user that popup blocker is not allowing the authentication process to start
      }
      //watch the mvpd popup for close
      clearInterval(cancelTimer);
      cancelTimer = setInterval(checkClosed, 200);
   }
   accessEnablerObject.setSelectedProvider(selectedMvpd);
}

function checkClosed() {
   try {
      if (mvpdWindow && mvpdWindow["closed"]) {
         clearInterval(cancelTimer);
         accessEnablerObject.setSelectedProvider(null);
         accessEnablerObject.getAuthentication();
         $('#mvpddiv').hide();
      }
   } catch (error) {
      console.log(error);
   }
}
```

>[!IMPORTANT]
>
>* 샘플 코드에는 사용된 requestorID - &#39;REF&#39;에 대해 하드코딩된 변수가 포함되어 있으며, 이 변수는 실제 프로그래머 요청자 ID로 대체해야 합니다.
>* 샘플 코드는 사용된 요청자 ID와 연결된 화이트리스트에 추가한 도메인에서만 제대로 실행됩니다.
>* 전체 코드를 다운로드할 수 있으므로 이 기술 노트에 제공된 코드가 잘렸습니다. 전체 샘플을 보려면 **JS iFrame과 팝업 샘플**.
>* 외부 JavaScript 라이브러리는 [Google 호스팅 서비스](https://developers.google.com/speed/libraries/).

