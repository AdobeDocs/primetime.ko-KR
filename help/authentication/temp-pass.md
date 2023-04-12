---
title: 임시 통과
description: 임시 통과
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2210'
ht-degree: 0%

---


# 임시 통과 {#temp-pass}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 기능 요약 {#tempass-featur-summary}

Temp Pass를 사용하면 프로그래머가 MVPD가 있는 계정 자격 증명이 없는 사용자를 위해 보호된 콘텐츠에 임시 액세스를 제공할 수 있습니다.  Temp Pass에는 다음 기능이 포함되어 있습니다.

* 임시 패스는 다음을 포함하여 다양한 시나리오에 적용할 임시 액세스를 제공하도록 구성할 수 있습니다.
   * 프로그래머는 해당 사이트 중 하나를 매일 짧게(예: 10분 미리 보기) 제공할 수 있습니다.
   * 프로그래머는 NCAA와 같은 주요 스포츠 행사, 즉 NCAA의 3월 광기 등을 하나의 긴 프리젠테이션을 제공할 수 있습니다.
   * 프로그래머는 이전의 두 가지 시나리오를 조합하여 제공할 수 있습니다. 예를 들어, 첫 번째, 긴 보기 기간 1일, 그 다음 몇 가지 후속 일 동안 일별로 반복되는 일련의 짧은 기간이 그 다음에 옵니다.
