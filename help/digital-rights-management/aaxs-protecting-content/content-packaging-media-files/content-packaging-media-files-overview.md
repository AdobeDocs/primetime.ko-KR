---
seo-title: 개요
title: 개요
uuid: 11cf1f1f-a4b2-4ac2-aae7-e925d96729d2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---


# 개요 {#overview}

*패키지* 는 FLV 또는 F4V 파일에 정책을 암호화하고 적용하는 프로세스를 말합니다. 미디어 패키징 API를 사용하여 파일을 패키지화할 수 있습니다. Adobe 액세스 Java SDK는 점진적 다운로드 Flash 및 AIR 컨텐츠(예: FLV, F4V 및 MP4)만 패키지할 수 있습니다. Adobe HTTP Dynamic Streaming(HDS) 또는 Apple HTTP 라이브 스트리밍(HLS)과 같은 기타 컨텐츠 포맷에 대한 Adobe 액세스 DRM을 사용하여 컨텐츠를 패키지하려면 Adobe 미디어 서버( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) 또는 Adobe 브로드캐스트 SDK를 구현하는 인코더( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf))와 같은 다른 도구를 사용해야 합니다 ). 또한 고객은 HDS, HLS 및 DASH와 같은 다양한 대상 포맷의 컨텐츠를 패키지화할 수 있는 Adobe의 Java Primetime Packager 툴 세트를 사용할 수 있습니다.

라이선스 서버에서 패키징이 제거됩니다. Packager가 라이센스 서버에 연결하여 콘텐트에 대한 정보를 교환할 필요가 없습니다. 라이센스 서버에서 라이센스 문제를 해결하는 데 필요한 모든 것이 컨텐츠 메타데이터에 포함됩니다.

파일이 암호화되면 해당 라이센스 없이는 해당 파일의 내용을 구문 분석할 수 없습니다. Adobe 액세스를 사용하면 암호화할 파일의 일부를 선택할 수 있습니다. Adobe® Access™는 FLV 및 F4V 내용의 파일 포맷을 구문 분석할 수 있으므로 전체 파일 대신 파일의 선택 부분을 지능적으로 암호화할 수 있습니다. 메타데이터 및 큐 포인트와 같은 데이터는 암호화되지 않은 상태로 유지되므로 검색 엔진이 파일을 계속 검색할 수 있습니다.

특정 컨텐츠에 여러 정책이 포함될 수 있습니다. 예를 들어 컨텐츠를 여러 번 패키징하지 않고도 다른 비즈니스 모델에서 컨텐츠에 라이선스를 부여하려는 경우 유용합니다. 예를 들어 짧은 기간 동안 익명 액세스를 허용할 수 있으며 그 이후에는 고객이 컨텐츠를 구매하고 제한 없이 액세스할 수 있습니다. 컨텐츠가 여러 정책을 사용하여 패키지되는 경우 라이센스 서버는 라이센스 발급에 사용할 정책을 선택하는 로직을 구현해야 합니다.

>[!NOTE]
>
>아키텍처는 컨텐츠를 패키지화할 때 사용 정책을 지정하고 컨텐츠에 바인딩하도록 허용합니다. 클라이언트가 콘텐트를 재생하려면 먼저 해당 컴퓨터에 대한 라이센스를 취득해야 합니다. 라이선스는 적용되는 사용 규칙을 지정하며 콘텐츠의 암호를 해독하는 데 사용되는 키를 제공합니다. 본 정책은 라이센스를 생성하기 위한 템플릿이지만 라이센스 서버는 라이센스를 발급할 때 사용 규칙을 무시하도록 선택할 수 있습니다. 만료 시간 또는 재생 창과 같은 제한 사항으로 인해 라이센스가 잘못 렌더링될 수 있습니다.

