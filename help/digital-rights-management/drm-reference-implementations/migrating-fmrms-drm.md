---
description: FMRMS(Flash 미디어 Rights Management 서버) 1.0 또는 1.5로 패키지화된 콘텐츠에 대한 라이선스를 계속 발급하려면 LiveCycle ES 서버에서 Adobe Primetime DRM SDK를 기반으로 하는 고객의 새 서버로 라이선스 및 DRM 정책 데이터를 마이그레이션해야 합니다.
title: FMRMS 1.0 또는 1.5에서 Adobe Primetime DRM 2.0 이상으로 마이그레이션
exl-id: 6490f2ad-4863-4b41-9ebd-1de47da4250b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# FMRMS 1.0 또는 1.5에서 Adobe Primetime DRM 2.0 이상으로 마이그레이션{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

FMRMS(Flash 미디어 Rights Management 서버) 1.0 또는 1.5로 패키지화된 콘텐츠에 대한 라이선스를 계속 발급하려면 LiveCycle ES 서버에서 Adobe Primetime DRM SDK를 기반으로 하는 고객의 새 서버로 라이선스 및 DRM 정책 데이터를 마이그레이션해야 합니다.

마이그레이션하려면 다음 작업을 완료하십시오.

1. 라이선스 정보 가져오기:

   1. LiveCycle ES에서 Primetime DRM 기반 서버로 라이센스 정보를 가져오려면 [!DNL Reference Implementation\Server\migration\db] 폴더를 삭제합니다.
   1. 샘플 스크립트를 실행하여 MySQL, Oracle 또는 SQL Server 데이터베이스의 관련 데이터를 CSV 파일 형식으로 내보냅니다.
   1. LiveCycle ES에서 데이터를 내보낸 후 데이터를 데이터베이스로 가져옵니다.

      내보낸 라이센스 정보에는 다음 항목이 포함됩니다.

      * 라이선스 ID
      * 패키징 시 할당되는 콘텐츠 ID
      * 적용 중인 DRM 정책의 ID
      * 콘텐츠가 패키징된 시간
      * 콘텐츠 암호화 키

      1.x 컨텐츠 메타데이터를 Primetime DRM 메타데이터 형식으로 변환하려면 이 정보가 필요합니다. 참조 구현에서 이 데이터는 라이선스 데이터베이스 테이블에 저장되고 다음에서 사용됩니다. `RefImplMetadataConvReqHandler`. 자세한 내용은 `FMRMSv1RequestHandler` 및 `FMRMSv1MetadataHandler`.


1. FMRMS 정책을 Primetime DRM 형식으로 변환:

   1. DRM 정책을 적용하여 버전 1.0 또는 버전 1.5 콘텐츠에 대한 메타데이터 및 발급 라이선스를 변환하려면 먼저 기존 DRM 정책을 Primetime DRM 형식으로 변환해야 합니다.

      다음 `Reference Implementation\Server\migration` 폴더에는 이전 DRM 정책을 기반으로 하는 Primetime DRM 정책을 생성하는 샘플 코드가 포함되어 있습니다. FMRMS 1.0에서 Primetime DRM으로 마이그레이션하려면 `V1_0PolicyConverter.java` 샘플.
   1. 다음을 실행하여 샘플 코드 컴파일 `ant-f build-migration.xml build-1.0-converter` 스크립트는에서 1.0 및 Primetime DRM 라이브러리를 검색합니다. [!DNL libs/1.0] 및 [!DNL libs/flashaccess] 디렉토리.

   1. 편집 [!DNL converter.properties] LiveCycle ES 서버를 지정하는 파일입니다.
   1. 실행 `ant -f build-migration.xml migrate-all-1.0-policies` 를 클릭하여 모든 FMRMS 1.0 DRM 정책을 Primetime DRM 형식으로 변환합니다.

      FMRMS 1.5에서 Primetime DRM으로 마이그레이션하려면 `V1_5PolicyConverter.java` 샘플.

   1. 다음을 실행하여 샘플 코드 컴파일 `ant-f build-migration.xml build-1.5-converter` 스크립트(1.5 및 3.0 라이브러리가 [!DNL libs/1.5] 및 [!DNL libs/flashaccess] 디렉토리.

   1. 편집 [!DNL converter.properties] LiveCycle ES 서버를 지정하는 파일입니다.
   1. 실행 `ant -f build-migration.xml migrate-all-1.5-policies` 를 클릭하여 모든 FMRMS 1.5 DRM 정책을 Primetime DRM 형식으로 변환합니다.

      변환된 DRM 정책은 파일 세트로 저장됩니다. 다음 `DRM PolicyConverter` 는 이전 DRM 정책 ID와 새 DRM 정책 ID의 매핑을 포함하는 CSV 형식의 파일을 생성합니다. 이 파일을 로 가져올 수 있습니다. [!DNL PolicyConversion] 다음에서 사용하는 참조 구현 데이터베이스의 테이블 `RefImplMetadataConvReqHandler`.

1. 에서 1.x 호환성 요청을 지원합니다. `FMRMSv1RequestHandler` 및 `FMRMSv1MetadataHandler` 속성:

   1. 관련 데이터가 Primetime DRM 기반 서버로 마이그레이션되면 1.x 호환성 요청에 대한 지원을 구현합니다.

      이러한 유형의 요청을 처리하는 방법에 대한 예는 를 참조하십시오. `RefImplUpgradeV1ClientHandler` 및 `RefImplMetadataConvReqHandler` 를 참조하십시오.
