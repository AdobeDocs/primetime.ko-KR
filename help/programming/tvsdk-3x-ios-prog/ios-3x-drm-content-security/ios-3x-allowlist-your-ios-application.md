---
description: Adobe의 Machotools 도구를 사용하여 iOS 앱을 허용 목록 할 수 있습니다.
title: iOS 애플리케이션 허용 목록
exl-id: 3af75d9a-3b38-4d3c-9890-513a4abc1809
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# iOS 애플리케이션 허용 목록 {#allowlist-your-ios-application}

Adobe의 Machotools 도구를 사용하여 iOS 앱을 허용 목록 할 수 있습니다.

일반적으로 TVSDK 애플리케이션을 완료하면 Adobe Primetime DRM 명령줄 도구를 사용하여 앱을 허용 목록 할 수 있습니다.

>[!TIP]
>
>이러한 도구를 사용하여 DRM 정책을 만들고 콘텐츠를 암호화할 수도 있습니다.

앱 목록을 허용하면 보호된 콘텐츠는 비디오 플레이어에서만 재생할 수 있습니다. 그러나 iOS 애플리케이션을 나열할 수 있도록 허용하려면 Apple의 애플리케이션 제출 정책에 작동하는 특별한 절차를 완료해야 합니다.

iOS 앱을 제출하기 전에 먼저 서명하고 Apple에 게시해야 합니다.

>[!NOTE]
>
>Apple은 개발자의 서명을 제거하고 자체 인증서로 애플리케이션에 다시 서명합니다.

재서명 때문에 Apple App Store에 제출하기 전에 생성한 허용 목록 정보를 사용할 수 없습니다.

이 제출 정책으로 작업하기 위해 Adobe에서 `machotools` iOS 응용 프로그램을 지문 처리하여 다이제스트 값을 만들고 이 값에 서명한 다음 iOS 응용 프로그램에 이 값을 삽입하는 도구입니다. iOS 앱의 지문을 채취한 후 앱을 Apple App Store에 제출할 수 있습니다. 사용자가 App Store에서 앱을 실행할 때 Primetime DRM은 애플리케이션 지문의 런타임 계산을 수행하고 애플리케이션에 이전에 삽입되었던 다이제스트 값으로 확인합니다. 지문이 일치하면 앱이 허용 목록에 추가된 것으로 확인되며, 보호된 콘텐츠는 재생할 수 있습니다.

Adobe `machotools` 도구는 iOS TVSDK SDK의 [!DNL]에 포함되어 있습니다 [...]/tools/DRM] 폴더

사용 `machotools`:

1. 키 쌍을 생성합니다.

   OpenSSL과 같은 유틸리티를 사용하려면 명령 창을 열고 다음을 입력합니다.

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. 메시지가 표시되면 개인 키를 보호하기 위한 암호를 입력합니다.

   암호에는 최소 12자가 포함되어야 하며, 문자에는 대문자 및 소문자 ASCII 문자와 숫자가 혼합되어야 합니다.
1. OpenSSL을 사용하여 강력한 암호를 생성하려면 명령 창을 열고 다음을 입력합니다.

   ```shell
   openssl rand -base64 8
   ```

1. CSR(인증서 서명 요청)을 생성합니다.

   OpenSSL을 사용하여 CSR을 생성하려면 명령 창을 열고 다음을 입력합니다.

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. 인증서에 직접 서명하고 기간을 입력합니다.

   다음 예는 20년 만료를 제공합니다.

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. 자체 서명된 인증서를 PKCS#12 파일로 변환:

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   자체 서명된 인증서를 사용하여 iOS 앱에 서명할 수 있습니다.

1. PFX 파일 및 암호 위치를 업데이트합니다.
1. Xcode에서 응용 프로그램을 빌드하기 전에  **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** 실행 스크립트에 다음 명령을 추가합니다.

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. 실행 [!DNL machotools] 앱 게시자 ID 해시 값을 생성합니다.

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. 새 DRM 정책을 생성하거나 기존 정책을 업데이트하여 반환된 게시자 ID 해시 값을 포함합니다.
1. 사용 [!DNL AdobePolicyManager.jar], 반환된 게시자 ID 해시 값, 선택적 앱 ID 및 포함된 최소/최대 버전 속성을 포함하도록 새 DRM 정책(기존 정책 업데이트)을 생성합니다 [!DNL flashaccess-tools.properties] 파일.

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. 새 DRM 정책을 사용하여 콘텐츠를 패키징하고 iOS 앱에 허용 목록에 있는 콘텐츠가 재생되는지 확인합니다.
