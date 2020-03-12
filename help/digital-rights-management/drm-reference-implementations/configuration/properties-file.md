---
description: 'null'
seo-description: 'null'
seo-title: 라이센스 서버 속성 파일
title: 라이센스 서버 속성 파일
uuid: 5e94ed1f-1dbf-4506-a097-183fcd5d25ef
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 라이센스 서버 속성 파일{#license-server-properties-file}

라이센스 서버는 [!DNL flashaccess-refimpl.properties] 파일에 설정된 속성을 참조합니다. 특정 값에 대한 자세한 내용과 각 속성에 대한 사용 정보를 직접 참조할 수 있습니다. 참조 구현()의 [!DNL resources] `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`디렉토리에 완전한 기능 샘플이 제공됩니다.

**자격 증명** - 등록 정보 파일에는 Adobe가 사용자에게 발행하는 자격 증명의 위치에 대한 설정이 포함됩니다. 암호를 사용하여 [!DNL .pfx] 파일에 이러한 자격 증명을 지정하거나 HSM에 저장된 자격 증명을 위한 별칭 및 암호를 제공할 수 있습니다. 전송 자격 증명 및 라이센스 서버 자격 증명과 관련된 속성을 구성해야 합니다. 속성에 지정한 디렉토리에 상대적인 자격 증명 파일의 위치를 `config.resourcesDirectory` 지정합니다.

**Flash Media Rights Management** Server - `flashaccess-refimpl.properties` 이 파일에는 컨텐츠 패키징과 관련된 여러 속성이 포함되어 있습니다. 이러한 속성은 Flash Media Rights Management Server 1.x 메타데이터 변환에만 사용됩니다. 이 속성 파일의 값을 수정한 후 변경 사항을 적용하려면 라이선스 서버를 다시 시작하십시오.
