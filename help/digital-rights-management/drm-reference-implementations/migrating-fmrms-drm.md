---
description: Flash Media Rights Management Server(FMRMS) 1.0 또는 1.5로 패키지된 컨텐츠에 대한 라이선스를 계속 발행하려면 LiveCycle ES 서버에서 Adobe Primetime DRM SDK를 기반으로 하는 고객의 새로운 서버로 라이선스 및 DRM 정책 데이터를 마이그레이션해야 합니다.
seo-description: Flash Media Rights Management Server(FMRMS) 1.0 또는 1.5로 패키지된 컨텐츠에 대한 라이선스를 계속 발행하려면 LiveCycle ES 서버에서 Adobe Primetime DRM SDK를 기반으로 하는 고객의 새로운 서버로 라이선스 및 DRM 정책 데이터를 마이그레이션해야 합니다.
seo-title: FMRMS 1.0 또는 1.5에서 Adobe Primetime DRM 2.0 이상으로 마이그레이션
title: FMRMS 1.0 또는 1.5에서 Adobe Primetime DRM 2.0 이상으로 마이그레이션
uuid: 49ecbbd2-d83b-4bf2-841e-c3f9e5d5e141
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# FMRMS 1.0 또는 1.5에서 Adobe Primetime DRM 2.0 이상으로 마이그레이션{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Flash Media Rights Management Server(FMRMS) 1.0 또는 1.5로 패키지된 컨텐츠에 대한 라이선스를 계속 발행하려면 LiveCycle ES 서버에서 Adobe Primetime DRM SDK를 기반으로 하는 고객의 새로운 서버로 라이선스 및 DRM 정책 데이터를 마이그레이션해야 합니다.

마이그레이션하려면 다음 작업을 완료하십시오.

1. 라이선스 정보 가져오기:

   1. LiveCycle ES에서 Primetime DRM 기반 서버로 라이선스 정보를 가져오려면 [!DNL Reference Implementation\Server\migration\db] 폴더의 샘플 데이터베이스 스크립트를 참조하십시오.
   1. 샘플 스크립트를 실행하여 관련 데이터를 MySQL, Oracle 또는 SQL Server 데이터베이스에서 CSV 파일 형식으로 내보냅니다.
   1. LiveCycle ES에서 데이터를 내보낸 후 데이터를 데이터베이스로 가져옵니다.

      내보낸 라이센스 정보에는 다음이 포함됩니다.

      * 라이선스 ID
      * 패키징 시 할당된 컨텐츠 ID
      * 적용되는 DRM 정책의 ID
      * 컨텐츠가 패키지된 시간
      * 컨텐츠 암호화 키
      1.x 콘텐츠 메타데이터를 Primetime DRM 메타데이터 형식으로 변환하려면 이 정보가 필요합니다. 참조 구현에서 이 데이터는 라이센스 데이터베이스 테이블에 저장되며 에서 `RefImplMetadataConvReqHandler`사용됩니다. For more information, see `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler`.


1. FMRMS 정책을 Primetime DRM 포맷으로 변환:

   1. DRM 정책을 적용하여 메타데이터를 변환하고 버전 1.0 또는 버전 1.5 콘텐츠에 대한 라이선스를 발행하려면 먼저 기존 DRM 정책을 Primetime DRM 형식으로 변환하십시오.

      이 `Reference Implementation\Server\migration` 폴더에는 이전 DRM 정책을 기반으로 하는 Primetime DRM 정책을 만들기 위한 샘플 코드가 포함되어 있습니다. FMRMS 1.0에서 Primetime DRM으로 마이그레이션하려면 `V1_0PolicyConverter.java` 샘플을 참조하십시오.
   1. 및 `ant-f build-migration.xml build-1.0-converter` 디렉토리에서 1.0 및 Primetime DRM 라이브러리를 검색하는 스크립트를 실행하여 샘플 코드를 [!DNL libs/1.0] [!DNL libs/flashaccess] 컴파일합니다.

   1. LiveCycle ES 서버를 가리키도록 파일을 [!DNL converter.properties] 편집합니다.
   1. 모든 `ant -f build-migration.xml migrate-all-1.0-policies` FMRMS 1.0 DRM 정책을 Primetime DRM 포맷으로 변환하려면 실행합니다.

      FMRMS 1.5에서 Primetime DRM으로 마이그레이션하려면 `V1_5PolicyConverter.java` 샘플을 참조하십시오.

   1. 1.5 및 3.0 라이브러리가 `ant-f build-migration.xml build-1.5-converter` 및 [!DNL libs/1.5] [!DNL libs/flashaccess] 디렉토리에 있어야 하는 스크립트를 실행하여 샘플 코드를 컴파일합니다.

   1. LiveCycle ES 서버를 가리키도록 파일을 [!DNL converter.properties] 편집합니다.
   1. 모든 `ant -f build-migration.xml migrate-all-1.5-policies` FMRMS 1.5 DRM 정책을 Primetime DRM 포맷으로 변환하려면 실행합니다.

      변환된 DRM 정책은 파일 세트로 저장됩니다. 는 이전 DRM 정책 ID의 새 DRM 정책 ID에 대한 매핑을 포함하는 CSV 형식 파일을 `DRM PolicyConverter` 생성합니다. 이 파일을 참조 구현 데이터베이스의 [!DNL PolicyConversion] 테이블로 가져올 수 있습니다. 여기서 이 파일을 사용합니다 `RefImplMetadataConvReqHandler`.

1. 및 속성을 사용하여 1.x 호환성 요청을 `FMRMSv1RequestHandler` `FMRMSv1MetadataHandler` 지원합니다.

   1. 관련 데이터가 Primetime DRM 기반 서버로 마이그레이션되면 1.x 호환성 요청에 대한 지원을 구현합니다.

      이러한 유형의 요청을 처리하는 방법에 대한 예는 참조 구현에서 `RefImplUpgradeV1ClientHandler` 및 `RefImplMetadataConvReqHandler` 을 참조하십시오.

