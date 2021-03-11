---
description: Primetime Android 참조 구현에서 Adobe Analytics 계정에서 작동하도록 구성하여 비디오 사용을 추적할 수 있습니다.
title: 비디오 분석 구성
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# 비디오 분석 구성 {#configure-video-analytics}

Primetime Android 참조 구현에서 Adobe Analytics 계정에서 작동하도록 구성하여 비디오 사용을 추적할 수 있습니다. Android 참조 구현은 비디오 사용 및 하트비트 데이터를 Adobe Analytics으로 전송하도록 설계되었습니다. 이 기능을 활성화하려면 먼저 Adobe Primetime 담당자에게 연락하여 Adobe Analytics 계정을 만들어야 합니다.

참조 구현 내에는 Adobe Analytics 통합을 사용하도록 구성해야 하는 두 가지 위치가 있습니다. 런타임 비디오 분석 구성은 재생을 위해 새 비디오를 선택하면 영향을 받습니다(즉, 새 PlayerActivity가 만들어지면).

1. `ADBMobileConfig.json` 자산 파일에서 로드 시간 옵션을 구성합니다.

   이 파일은 Adobe 담당자가 제공합니다. 기본적으로 Primetime SDK 번들에 포함되어 있지 않습니다. 이 구성 파일의 설정에 대한 자세한 내용은 다음 Android Programmer&#39;s Guide를 참조하십시오.비디오 분석을 초기화하고 구성합니다.
1. 참조 구현 설정 메뉴에서 런타임 옵션 구성

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | 런타임 옵션 | 설명 |
   |---|---|
   | 비디오 분석 추적 서버 | 비디오 분석 백엔드 컬렉션 끝점의 URL. 모든 비디오 하트비트 추적 호출이 전송되는 곳입니다. |
   | 작업 ID | 처리 작업 식별자입니다. 이것은 비디오 추적 호출에 적용할 처리 종류를 백엔드 끝점으로 나타냅니다. |
   | 채널 | 사용자가 컨텐츠를 시청하는 채널의 이름입니다. 모바일 응용 프로그램의 경우 일반적으로 응용 프로그램의 이름입니다. |
   | 게시자 | 컨텐츠 게시자의 이름 |
   | 디버그 로깅 | 광범위한 로깅을 활성화합니다. 기본적으로 비활성화되어 있으면 활성화되면 성능에 영향을 줄 수 있으므로 프로덕션 환경에서 이 설정을 사용하지 않도록 설정합니다. |
   | 자동 모드 | 이 기능을 활성화하면 네트워크 호출이 수행되지 않으므로 로컬 디버깅에 유용하지만 제작 환경에서는 비활성화해야 합니다. |