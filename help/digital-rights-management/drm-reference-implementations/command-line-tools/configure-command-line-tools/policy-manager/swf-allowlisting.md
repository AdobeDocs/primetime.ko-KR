---
title: SWF 애플리케이션 허용 목록
description: SWF 애플리케이션 허용 목록
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# SWF 애플리케이션 허용 목록 {#swf-application-allowlisting}

SWF 응용 프로그램을 허용 목록 하려면 다음 두 가지 전략 중 하나를 따를 수 있습니다.

* SWF URL을 지정할 수 있습니다. 이는 특히 정기적으로 SWF을 재구축하는 개발 환경에서 매우 유연한 접근 방식입니다.
* SWF 해시를 지정할 수 있습니다. SWF의 암호화 다이제스트 값입니다. 이 방법은 응용 프로그램이 변경되고 다시 빌드될 때 SWF 해시가 변경되므로 유연성은 떨어지지만 훨씬 엄격합니다. 이 경우 이전 HASH에 바인딩된 모든 컨텐츠가 새 플레이어에서 재생되지 않고 다시 패키징되어야 합니다. 다음 [!DNL PolicyManager.jar] 을 지정하면 도구가 자동으로 해시를 계산합니다. [!DNL .swf] 파일.

  반면 Flash/Adobe Media Server(FMS/AMS)을 통해 Primetime DRM을 사용하는 경우 특정 SWF에 경로를 제공할 수 있으며, FMS/AMS는 사용자가 FMS/AMS에 의해 스트리밍되는 컨텐츠를 패키징하는 데 사용되는 DRM 정책에 삽입할 SWF을 자동으로 해시합니다.

다음을 참조하십시오 `policy.allowedSWFApplication.n` 위치: *구성 속성* 을 참조하십시오.