컨텐츠를 패키지화할 때 사용할 수 있는 다양한 옵션이 있습니다. 이러한 클래스는 `DRMParameters` 인터페이스에 지정되어 있으며 해당 인터페이스를 구현하는 클래스입니다(예: `F4VDRMParameters` 및 `FLVDRMParameters`). 이러한 클래스를 사용하면 서명 및 키 매개 변수를 설정할 수 있을 뿐만 아니라 오디오 콘텐트, 비디오 콘텐트 또는 스크립트 데이터를 암호화할 것인지 여부를 지정할 수 있습니다. 이러한 구현이 참조 구현에서 구현되는 방식을 보려면 *Adobe 액세스 참조 구현 사용*&#x200B;에서 설명한 Media Packager 명령줄 옵션에 대한 설명을 참조하십시오. 이러한 옵션은 Java API를 기반으로 하므로 프로그래밍 방식으로 사용할 수 있습니다.

패키지 옵션은 다음과 같습니다.

* 암호화 옵션(오디오, 비디오, 부분 암호화).
* 라이센스 서버 URL(클라이언트는 이것을 라이센스 서버에 전송된 모든 요청에 대한 기본 URL로 사용)
* 라이선스 서버 전송 인증서
* CEK를 암호화하는 데 사용되는 라이센스 서버 인증서
* 메타데이터 서명을 위한 패키지 자격 증명

Adobe 액세스는 CEK에 전달하기 위한 API를 제공합니다. CEK를 지정하지 않으면 SDK에서 임의로 생성합니다. 일반적으로 각 컨텐츠에 대해 다른 CEK가 필요합니다. 그러나 Dynamic Streaming에서는 해당 컨텐츠의 모든 파일에 대해 동일한 CEK를 사용할 수 있으므로 사용자는 단일 라이선스만 필요하며 한 비트 전송률에서 다른 비트 전송률로 원활하게 전환할 수 있습니다. 여러 콘텐트에 대해 동일한 키와 라이선스를 사용하려면 동일한 `DRMParameters` 개체를 `MediaEncrypter.encryptContent()`에 전달하거나 `V2KeyParameters.setContentEncryptionKey()`를 사용하여 CEK에 전달합니다. 각 컨텐츠 조각에 대해 다른 키와 라이선스를 사용하려면 각 파일에 대해 새 `DRMParameters` 인스턴스를 만듭니다.

키 회전을 사용하여 컨텐츠를 패키지화할 때 사용되는 순환 키와 키가 변경되는 빈도를 제어할 수 있습니다. `F4VDRMParameters` 를  `FLVDRMParameters` 사용하여  `KeyRotationParameters` 인터페이스를 구현합니다. 이 인터페이스를 통해 키 회전을 활성화할 수 있습니다. `RotatingContentEncryptionKeyProvider`도 지정해야 합니다. 암호화된 각 샘플에 대해 이 클래스는 사용할 순환 키를 결정합니다. 귀하는 자체 공급자를 구현하거나 SDK에 포함된 `TimeBasedKeyProvider`을 사용할 수 있습니다. 이 구현은 지정된 시간(초) 후 새 키를 임의로 생성합니다.

경우에 따라 컨텐츠 메타데이터를 별도의 파일로 저장하고 클라이언트가 컨텐츠와 별도로 사용하도록 설정해야 할 수도 있습니다. 이렇게 하려면 `MediaEncrypterResult` 개체를 반환하는 `MediaEncrypter.encryptContent()`을 호출합니다. `MediaEncrypterResult.getKeyInfo()`을(를) 호출하고 결과를 `V2KeyStatus`에 캐스팅합니다. 그런 다음 컨텐츠 메타데이터를 검색하여 파일에 저장합니다.

이러한 모든 작업은 Java API를 사용하여 수행할 수 있습니다. 이 장에서 설명한 Java API에 대한 자세한 내용은 *Adobe 액세스 API 참조*&#x200B;를 참조하십시오.

Media Packager 참조 구현에 대한 자세한 내용은 *Adobe 액세스 참조 구현 사용*&#x200B;을 참조하십시오.
