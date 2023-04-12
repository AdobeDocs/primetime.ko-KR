---
title: iOS/tvOS 애플리케이션 등록
description: iOS/tvOS 애플리케이션 등록
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# iOS/tvOS 애플리케이션 등록 {#iostvos-application-registration}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#Intro}

iOS/tvOS AccessEnabler SDK 버전 3.0부터 Adobe 서버를 사용하는 인증 메커니즘을 변경하고 있습니다. Adobe는 공개 키와 암호 시스템을 사용하여 requestorID에 서명하는 대신 SDK가 서버에 수행하는 모든 호출에 대해 나중에 사용되는 액세스 토큰을 가져오는 데 사용할 수 있는 Software 문 문자열의 개념을 소개합니다. 소프트웨어 문 외에 애플리케이션에 사용자 지정 URL 체계도 필요합니다.

자세한 내용은 [동적 클라이언트 등록](/help/authentication/dynamic-client-registration.md)

## 소프트웨어 설명서란 무엇입니까? {#Soft_state}

Software Statement는 애플리케이션에 대한 정보가 포함된 JWT 토큰입니다. 모든 응용 프로그램에는 서버에서 Adobe 시스템에서 응용 프로그램을 식별하는 데 사용하는 고유한 소프트웨어 설명이 있어야 합니다. AccessEnabler SDK를 초기화할 때 Software Statement를 전달해야 하며 이 Software Statement를 사용하여 Adobe에 애플리케이션을 등록합니다. 등록 시 SDK는 액세스 토큰을 가져오는 데 사용되는 클라이언트 ID와 클라이언트 암호를 수신합니다. SDK가 서버에 수행하는 모든 호출에는 유효한 액세스 토큰이 필요합니다. SDK는 애플리케이션 등록, 액세스 토큰을 가져오고 새로 고칠 책임이 있습니다.

**참고:** Software Statement는 앱에 따라 다르며 둘 이상의 응용 프로그램에서 동일한 소프트웨어 문을 사용할 수 없습니다. 프로그래머 수준 소프트웨어 명령문은 또한 동일한(즉, 단일 채널 또는 다중 채널) 애플리케이션에만 사용할 수 있습니다. 이 제한은 사용자 지정 구성표에도 적용됩니다.

## 소프트웨어 명세서를 얻는 방법 {#obtain}

### Adobe의 TVE 대시보드에 액세스할 수 있는 경우:

- 브라우저를 열고 다음 위치로 이동합니다. <https://console.auth.adobe.com>
- 다음으로 이동 `Channels` 섹션을 선택하고 채널을 선택합니다.
- 다음으로 이동 `Registered Applications` 탭.
- 클릭 `Add new application`.
- 애플리케이션의 이름과 버전을 제공하고 사용 가능한 플랫폼을 선택합니다. 이 예제에서는 iOS/tvOS를 사용합니다.
- 변경 사항을 서버에 푸시한 다음 채널의 등록된 애플리케이션 탭으로 다시 이동합니다.
- 등록된 모든 응용 프로그램이 있는 목록이 표시됩니다. 을(를) 클릭합니다.   `Download` 방금 만든 애플리케이션의 단추. 소프트웨어를 다운로드할 준비가 되기 전에 몇 분 정도 기다려야 할 수 있습니다.
- 텍스트 파일이 다운로드됩니다. 소프트웨어 설명서로 컨텐츠를 사용합니다.

자세한 내용은 다음을 참조하십시오. [동적 클라이언트 등록 관리](/help/authentication/dynamic-client-registration-management.md).

### Adobe의 TVE 대시보드에 액세스할 수 없는 경우:

다음 위치에 티켓 제출 <tve-support@adobe.com>. 채널, 애플리케이션 이름, 버전 및 플랫폼과 같은 필요한 모든 정보를 포함하십시오. 지원 팀의 누군가가 귀하를 위해 소프트웨어 설명을 작성하겠습니다.

## 소프트웨어 명세서를 사용하는 방법 {#use}

소프트웨어 구문을 얻은 후에는 Access Enabler 생성자에서 매개 변수로 전달해야 합니다. 원격 위치에서 소프트웨어 구문을 호스팅하는 것이 좋습니다. 이렇게 하면 새로운 버전의 애플리케이션을 출시하지 않고도 소프트웨어 구문을 쉽게 취소하고 변경할 수 있습니다.

## 애플리케이션의 사용자 지정 URL 체계 생성 {#generating}

### Adobe의 TVE 대시보드에 액세스할 수 있는 경우:

- 브라우저를 열고 다음 위치로 이동합니다. <https://console.auth.adobe.com>
- 다음으로 이동 `Channels` 섹션을 선택하고 채널을 선택합니다.
- 다음으로 이동 `Custom Schemes` 탭.
- 클릭 `Generate a new custom scheme`.
- 애플리케이션에 대해 새로운 사용자 지정 구성표가 생성됩니다. 예: `adbe.1JqxQsYhQOCIrwPjaooY8w://`
- 변경 사항을 서버에 푸시합니다.

### Adobe의 TVE 대시보드에 액세스할 수 없는 경우:

다음 위치에 티켓 제출 <tve-support@adobe.com>. 채널 ID를 포함하십시오. 그러면 지원 팀의 누군가가 사용자 지정 구성표를 만듭니다.

## 사용자 지정 체계를 사용하는 방법 {#use_custom}

애플리케이션의 `info.plist` 파일에 다음 코드를 추가합니다.

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>adbe.u-XFXJeTSDuJiIQs0HVRAg</string> // replace this with your custom scheme
            </array>
        </dict>
    </array>
```
