---
seo-title: SWF 애플리케이션 화이트리스트
title: SWF 애플리케이션 화이트리스트
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# SWF 애플리케이션 화이트리스트{#swf-application-whitelisting}

SWF 애플리케이션을 화이트리스트하려면 다음 두 가지 전략 중 하나를 따르십시오.

* SWF에 대한 URL을 지정할 수 있습니다. 이는 특히 SWF를 정기적으로 재구축하는 개발 환경에서 매우 유연한 접근 방식입니다.
* SWF 해시를 지정할 수 있습니다. SWF의 암호화 다이제스트 값입니다. SWF 해시는 응용 프로그램이 변경되고 다시 빌드될 때 변경되므로 이러한 방식은 유연성이 떨어지며 더욱 엄격해집니다. 이 경우 이전 HASH에 바인딩된 모든 콘텐츠가 새 플레이어에서 재생되지 않으므로 다시 패키지해야 합니다. 파일을 지정할 경우 [!DNL PolicyManager.jar] 도구는 자동으로 해시를 [!DNL .swf] 계산합니다.

   반면 Flash/Adobe Media Server(FMS/AMS)를 통해 Primetime DRM을 사용하는 경우 특정 SWF의 경로를 제공할 수 있으며 FMS/AMS는 FMS/AMS에서 스트리밍한 컨텐츠를 패키지하는 데 사용되는 DRM 정책에 삽입할 수 있도록 SWF를 자동으로 해시합니다. .

자세한 `policy.allowedSWFApplication.n` 내용은 *구성 속성을* 참조하십시오.
