---
seo-title: SWF 응용 프로그램 목록 허용
title: SWF 응용 프로그램 목록 허용
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# SWF 응용 프로그램에서 {#swf-application-allowlisting} 나열을 허용합니다.

SWF 애플리케이션을 허용 목록하려면 다음 두 가지 전략 중 하나를 따라야 합니다.

* SWF에 대한 URL을 지정할 수 있습니다. 이는 특히 SWF를 정기적으로 재구성하는 개발 환경에서 매우 유연한 접근 방식입니다.
* SWF 해시를 지정할 수 있습니다. SWF의 암호화 다이제스트 값입니다. SWF 해시는 응용 프로그램이 변경되고 다시 빌드될 때 변경되므로 이 방법은 덜 유연하지만 훨씬 더 엄격합니다. 이 경우 이전 HASH에 연결된 모든 콘텐츠가 새 플레이어에서 재생되지 않으므로 다시 패키지해야 합니다. [!DNL .swf] 파일을 지정하는 경우 [!DNL PolicyManager.jar] 도구는 해시를 자동으로 계산합니다.

   반면 Flash/Adobe 미디어 서버(FMS/AMS)를 통해 Primetime DRM을 사용하는 경우 특정 SWF에 대한 경로를 제공할 수 있으며 FMS/AMS는 FMS/AMS에서 스트리밍한 컨텐츠를 패키지하는 데 사용되는 DRM 정책에 삽입하기 위해 SWF를 자동으로 해시합니다. ..

자세한 내용은 *구성 속성*&#x200B;의 `policy.allowedSWFApplication.n`을 참조하십시오.
