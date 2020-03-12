---
seo-title: 사전 요구 사항 소프트웨어 다운로드 및 구성
title: 사전 요구 사항 소프트웨어 다운로드 및 구성
description: 설치 프로세스는 간단합니다. 시스템에 JDK가 이미 설치되어 있는 경우 이 단계를 건너뛸 수 있지만 JDK, Eclipse IDE 및 OS가 호환되어야 합니다.
seo-description: 설치 프로세스는 간단합니다. 시스템에 JDK가 이미 설치되어 있는 경우 이 단계를 건너뛸 수 있지만 JDK, Eclipse IDE 및 OS가 호환되어야 합니다.
uuid: ca29144f-8088-4c8d-93cf-aa59007da034
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 사전 요구 사항 소프트웨어 다운로드 및 구성 {#download-and-configure-prerequisite-software}

1. https://www.oracle.com/technetwork/java/javase/downloads/에서 JDK를 [다운로드하십시오](https://www.oracle.com/technetwork/java/javase/downloads/).

   설치 프로세스는 간단합니다. 시스템에 JDK가 이미 설치되어 있는 경우 이 단계를 건너뛸 수 있지만 JDK, Eclipse IDE 및 OS가 호환되어야 합니다.
1. https://www.eclipse.org/downloads에서 Java 개발자용 Eclipse IDE를 [다운로드하십시오](https://www.eclipse.org/downloads).

   패키지의 압축을 푼 후 Eclipse를 직접 실행할 수 있습니다. 설치 프로그램이 없습니다.
1. https://developer.android.com/sdk/index.html에서 Android SDK ADT 번들을 [다운로드하십시오](https://developer.android.com/sdk/index.html).

   이 번들에는 Eclipse가 포함되어 있습니다. 시스템에 Eclipse가 이미 설치되어 있는 경우 [!UICONTROL Use An Existing IDE] 섹션에서 플랫폼용 SDK 도구를 다운로드할 수 있습니다.

   압축을 풀고 기억할 위치에 설치합니다. 나중에 참조해야 합니다.
1. Android SDK를 구성합니다.
   1. 터미널(Mac OS X에서) 또는 명령 프롬프트(Windows)를 엽니다.
   1. Android SDK를 다운로드/압축을 푼 디렉토리로 이동합니다.
   1. 이름이 [!DNL android]있는 파일이 들어 있는 tools 폴더로 이동합니다.
   1. 다음 명령을 실행합니다.

      * Mac OS X/Unix의 경우:

         ```
         chmod +x android 
         android update sdk --no-ui
         ```

      * Windows의 경우:

         ```
         android update sdk --no-ui
         ```

         이 프로세스는 시간이 오래 걸립니다.

1. Eclipse 구성
   1. Eclipse를 시작합니다.

      Windows의 경우 Eclipse가 시작되지 않고 보고된 문제는 Eclipse가 필요한 Java 파일을 찾을 수 없다는 것입니다. 다음을 시도해 보십시오.

      * 파일에 `-vm C:\[path to your JDK bin]\javaw.exe` 추가할 수 [!DNL eclipse.ini] 있습니다.
   1. > **[!UICONTROL Help]** 를 **[!UICONTROL Install New Software]** 선택합니다.
   1. 클릭 **[!UICONTROL Add...]**.
   1. 이름을 `Android` 입력합니다.
   1. 링크를 `https://dl-ssl.google.com/android/eclipse/` 입력합니다 **[!UICONTROL Work with]** .
   1. 클릭 **[!UICONTROL OK]**.

      다음과 유사한 대화 상자가 표시됩니다.

      ![](assets/available_software.jpg)

   1. 결과 패키지(개발자 도구 및 NDK 플러그인의 패키지)를 선택하고 **[!UICONTROL Next]**&#x200B;클릭합니다.

      이렇게 하면 ADT(Android Development Tools)가 다운로드됩니다.
   1. 다운로드가 완료되면 Eclipse를 다시 시작합니다.
   Android SDK가 이제 설치됩니다. 1.Android SDK를 찾아 리소스로 사용할 수 있도록 Eclipse를 구성합니다.
   1. Eclipse를 엽니다.
   1. Windows **[!UICONTROL Window]** 에서 **[!UICONTROL Preferences]** > 선택; > **[!UICONTROL ADT]** Mac OS **[!UICONTROL Preferences]** X에서
   1. 탭을 **[!UICONTROL Android]** 선택합니다.
   1. Android SDK의 위치를 찾습니다.
   1. 클릭 **[!UICONTROL Apply]**.

      ![단계 결과](assets/ss2.jpg)