* 프로그래머는 임시 패스의 기간(Time-To-Live 또는 TTL)을 지정합니다.
* Temp Pass는 요청자별로 작동합니다.  예를 들어, NBC는 요청자 &quot;NBCOlifics&quot;에 대해 4시간 임시 패스를 설정할 수 있습니다.
* 프로그래머는 특정 요청자에게 부여된 모든 토큰을 재설정할 수 있습니다.  Temp Pass를 구현하는 데 사용되는 &quot;임시 MVPD&quot;는 &quot;요청자별 인증&quot;을 사용하도록 설정해야 합니다.
* **임시 통과 액세스 권한은 특정 장치의 개별 사용자에게 부여됩니다**. 사용자에 대한 임시 통과 액세스가 만료되면 해당 사용자가 만료될 때까지 해당 사용자는 동일한 장치에 대한 임시 액세스를 얻을 수 없습니다 [인증 토큰](/help/authentication/glossary.md#authz-token) 이 Adobe Primetime 인증 서버에서 지워졌습니다.


>[!NOTE]
>
>임시 패스는 Premium 워크플로우 패키지의 일부입니다. 이 기능을 사용하려면 Primetime 영업 담당자에게 문의하십시오.

## 기능 세부 사항 {#tempass-featur-details}

* **보기 시간 계산 방법** - Temp Pass가 유효한 상태로 남아 있는 시간은 사용자가 Programmer의 응용 프로그램에서 콘텐츠를 보는 데 걸리는 시간과 관련이 없습니다.  Temp Pass를 통해 인증을 요청하는 초기 사용자 요청 시 초기 현재 요청 시간을 Programmer에서 지정한 TTL에 추가하여 만료 시간을 계산합니다. 이 만료 시간은 사용자의 장치 ID 및 프로그래머의 요청자 ID와 연결되며 Primetime 인증 데이터베이스에 저장됩니다. 사용자가 동일한 장치에서 Temp Pass를 사용하여 컨텐츠에 액세스하려고 할 때마다 Primetime 인증은 서버 요청 시간을 사용자의 장치 ID 및 프로그래머 ID와 연결된 만료 시간과 비교합니다. 서버 요청 시간이 만료 시간보다 작으면 인증이 부여됩니다. 그렇지 않으면 허가가 거부됩니다.
* **구성 매개 변수** - Programmer에서 임시 전달 매개 변수를 지정하여 임시 통과 규칙을 만들 수 있습니다.
   * **토큰 TTL** - MVPD에 로그인하지 않고 사용자가 볼 수 있는 시간입니다. 이 시간은 클럭 기반이며 사용자가 컨텐츠를 보고 있는지 여부를 만료합니다.
   >[!NOTE]
   >요청자 ID에는 두 개 이상의 Temp Pass 규칙이 연결되어 있을 수 없습니다.
* **인증/인증** - 임시 통과 플로우에서 MVPD를 &quot;임시 통과&quot;로 지정합니다.  Primetime 인증이 Temp Pass 흐름의 실제 MVPD와 통신하지 않으므로 &quot;Temp Pass&quot; MVPD는 모든 리소스를 허용합니다. 프로그래머는 사이트의 나머지 리소스에 대해 수행하는 것처럼 Temp Pass를 사용하여 액세스할 수 있는 리소스를 지정할 수 있습니다. 미디어 확인 프로그램 라이브러리는 평소대로 사용하여 Temp Pass 짧은 미디어 토큰을 확인하고 재생 전에 리소스 확인을 적용할 수 있습니다.
* **임시 통과 흐름에서 데이터 추적** - Temp Pass 권한 흐름 중 추적 데이터에 대한 두 가지 사항:
   * Primetime 인증에서 사용자 **sendTrackingData()** 콜백은 장치 ID의 해시입니다.
   * Temp Pass 흐름에 사용되는 MVPD ID가 &quot;Temp Pass&quot;이므로 동일한 MVPD ID가에 다시 전달됩니다 **sendTrackingData()**. 대부분의 프로그래머는 Temp Pass 지표를 실제 MVPD 지표와 다르게 처리할 가능성이 있습니다. 이를 위해서는 분석 구현에서 몇 가지 추가 작업이 필요합니다.

다음 그림은 임시 통과 플로우를 보여줍니다.

![임시 통과 흐름](assets/temp-pass-flow.png)

*그림: 임시 통과 흐름*

## 임시 통과 구현 {#implement-tempass}

Primetime 인증 측에서는 &quot;TempPass&quot;라는 의사-MVPD가 참여하는 프로그래머의 서버 구성에 추가되어 Temp Pass가 구현됩니다.  이 의사-MVPD는 프로그래머가 보호된 콘텐츠에 일시적으로 액세스를 부여하는 실제 MVPD와 같은 역할을 합니다.

프로그래머 측에서 Temp Pass는 MVPD가 인증에 사용하는 두 가지 시나리오에 대해 다음과 같이 구현됩니다.

* **프로그래머 페이지의 iFrame**. Temp Pass는 MVPD의 인증 유형에 관계없이 작동하지만 iFrame 시나리오의 경우 현재 인증 흐름을 취소하고 Temp Pass로 인증하려면 추가 단계가 필요합니다. 이러한 단계는 [iFrame 로그인](/help/authentication/temp-pass.md) 아래의 제품에서 사용할 수 있습니다.
* **MVPD 로그인 페이지로 리디렉션**. MVPD에서 인증을 시작하기 전에 임시 패스를 트리거하기 위한 UI가 표시되는 일반적인 경우에는 특별한 단계를 수행할 필요가 없습니다. 임시 패스는 일반 MVPD처럼 처리되어야 합니다.

다음은 두 구현 시나리오에 적용됩니다.

* Temp Pass 인증을 아직 요청하지 않은 사용자에 대해서만 &quot;Temp Pass&quot;가 MVPD 선택기에 표시됩니다. 쿠키에 플래그를 유지하여 후속 요청에 대한 표시를 차단할 수 있습니다. 사용자가 브라우저 캐시를 지우지 않는 한 작동합니다. 사용자가 브라우저 캐시를 지운 경우 선택기에 &quot;임시 패스&quot;가 다시 나타나고 사용자가 다시 요청할 수 있습니다. &quot;임시 통과&quot; 시간이 아직 만료되지 않은 경우에만 액세스가 허용됩니다.
* 사용자가 Temp Pass를 통해 액세스를 요청하면 Primetime 인증 서버는 인증 프로세스 동안 일반적인 SAML(Security Assertion Markup Language) 요청을 수행하지 않습니다. 대신, 인증 엔드포인트는 토큰이 장치에 유효한 동안 호출될 때마다 성공을 반환합니다.
* Temp Pass가 만료되면 Temp Pass 흐름에서 인증 토큰과 인증 토큰의 만료 날짜가 동일하므로 해당 사용자는 더 이상 인증되지 않습니다. 사용자에게 Temp Pass가 만료되었음을 설명하기 위해 프로그래머는 호출 직후 선택한 MVPD를 검색해야 합니다 `setRequestor()`, 그런 다음 를 호출합니다. `checkAuthentication()` 평소대로 에서 `setAuthenticationStatus()` callback 인증 상태가 0인지 확인하기 위해 검사를 수행할 수 있습니다. 따라서 선택한 MVPD가 &quot;TempPass&quot;인 경우 사용자에게 Temp Pass 세션이 만료되었음을 알리는 메시지를 표시할 수 있습니다.
* 사용자가 만료 전에 Temp Pass 토큰을 삭제하는 경우, 후속 권한 검사는 TTL이 나머지 시간과 같은 토큰을 생성합니다.
* 사용자가 만료 후 임시 통과 토큰을 삭제하면 후속 권한 검사는 &quot;사용자가 승인되지 않음&quot;을 반환합니다.

의 샘플을 참조하십시오. [샘플 코드](/help/authentication/temp-pass.md#tempass-sample-code) 이 섹션에 설명된 구현 세부 사항을 코딩하는 방법에 대한 예는 아래에 나와 있습니다.

## 샘플 코드 {#tempass-sample-code}

아래 섹션에서는 Primetime 인증 API를 호출하여 Temp Pass 흐름을 구현하는 방법을 보여줍니다.

* [iFrame 로그인 샘플](/help/authentication/temp-pass.md#iframe-login-sample)
* [자동 로그인 샘플](/help/authentication/temp-pass.md#auto-login-sample)

### iFrame 로그인 샘플 {#iframe-login-sample}

다음 예에서는 MVPD가 iFrame 통합을 지원하는 경우에 대해 Temp Pass를 구현하는 방법을 보여줍니다.

```HTML
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
        "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript" src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var ae, ifrm, providersMenu, previousSelectedProvider;
        var tempassSelected = false;
 
        $(document).ready(function() {
            ifrm = $('#ifrm');
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {wmode: "transparent", allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded() {
            ae = $('#accessEnabler')[0];
            ae.setProviderDialogURL("none");
            ae.setRequestor("sample_requestor_Id");
            previousSelectedProvider = ae.getSelectedProvider(); 
            ae.checkAuthentication();
        }
 
        function createIFrame() {
            providersMenu.hide();
 
            // If the user already used TempPass once, hide the button
            if ($.cookie("TPSelected") == "1"){
                $('#tempassBtn').hide();
            }
            ifrm.show();
        }
 
        function displayProviderDialog(providers) {
            if (tempassSelected) {
                // Remember in a cookie that the user selected temp pass
                $.cookie("TPSelected", "1", {expires: 366, path: '/'});
 
                // Authenticate with temp pass
                ae.setSelectedProvider("TempPass");
            } else {
                $('#loginBtn').hide();
                providersMenu = $('<select></select>');
 
                providersMenu.change(function(event){
                    ae.setSelectedProvider(event.target.value);
                });
 
                $.each(providers, function(k, v) {
                    // Add the MVPDs to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if(v.ID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:v.ID}).text(v.displayName));                       
                    }
                });
                $('body').append(providersMenu);
            }
        }
 
        function setAuthenticationStatus(status, code) {
            loginBtn = $('#loginBtn');
            logoutBtn = $('#logoutBtn');
            console.log(previousSelectedProvider);
 
            if (status == 1) {
                $('#selectedProvider').text("Authenticated with " + ae.getSelectedProvider().MVPD + "   ");
                loginBtn.hide();
                logoutBtn.show();
 
                // Get authorization
                ae.getAuthorization("sample_requestor_Id");
            } else {
                // If selected provider is TempPass but the user is not authenticated,
                //   infer that the TempPass period has expired, so reset the MVPD selection
                if (previousSelectedProvider && previousSelectedProvider.MVPD == "TempPass") {
                    previousSelectedProvider = null;
                    ae.setSelectedProvider(null);
                    alert("Your Temp Pass has expired, please login with your regular cable provider!");
                }
                loginBtn.show();
                logoutBtn.hide();
            }
        }
 
        function selectTempPass() {
            ifrm.hide();
 
            // Signal the fact that the user selected temp pass
            tempassSelected = true;
 
            // Cancel the current authentication flow
            ae.setSelectedProvider(null);
 
            // Retry authentication
            ae.getAuthentication();
 
        }
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="ae.getAuthentication();">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
           style="display: none" onclick="ae.logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px; width: 400px; height: 400px; border: 2px solid red;">
        <button id="tempassBtn"
           onclick="selectTempPass();"
             style="float:left">Don't know your credentials? Click here to get a Temp Pass.
        </button>
        <button onclick="window.location.reload()" style="float:right">X</button>
        <br />
        <hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="90%" height="90%" frameborder="0"></iframe>
    </div>
    <br/>
    <div id="ae" style="display: none">
        <p>Loading Access Enabler...</p>
    </div>
</body>
</html>
```

#### iFrame 로그인 사용 사례 {#iframe-login-use-cases}

**처음 임시 패스를 요청하려면 다음을 수행합니다.**

1. 사용자가 프로그래머 페이지에 액세스하여 로그인 링크를 클릭합니다.
1. MVPD 선택기가 열리고 사용자가 목록에서 MVPD를 선택합니다.
1. 인증 iFrame이 표시됩니다. 이 iFrame에는 &quot;임시 통과&quot; 링크가 포함되어 있습니다.
1. 사용자가 &quot;임시 통과&quot;를 클릭하므로 Programmer는 쿠키에 플래그를 추가하여 사용자가 페이지의 후속 방문 시 &quot;임시 통과&quot; 링크를 볼 수 없도록 합니다.
1. Temp Pass 인증 요청이 Primetime 인증 서버에 도달하고 인증 토큰을 생성합니다. TTL은 Programmer가 임시 패스에 대해 설정한 기간과 같습니다.
1. Temp Pass 인증 요청이 Primetime 인증 서버에 도달합니다.
1. Primetime 인증 서버는 요청에서 장치 및 요청자 ID를 추출하고 만료 시간과 함께 데이터베이스에 저장합니다. 만료 시간은 다음과 같이 계산됩니다. 초기 Temp Pass 요청 시간에 TTL(Programmer에서 지정)을 더한 값입니다.
1. Primetime 인증 서버는 인증 토큰을 생성합니다.
1. 사용자는 보호된 콘텐츠에 액세스합니다.

**재방문 Temp Pass 사용자가 브라우저 쿠키를 삭제한 후 Temp Pass를 다시 요청하려면:**

1. 사용자가 프로그래머 페이지에 액세스하여 로그인 링크를 클릭합니다.
1. MVPD 선택기가 열리고 사용자가 목록에서 MVPD를 선택합니다.
1. 인증 iFrame이 표시됩니다. 이 iFrame에 &quot;Temp Pass&quot; 링크가 포함되어 있습니다(사용자가 원래 쿠키를 삭제했으므로 사용자가 &quot;Temp Pass&quot; 링크를 이전에 클릭했는지 여부를 Programmer가 알지 못합니다.)
1. 사용자가 &quot;임시 통과&quot;를 다시 클릭하면 프로그래머가 쿠키에 다시 플래그를 추가하여 사용자가 페이지의 후속 방문 시 &quot;임시 통과&quot; 링크를 볼 수 없도록 합니다.
1. Temp Pass 인증 요청이 인증 토큰을 생성하는 Primetime 인증 서버에 도달합니다. 이제 TTL이 Temp Pass의 나머지 시간(현재 시간과 장치 ID와 연관된 만료 시간 간의 차이)입니다.
1. Temp Pass 인증 요청이 Primetime 인증 서버에 도달합니다.
1. Primetime 인증 서버는 요청에서 장치 및 요청자 ID를 추출하여 Primetime 인증 데이터베이스에서 만료 시간을 검색하는 데 사용합니다. 현재 시간은 만료 시간과 비교됩니다.
1. 사용자의 Temp Pass가 만료되지 않은 경우 Primetime 인증 서버는 인증 토큰을 생성합니다.
1. 사용자의 Temp Pass가 만료되지 않은 경우 사용자는 보호된 콘텐츠에 액세스할 수 있습니다.

### 자동 로그인 샘플 {#auto-login-sample}

다음 샘플은 사이트를 방문할 때 사용자가 TempPass로 자동으로 로그인하는 사례를 보여줍니다. 사용자는 언제든지 일반 MVPD로 로그인하도록 선택할 수 있으며 TempPass가 만료된 경우 경고됩니다.

```HTML
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript"
             src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript"
             src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript"
             src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var REQUESTOR = "REF";
        var RESOURCE = "sample_requestor_Id";
        var selectedProvider = null;
        var mvpds;
        var hasTempPassMVPD = false;
 
        // Used to cache the mvpd picker
        var picker;
 
        $(document).ready(function() {
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded(){
            console.log("AccessEnabler loaded");
            ae = $('#accessEnabler')[0];
 
            // Make sure the default picker is disabled
            ae.setProviderDialogURL("none");
 
            ae.setRequestor(REQUESTOR);
            ae.checkAuthentication();
        }
 
        /**
         * Callback received as a result of setRequestor()
         *
         * @param xml object holding the configuration for the current REQUESTOR
         * including the MVPD list
         */
        function setConfig(config) {
            // Save the mvpd list
            var mvpdList = $.parseXML(config);
            mvpds = $(mvpdList).find('mvpd');
 
            // Create the picker only once and cache it
            if(!picker) {
                picker = $('<div id="mvpdPicker"/>');
 
                var providersMenu = $('<select id="mvpdList" multiple></select>');
 
                $.each(mvpds, function(k, v) {
                    var mvpdID = $(v).find("id").text();
                    var mvpdName = $(v).find("displayName").text();
 
                    // Add the mvpd's to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if (mvpdID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:mvpdID}).text(mvpdName));
                    } else {
                        hasTempPassMVPD = true;
                    }
                });
                picker.append(providersMenu);
                picker.append($('<br/>'));
                picker.append($('<input type="button" onclick="login()" value="login" />'));
                picker.append($('<input type="button" onclick="cancelPicker()" value="cancel" />'));                  
            }
 
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");             
            }
        }
 
        /**
         * Callback triggered for iFramed MVPD's
         */
        function createIFrame() {
            $('#mvpdPicker').remove();
            $('#ifrm').show();
        }
 
        /**
         * Hides the MVPD picker
         * when the user clicks "Cancel"
         */
        function cancelPicker() {
            $('#video').show();
            $('#mvpdPicker').remove();
            $('#loginBtn').show();
        }
 
        /**
         * Pops up the MVPD picker
         */
        function showPicker() {
            $('#video').hide();
            $('#loginBtn').hide();
            $('body').append(picker);
        }
 
        function logout() {
            $.removeCookie('tempPassUsed');
            ae.logout();
        }
 
        /**
         * Performs login with the selected MVPD
         */
        function login() {
            selectedProvider = $('#mvpdList').val()[0];
 
            // Make sure we clear out previously
            // selected. This is a must if we want to force
            // login with a real MVPD while still logged in with
            // TempPass, without doing an ae.logout()
            ae.setSelectedProvider(null);
            ae.getAuthentication();
        }

        /**
         * Callback triggered by AccessEnabler. This is usually
         * triggered in order to display the MVPD picker, but
         * since we already constructed, cached, and displayed the
         * picker, and the user already picked the MVPD, we don't need
         * to do anything here but state management
         */
        function displayProviderDialog() {
            // If the selected MVPD is TempPass
            // store this fact in a cookie,
            // otherwise clear it
            if (selectedProvider != 'TempPass') {
                $.removeCookie('tempPassUsed');
            } else {
                $.cookie("tempPassUsed", 1);
            }
 
            // Since the picker was already shown
            // and the user picked an MVPD,
            // just proceed to login
            ae.setSelectedProvider(selectedProvider);
        }
 
        function setAuthenticationStatus(status, code) {
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");
            } else if(status == 1) {
                selectedProvider = ae.getSelectedProvider().MVPD;
                $('#selectedProvider').text("Authenticated with " + selectedProvider + "   ");
 
                // If authenticated with TempPass
                // allow the user to login with
                // a real MVPD
                if (selectedProvider == "TempPass") {
                    $('#loginBtn').show();
                    $('#logoutBtn').hide();
                } else {
                    $('#loginBtn').hide();
                    $('#logoutBtn').show();
                }
 
                // Get authorization
                // Note: This is mandatory in order to "start" the temp pass countdown
                ae.checkAuthorization(RESOURCE);
            } else if(code != "Provider not Selected Error") {
                // Auto-authenticate with TempPass only if we infer
                // that TempPass has not expired, otherwise we
                // inform the user that TempPass has expired
                if ($.cookie('tempPassUsed') == 1) {
                   $('#selectedProvider').text("Your Temp Pass has expired, please log in with your cable provider!");
                   $('#logoutBtn').show();
                   showPicker();
                } else {
                    selectedProvider = 'TempPass';
                    ae.getAuthentication();
                }
            }
        }
 
        /**
         * Displays the picker as a result
         * of user action
         */
        function loginClicked() {
            $('#loginBtn').hide();
            showPicker();
        }
 
        /**
         * Callback triggered in case of authorization success
         */
        function setToken(token) {
            console.log(token);
            $('#video').html('<img src=">');
        }
 
        /**
         * Callback triggered in case of authz failure
         */
        function tokenRequestFailed(resource, status, message) {
            console.log(resource);
            $('#video').html('<p style="color: red">' + status + ': ' + message + '</p>');
        }
 
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="loginClicked()">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
        style="display: none" onclick="logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px;
         width: 400px; height: 400px; border: 2px solid red;">
        <button onclick="window.location.reload()" style="float:right">Close this window</button>
        <br /><hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="80%" height="80%" frameborder="0"></iframe>  
    </div>
    <br/>
 
    <div id="video"></div>
    <div id="ae" style="display: none"><p>Loading Access Enabler...</p></div>
</body>
</html>
```

## 복수 임시 가공 패스 사용 {#use-mult-tempass}

특정 이벤트에는 초기 무료 액세스 간격(예: 4시간), 일별 무료 액세스(예: 다음 날 10분) 등 콘텐츠에 대한 단계별 무료 액세스 권한이 필요합니다.  프로그래머가 이 시나리오를 구현하려면 Adobe 연락처와 해당 시나리오를 정렬하여 프로그래머용 두 개의 임시 MVPD를 구성해야 합니다.

이 예제 시나리오(초기 4시간 무료 세션, 일별 10분 무료 세션)의 경우 Adobe은 TempPass1이라는 MVPD를 4시간의 TTL(Time-To-Live)로 구성하고, 다음 기간 동안 TTL이 10분의 TempPass2를 구성합니다.  이 두 항목은 모두 프로그래머의 요청자 ID와 연결됩니다.

### 프로그래머 구현 {#mult-tempass-prog-impl}

Adobe이 두 TempPass 인스턴스를 구성한 후 두 개의 추가 MVPD(TempPass1 및 TempPass2)가 프로그래머의 MVPD 목록에 나타납니다.  프로그래머는 여러 임시 가공 패스를 구현하려면 다음 단계를 수행해야 합니다.

1. 사용자가 사이트를 처음 방문할 때 자동으로 TempPass1로 로그인합니다. 이 작업의 시작점으로 위의 자동 예제 를 사용할 수 있습니다.
1. TempPass1이 만료되었음을 감지하면 팩트(쿠키/로컬 저장소)를 저장하고 표준 MVPD 선택기를 사용하여 사용자에게 표시합니다. **해당 목록에서 TempPass1 및 TempPass2를 필터링해야 합니다**.
1. TempPass1이 만료된 경우 각 후속 날에 TempPass2를 사용하여 해당 사용자를 자동으로 생성합니다.
1. TempPass2가 만료되면 그 날의 팩트(쿠키/로컬 저장소)를 저장하고 표준 MVPD 선택기를 사용하여 사용자에게 표시합니다. 다시, 해당 목록에서 TempPass1 및 TempPass2를 필터링해야 합니다.
1. 각각의 새로운 날에, 00:00시간에, 를 사용하여 TempPass2에 대한 모든 임시 패스를 재설정합니다. [TempPass 웹 API 재설정](/help/authentication/temp-pass.md#reset-all-tempass).

>[!NOTE]
>**프로그래밍 참고:** Primetime 인증에는 10분이 지난 후 무료 스트리밍을 중지하는 기본 메커니즘이 없습니다.  TempPass2가 만료되면 액세스를 제한하는 것은 프로그래머에게 달려 있습니다. 이를 위해 프로그래머는 X분마다 사이트/앱에서 &quot;checkAuthorization&quot; 호출을 구현할 수 있습니다. 여기서 X는 프로그래머가 앱에 대해 적절하다고 결정하는 기간입니다.

## 모든 임시 패스 재설정 {#reset-all-tempass}

특정 비즈니스 규칙에서는 Temp Pass를 정기적으로 제거하거나 특정 요청자 ID 및 MVPD ID에 대해 발급된 모든 임시 가공 패스를 임시 재설정해야 합니다. 이 기능은 다음과 같은 사용 사례를 지원합니다.

* 매일 10분 임시 패스(임시 패스는 시작 시 재설정되어야 함)
* 최신 뉴스 중에 모든 사용자가 사용할 수 있는 임시 패스입니다. (최신 뉴스가 시작하는 즉시 모든 장치에 대해 Temp Pass를 재설정해야 합니다.)
* 일부 길이의 초기 보기 기간과 다른 길이의 후속 일별 기간의 조합을 제공하는 복수 임시 전달 시나리오와,

모든 임시 패스를 재설정하기 위해 Primetime 인증에서는 프로그래머에게 *공용* 웹 API:

```url
DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset
```

>[!NOTE]
>위의 URL은 이전 재설정 API를 대체합니다. 이전 재설정 API(v1)는 더 이상 지원되지 않습니다.

* **프로토콜:** HTTPS
* **호스트:**
   * 릴리스 - mgmt.auth.adobe.com
   * Prequal - mgmt-prequal.auth.adobe.com
* **경로:** /reset-tempass/v2/reset
* **쿼리 매개 변수:** `device_id=all&requestor_id=REQUESTOR_ID&mvpd_id=TEMPPASS_MVPD_ID`
* **머리글:** ApiKey - 1232293681726481
* **응답:**
   * 성공 - HTTP 204
   * 실패:
      * 잘못된 요청에 대한 HTTP 400
      * ApiKey가 지정되지 않은 경우 HTTP 401
      * ApiKey가 잘못된 경우 HTTP 403

예:

```curl
$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"
```

## 지원되는 클라이언트 {#supp-clients}

플랫폼별 임시 패스 및 재설정 도구 지원:

| Adobe Primetime 인증 클라이언트 | 임시 통과 | 재설정 도구 |
|:--------------------------------------:|:---------:|:----------:|
| JS AccessEnabler | 예 | 예 |
| 기본 클라이언트 iOS | 예 | 예 |
| 기본 클라이언트 tvOS | 예 | 예 |
| 기본 클라이언트 Android | 예 | 예 |
| 기본 클라이언트 fireTV | 예 | 예 |
| Clientless API | 예 | 예 |

## 제한 사항 및 알려진 문제 {#limitations}

이 섹션에서는 현재 Temp Pass 구현에 적용되는 제한 사항에 대해 설명합니다.

**JavaScript SDK**: 버전에서 임시 통과 기능 재설정 **3.X 이상**.

<!--For Customers migrating from the 2.X JavaScript AccessEnabler to the 3.X JavaScript AccessEnabler, see [AccessEnabler JS 2.x to JS 3.x migration guide](https://tve.helpdocsonline.com/accessenabler-js-to-js-migration-guide).-->