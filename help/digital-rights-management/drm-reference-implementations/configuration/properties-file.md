---
title: 라이선스 서버 속성 파일
description: 라이선스 서버 속성 파일
copied-description: true
exl-id: 07cd9866-c29b-476e-a63f-9c5272ccd678
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# 라이선스 서버 속성 파일{#license-server-properties-file}

라이센스 서버는 [!DNL flashaccess-refimpl.properties] 파일. 특정 값에 대한 세부 정보와 각 속성에 대한 사용 정보는 해당 파일을 직접 참조할 수 있습니다. 완전한 기능을 갖춘 샘플은 [!DNL resources] 참조 구현의 디렉터리( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**자격 증명** - Adobe 파일에는 사용자에게 문제가 되는 자격 증명의 위치에 대한 설정이 포함되어 있습니다. 다음에서 이러한 자격 증명을 지정할 수 있습니다. [!DNL .pfx] HSM에 저장된 자격 증명에 대한 별칭 및 암호를 입력합니다. 적어도 전송 자격 증명 및 라이선스 서버 자격 증명과 관련된 속성을 구성해야 합니다. 에서 지정한 디렉터리를 기준으로 자격 증명 파일의 위치를 지정합니다. `config.resourcesDirectory` 속성.

**Flash 미디어 Rights Management 서버** - `flashaccess-refimpl.properties` 파일에는 콘텐츠 패키지와 관련된 몇 가지 속성도 포함되어 있습니다. 이러한 속성은 Flash 미디어 Rights Management 서버 1.x 메타데이터 변환에만 사용됩니다. 이 등록 정보 파일의 값을 수정한 후 변경 사항을 적용하려면 라이센스 서버를 다시 시작하십시오.
