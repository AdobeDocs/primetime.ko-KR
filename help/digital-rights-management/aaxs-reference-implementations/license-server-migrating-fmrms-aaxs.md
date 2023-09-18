---
title: FMRMS 1.0 또는 1.5에서 Adobe 액세스 2.0 이상으로 마이그레이션
description: FMRMS 1.0 또는 1.5에서 Adobe 액세스 2.0 이상으로 마이그레이션
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# FMRMS 1.0 또는 1.5에서 Adobe 액세스 2.0 이상으로 마이그레이션 {#migrating-from-fmrms-or-to-adobe-access-and-above}

FMRMS(Flash 미디어 Rights Management 서버) 1.0 또는 1.5를 사용하여 패키징된 콘텐츠에 대한 라이선스를 계속 발급하려면 라이선스 및 정책 데이터를 LiveCycle ES 서버에서 Adobe 액세스 SDK를 기반으로 고객의 새 서버로 마이그레이션해야 합니다. 중요한 단계는 다음과 같습니다.

1. 라이선스 정보 가져오는 중
1. FMRMS 정책을 Adobe 액세스 형식으로 변환 중
1. 를 통해 1.x 호환성 요청 지원 `FMRMSv1RequestHandler` 및 `FMRMSv1MetadataHandler`

LiveCycle ES에서 Adobe 액세스 기반 서버로 라이선스 정보를 가져오려면 [!DNL Reference Implementation\Server\migration\db] 폴더를 삭제합니다. MySQL, Oracle 또는 SQL Server 데이터베이스의 관련 데이터를 CSV 파일 형식으로 내보내는 샘플 스크립트가 제공됩니다. 데이터를 내보내면 선택한 데이터베이스로 가져올 수 있습니다. 내보낸 라이선스 정보에는 라이선스 ID, 패키징 시간에 할당된 콘텐츠 ID, 사용된 정책 ID, 콘텐츠가 패키징된 시간 및 콘텐츠 암호화 키가 포함됩니다. Adobe 액세스의 경우 1.x 컨텐츠 메타데이터를 Adobe 액세스 메타데이터 형식으로 변환하려면 이 정보가 필요합니다( 참조) `FMRMSv1RequestHandler` 및 `FMRMSv1MetadataHandler`). 참조 구현에서 이 데이터는 라이선스 데이터베이스 테이블에 저장되고 다음에서 사용됩니다. `RefImplMetadataConvReqHandler`.

메타데이터를 변환하고 1.0 또는 1.5 콘텐츠에 대한 라이선스를 발급할 때 기존 정책을 사용하려면 Adobe 액세스 형식으로 변환해야 합니다. Reference Implementation\Server\migration 폴더에는 이전 정책을 기반으로 Adobe 액세스 정책을 만들기 위한 샘플 코드가 들어 있습니다.

FMRMS 1.0에서 Adobe 액세스로 마이그레이션하는 경우 V1_0PolicyConverter.java 샘플을 참조하십시오. 를 실행하여 샘플 코드를 컴파일합니다. `ant-f build-migration.xml build-1.0-converter`&quot;(스크립트는 1.0 및 Adobe 액세스 라이브러리가 [!DNL libs/1.0] 및 libs/flashaccess가 각각). LiveCycle ES 서버를 가리키도록 converter.properties 파일을 편집합니다. 그런 다음 &quot; 실행 `ant -f build-migration.xml migrate-all-1.0-policies`모든 FMRMS 1.0 정책을 Adobe 액세스 형식으로 변환합니다.

FMRMS 1.5에서 Adobe 액세스로 마이그레이션하는 경우 V1_5PolicyConverter.java 샘플을 참조하십시오. 를 실행하여 샘플 코드를 컴파일합니다. `ant-f build-migration.xml build-1.5-converter`&quot;(스크립트는 1.5 및 3.0 라이브러리가 각각 libs/1.5 및 libs/flashaccess에 있을 것으로 예상함). LiveCycle ES 서버를 가리키도록 converter.properties 파일을 편집합니다. 그런 다음 &quot; 실행 `ant -f build-migration.xml migrate-all-1.5-policies`모든 FMRMS 1.5 정책을 Adobe 액세스 형식으로 변환합니다.

변환된 정책은 파일 집합에 기록됩니다. 또한 PolicyConverter는 이전 정책 ID와 새 정책 ID의 매핑이 포함된 CSV 파일을 출력합니다. 이 파일은 참조 구현 데이터베이스의 &quot;PolicyConversion&quot; 테이블로 가져올 수 있으며 `RefImplMetadataConvReqHandler`.

관련 데이터가 Adobe 액세스 기반 서버로 마이그레이션되면 1.x 호환성 요청에 대한 지원을 구현할 준비가 된 것입니다. 다음을 참조하십시오 `RefImplUpgradeV1ClientHandler` 및 `RefImplMetadataConvReqHandler` 참조 구현에서 이러한 유형의 요청을 처리하는 방법에 대한 예를 참조하십시오.
