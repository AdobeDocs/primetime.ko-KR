---
title: 라이센스 서버 속성 파일
description: 라이센스 서버 속성 파일
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# 라이센스 서버 속성 파일{#license-server-properties-file}

라이센스 서버는 [!DNL flashaccess-refimpl.properties] 파일에 설정된 속성을 참조합니다. 특정 값에 대한 자세한 내용과 각 속성에 대한 사용 정보를 보려면 해당 파일을 직접 참조할 수 있습니다. 전체 기능 샘플은 참조 구현( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`)의 [!DNL resources] 디렉토리에 제공됩니다.

**자격 증명**  - 속성 파일에는 Adobe이 사용자에게 문제를 일으키는 자격 증명 위치의 설정이 포함됩니다. [!DNL .pfx] 파일에서 암호를 사용하여 이러한 자격 증명을 지정하거나 HSM에 저장된 자격 증명을 위한 별칭 및 암호를 제공할 수 있습니다. 전송 자격 증명 및 라이센스 서버 자격 증명과 관련된 속성을 적어도 구성해야 합니다. `config.resourcesDirectory` 속성에 지정한 디렉토리를 기준으로 자격 증명 파일의 위치를 지정합니다.

**Flash 미디어 Rights Management 서버**  -  `flashaccess-refimpl.properties` 파일에는 컨텐츠 패키징과 관련된 여러 속성이 포함되어 있습니다. 이러한 속성은 Flash Media Rights Management Server 1.x 메타데이터 변환에만 사용됩니다. 이 속성 파일의 값을 수정한 후 변경 사항을 적용하려면 라이선스 서버를 다시 시작하십시오.
