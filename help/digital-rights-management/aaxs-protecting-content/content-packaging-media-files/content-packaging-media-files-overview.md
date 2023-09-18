---
title: 개요
description: 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 개요 {#overview}

*패키징* 는 FLV 또는 F4V 파일을 암호화하고 정책을 적용하는 프로세스를 말합니다. 미디어 패키징 API를 사용하여 파일을 패키징합니다. Adobe 액세스 Java SDK는 점진적 다운로드 Flash과 FLV, F4V 및 MP4와 같은 AIR 콘텐츠만 패키징할 수 있습니다. HDS(Adobe HTTP Dynamic Streaming) 또는 HLS(Apple HTTP Live Streaming)와 같은 다른 컨텐츠 형식에 대해 Adobe 액세스 DRM을 사용하여 컨텐츠를 패키징하려면 Adobe Media Server( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) 또는 Adobe 브로드캐스트 SDK( )를 구현하는 인코더 [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). 또는 HDS, HLS 및 DASH와 같은 다양한 대상 형식에 대한 컨텐츠를 패키징할 수 있는 Adobe의 Java Primetime Packager 도구 세트를 사용할 수도 있습니다.

패키지로 라이센스 서버에서 연결이 해제됩니다. 패키저가 라이센스 서버에 연결하여 콘텐츠에 대한 정보를 교환할 필요가 없습니다. 라이센스 서버가 라이센스를 발급하기 위해 알아야 하는 모든 사항이 컨텐츠 메타데이터에 포함됩니다.

파일이 암호화되면 적절한 라이센스가 없으면 해당 콘텐츠를 구문 분석할 수 없습니다. Adobe 액세스를 통해 암호화할 파일의 부분을 선택할 수 있습니다. Adobe® Access™은 FLV 및 F4V 컨텐츠의 파일 형식을 구문 분석할 수 있으므로 전체 파일이 아닌 파일의 선택적 부분을 지능적으로 암호화할 수 있습니다. 메타데이터 및 큐 포인트와 같은 데이터는 암호화되지 않은 상태로 유지되므로 검색 엔진이 여전히 파일을 검색할 수 있습니다.

지정된 콘텐츠 조각에 여러 정책이 있을 수 있습니다. 이 기능은 예를 들어 콘텐츠를 여러 번 패키징하지 않고 다른 비즈니스 모델에 따라 콘텐츠에 라이선스를 부여하려는 경우 유용할 수 있습니다. 예를 들어 짧은 기간 동안 익명 액세스를 허용할 수 있으며, 그 후에는 고객이 콘텐츠를 구입하고 무제한 액세스할 수 있습니다. 콘텐츠가 여러 정책을 사용하여 패키지화된 경우 라이선스 서버는 라이선스를 발급하는 데 사용할 정책을 선택하는 논리를 구현해야 합니다.

>[!NOTE]
>
>아키텍처를 사용하면 콘텐츠를 패키징할 때 사용 정책을 지정하고 콘텐츠에 바인딩할 수 있습니다. 클라이언트가 콘텐츠를 재생하려면 먼저 클라이언트가 해당 컴퓨터에 대한 라이선스를 취득해야 합니다. 라이선스는 적용되는 사용 규칙을 지정하고 콘텐츠를 해독하는 데 사용되는 키를 제공합니다. 정책은 라이선스를 생성하기 위한 템플릿이지만 라이선스 서버는 라이선스를 발급할 때 사용 규칙을 재정의하도록 선택할 수 있습니다. 라이선스는 만료 시간 또는 재생 기간과 같은 제약 조건에 의해 유효하지 않게 렌더링될 수 있습니다.

콘텐츠를 패키징할 때 사용할 수 있는 다양한 옵션이 있습니다. 다음은에 지정됩니다. `DRMParameters` 인터페이스 및 해당 인터페이스를 구현하는 클래스입니다. `F4VDRMParameters` 및 `FLVDRMParameters`. 이러한 클래스를 사용하여 서명 및 키 매개 변수를 설정할 수 있을 뿐만 아니라 오디오 콘텐츠, 비디오 콘텐츠 또는 스크립트 데이터를 암호화할지 여부를 지정할 수 있습니다. 참조 구현에서 이러한 옵션이 어떻게 구현되는지 보려면 에서 설명한 미디어 패키지 프로그램 명령줄 옵션에 대한 설명을 참조하십시오. *Adobe 액세스 참조 구현 사용*. 이러한 옵션은 Java API를 기반으로 하므로 프로그래밍 방식으로 사용할 수 있습니다.

패키징 옵션은 다음과 같습니다.

* 암호화 옵션(오디오, 비디오, 부분 암호화).
* 라이선스 서버 URL(클라이언트는 라이선스 서버로 전송된 모든 요청에 대해 이 URL을 기본 URL로 사용)
* 라이선스 서버 전송 인증서
* CEK 암호화에 사용되는 라이선스 서버 인증서.
* 서명 메타데이터에 대한 패키지 자격 증명

Adobe 액세스는 CEK 전달을 위한 API를 제공합니다. CEK를 지정하지 않으면 SDK가 임의로 생성합니다. 일반적으로 각 콘텐츠에 대해 다른 CEK가 필요합니다. 그러나 Dynamic Streaming에서는 해당 컨텐츠의 모든 파일에 동일한 CEK를 사용할 수 있으므로 사용자는 단일 라이센스만 필요하며 한 비트율에서 다른 비트율로 원활하게 전환할 수 있습니다. 여러 콘텐츠에 대해 동일한 키와 라이센스를 사용하려면 동일한 키를 전달합니다 `DRMParameters` 대상 오브젝트 `MediaEncrypter.encryptContent()`또는 를 사용하여 CEK에 전달 `V2KeyParameters.setContentEncryptionKey()`. 각 콘텐츠에 대해 다른 키와 라이선스를 사용하려면 새 를 만드십시오 `DRMParameters` 각 파일의 인스턴스입니다.

키 회전을 사용하여 컨텐츠를 패키징할 때 사용되는 회전 키와 키 변경 빈도를 제어할 수 있습니다. `F4VDRMParameters` 및 `FLVDRMParameters` 구현 `KeyRotationParameters` 인터페이스. 이 인터페이스를 통해 키 순환을 활성화할 수 있습니다. 또한 다음을 지정해야 합니다. `RotatingContentEncryptionKeyProvider`. 암호화된 각 샘플에 대해 이 클래스는 사용할 회전 키를 결정합니다. 자체 공급자를 구현하거나 `TimeBasedKeyProvider` SDK에 포함됩니다. 이 구현은 지정된 시간(초) 후 임의로 새 키를 생성합니다.

경우에 따라 컨텐츠 메타데이터를 별도의 파일로 저장하고 컨텐츠와 별도로 클라이언트에서 사용할 수 있도록 해야 할 수 있습니다. 이렇게 하려면 를 호출하십시오. `MediaEncrypter.encryptContent()`: `MediaEncrypterResult` 개체. 호출 `MediaEncrypterResult.getKeyInfo()` 결과를 다음으로 캐스트 `V2KeyStatus`. 그런 다음 콘텐츠 메타데이터를 검색하고 파일에 저장합니다.

이러한 모든 작업은 Java API를 사용하여 수행할 수 있습니다. 이 장에서 설명한 Java API에 대한 자세한 내용은 *Adobe 액세스 API 참조*.

Media Packager 참조 구현에 대한 자세한 내용은 *Adobe 액세스 참조 구현 사용*.
