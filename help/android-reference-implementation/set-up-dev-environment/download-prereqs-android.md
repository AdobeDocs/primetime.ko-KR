---
title: 사전 요구 사항 소프트웨어 다운로드 및 구성
description: 설치 프로세스는 간단합니다. 시스템에 JDK가 이미 설치되어 있는 경우 이 단계를 건너뛸 수 있지만 JDK, Eclipse IDE 및 OS는 호환되어야 합니다.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# 사전 요구 사항 소프트웨어 {#download-and-configure-prerequisite-software} 다운로드 및 구성

1. [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/)에서 JDK를 다운로드합니다.

   설치 프로세스는 간단합니다. 시스템에 JDK가 이미 설치되어 있는 경우 이 단계를 건너뛸 수 있지만 JDK, Eclipse IDE 및 OS는 호환되어야 합니다.
1. [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads)에서 Java 개발자용 Eclipse IDE를 다운로드합니다.

   패키지를 압축 해제한 후 Eclipse를 직접 실행할 수 있습니다. 설치 프로그램이 없습니다.
1. [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)에서 Android SDK ADT 번들을 다운로드합니다.

   이 번들에는 Eclipse가 포함되어 있습니다. 시스템에 Eclipse가 이미 설치되어 있는 경우 [!UICONTROL Use An Existing IDE] 섹션에서 플랫폼용 SDK 도구를 다운로드할 수 있습니다.

   압축을 풀고 기억되는 위치에 설치합니다. 나중에 이 항목을 참조해야 합니다.
1. Android SDK를 구성합니다.
   1. Mac OS X에서 터미널 또는 명령 프롬프트를 엽니다(Windows).
   1. Android SDK를 다운로드/압축 해제한 디렉토리로 이동합니다.
   1. [!DNL android] 파일이 포함된 도구 폴더로 이동합니다.
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

      Windows의 경우 Eclipse가 시작되지 않고 Eclipse가 필요한 Java 파일을 찾을 수 없는 문제가 보고되는 경우 다음을 시도해 보십시오.

      * [!DNL eclipse.ini] 파일에 `-vm C:\[path to your JDK bin]\javaw.exe`을(를) 추가합니다.
   1. **[!UICONTROL Help]** > **[!UICONTROL Install New Software]**&#x200B;을 선택합니다.
   1. 클릭 **[!UICONTROL Add...]**.
   1. 이름에 `Android`을 입력합니다.
   1. **[!UICONTROL Work with]** 링크에 `https://dl-ssl.google.com/android/eclipse/`을 입력합니다.
   1. 클릭 **[!UICONTROL OK]**.

      다음과 유사한 대화 상자가 표시됩니다.

      ![](assets/available_software.jpg)

   1. 결과 패키지(개발자 도구 및 NDK 플러그인의 패키지)를 선택하고 **[!UICONTROL Next]**&#x200B;을 클릭합니다.

      이렇게 하면 ADT(Android Development Tools)가 다운로드됩니다.
   1. 다운로드가 완료되면 Eclipse를 다시 시작합니다.

   이제 Android SDK가 설치됩니다. 1. Android SDK를 찾아 리소스로 사용할 수 있도록 Eclipse를 구성합니다.
   1. Eclipse를 엽니다.
   1. Windows에서 **[!UICONTROL Window]** > **[!UICONTROL Preferences]** 선택 Mac OS X의 **[!UICONTROL ADT]** > **[!UICONTROL Preferences]**
   1. **[!UICONTROL Android]** 탭을 선택합니다.
   1. Android SDK 위치를 찾습니다.
   1. 클릭 **[!UICONTROL Apply]**.

      ![단계 결과](assets/ss2.jpg)


