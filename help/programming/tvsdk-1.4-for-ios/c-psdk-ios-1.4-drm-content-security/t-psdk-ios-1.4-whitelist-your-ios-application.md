---
description: Adobe의 machotools 도구를 사용하여 iOS 앱을 화이트리스트할 수 있습니다.
seo-description: Adobe의 machotools 도구를 사용하여 iOS 앱을 화이트리스트할 수 있습니다.
seo-title: iOS 애플리케이션 화이트리스트
title: iOS 애플리케이션 화이트리스트
uuid: 52ce1dd7-5f10-418e-9916-cec60eae874e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# iOS 애플리케이션 화이트리스트{#whitelist-your-ios-application}

Adobe의 machotools 도구를 사용하여 iOS 앱을 화이트리스트할 수 있습니다.

일반적으로 TVSDK 애플리케이션을 완료하면 Adobe Primetime DRM 명령줄 툴을 사용하여 앱을 화이트리스트에 추가할 수 있습니다.

>[!TIP]
>
>이러한 도구를 사용하여 DRM 정책을 만들고 내용을 암호화할 수도 있습니다.

앱을 화이트리스트에 추가하면 보호된 콘텐츠를 비디오 플레이어에서만 재생할 수 있습니다. 그러나 iOS 애플리케이션을 화이트리스트에 게시하려면 Apple의 애플리케이션 제출 정책과 작동하는 특별 절차를 완료해야 합니다.

iOS 앱을 제출하기 전에 앱을 서명하여 Apple에 게시해야 합니다.

>[!NOTE]
>
>Apple은 개발자 서명을 제거하고 자체 인증서를 사용하여 응용 프로그램에 다시 서명합니다.

다시 서명하기 때문에 Apple App Store에 제출하기 전에 생성된 화이트 리스트 정보는 사용할 수 없습니다.

Adobe는 이 제출 정책을 수행하기 위해 iOS 응용 프로그램의 지문을 사용하여 다이제스트 값을 만들고 이 값에 서명하고 iOS 응용 프로그램에서 이 값을 주입하는 `machotools` 도구를 만들었습니다. iOS 앱을 지문한 후 Apple App Store에 앱을 제출할 수 있습니다. 사용자가 App Store에서 앱을 실행할 때 Primetime DRM은 애플리케이션 지문을 런타임 계산하여 이전에 애플리케이션에 삽입된 다이제스트 값으로 확인합니다. 지문과 일치하는 경우 앱이 화이트리스트에 포함되고 보호된 콘텐츠가 재생되도록 허용됩니다.

Adobe `machotools` 도구는 [!DNL...]의 iOS TVSDK SDK에 포함되어 [있습니다.]/tools/DRM] 폴더를 참조하십시오.

사용 방법 `machotools`:

1. 키 쌍을 생성합니다.

   OpenSSL과 같은 유틸리티를 사용하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. 메시지가 표시되면 암호를 입력하여 개인 키를 보호합니다.

   암호는 12자 이상이어야 하며 대문자와 소문자를 혼합하여 사용해야 합니다.
1. OpenSSL을 사용하여 강력한 암호를 생성하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl rand -base64 8
   ```

1. CSR 파섹

   OpenSSL을 사용하여 CSR을 생성하려면 명령 창을 열고 다음을 입력합니다.

   ```
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. 인증서를 직접 서명하고 원하는 기간을 입력합니다.

   다음 예에서는 20년 만료를 제공합니다.

   ```
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. 자체 서명된 인증서를 PKCS#12 파일로 변환합니다.

   ```
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   자체 서명된 인증서를 사용하여 iOS 앱에 서명할 수 있습니다.

1. PFX 파일 및 암호 위치를 업데이트합니다.
1. Xcode에서 애플리케이션을 제작하기 전에 **[!UICONTROL Build Phases]** >에서 다음 명령을 실행 스크립트에 **[!UICONTROL Run Script]** 추가합니다.

   ```
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. 앱 게시자 ID 해시 값을 [!DNL machotools] 생성하기 위해 실행합니다.

   ```
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. 새 DRM 정책을 만들거나 반환된 게시자 ID 해시 값을 포함하도록 기존 정책을 업데이트합니다.
1. 을 [!DNL AdobePolicyManager.jar]사용하여 새 DRM 정책(기존 정책 업데이트)을 만들어 반환된 게시자 ID 해시 값, 선택적 앱 ID, 포함된 [!DNL flashaccess-tools.properties] 파일에 최소 및 최대 버전 속성을 포함합니다.

   ```
   java -jar libs/AdobePolicyManager.jar new app_whitelist.pol
   ```

1. 새로운 DRM 정책을 사용하여 컨텐츠를 패키지하고 iOS 앱에서 화이트리스트 컨텐츠 재생을 확인합니다.

