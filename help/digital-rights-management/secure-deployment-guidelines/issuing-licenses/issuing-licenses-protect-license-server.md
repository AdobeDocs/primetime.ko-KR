---
description: '라이선스를 안전하게 발급해야 합니다. 라이센스 서버를 보호하기 위해 이러한 우수 사례를 고려하십시오 '
seo-description: '라이선스를 안전하게 발급해야 합니다. 라이센스 서버를 보호하기 위해 이러한 우수 사례를 고려하십시오 '
seo-title: 라이센스 서버 보호
title: 라이센스 서버 보호
uuid: 7b5de17d-d0a7-41df-9651-4ff51c9965c6
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 라이센스 서버 보호 {#protecting-the-license-server}

라이선스를 안전하게 발급해야 합니다. 라이센스 서버를 보호하기 위해 다음 우수 사례를 고려하십시오.

## 로컬에서 생성된 CRL 사용 {#consuming-locally-generated-crls}

로컬에서 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인합니다.

다음 API는 목록이 무단 변경되었는지, 그리고 목록이 올바른 라이센스 서버에서 서명되었는지 확인합니다.

* RevocationList [.verifySignature를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) 호출하여 [API에 RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 를 제공하기 전에 서명을확인합니다.

   자세한 내용은 RevocationListFactory를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* PolicyUpdateList [.verifySignature를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) 호출하여 `PolicyUpdateList` API에 대한 서명을제공합니다.

   자세한 내용은 PolicyUpdateList를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Adobe에서 게시한 CRL 사용{#consuming-crls-published-by-adobe}

SDK 파섹 이러한 파일에 대한 액세스가 차단되거나 이러한 CRL의 적용이 차단되지 않도록 해야 합니다.

SDK에는 Adobe CRL을 검색할 때 오류를 무시하는 구성 옵션이 있으며, 개발 환경에서만 이 옵션을 적용할 수 있습니다. 프로덕션 환경에서는 라이센스 서버가 Adobe에서 CRL을 검색해야 합니다. 라이센스 서버에서 유효한 CRL을 가져올 수 없는 경우 오류가 발생했습니다.

## Adobe에서 게시한 CRL을 보완하기 위한 CRL 생성{#generating-crls-to-supplement-those-published-by-adobe}

Adobe Primetime DRM 파섹

Primetime DRM SDK는 Adobe CRL을 확인하고 적용합니다. 그러나 Primetime DRM SDK에 CRL을 전달하여 추가 시스템 자격 증명을 취소하는 CRL을 만들어 추가 클라이언트 컴퓨터를 허용하지 않을 수 있습니다. 라이센스를 발행할 때 SDK는 Adobe CRL과 CRL을 확인합니다.

CRL을 생성하려면 RevocationListFactory를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## 롤백 감지 {#rollback-detection}

Adobe Primetime DRM의 구현에서 클라이언트가 상태(예: 재생 창 간격)를 유지해야 하는 비즈니스 규칙을 사용하는 경우 서버가 롤백 카운터를 계속 추적하고 AIR 또는 SWF 화이트리스트를 사용하는 것이 좋습니다.

롤백 카운터는 클라이언트의 대부분의 요청에서 서버로 전송됩니다. Primetime DRM의 구현에 롤백 카운터가 필요하지 않은 경우 무시될 수 있습니다. 그렇지 않으면 서버가 MachineToken.getUniqueId() [를 사용하여 얻은 무작위 컴퓨터 ID와](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())데이터베이스의 현재 카운터 값을 저장하는 것이 좋습니다.

롤백 카운터를 증분하고 추적하는 방법에 대한 자세한 내용은 ClientState [및](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) Rollback 검색을 참조하십시오.

## 라이선스 발행 시 시스템 수 {#machine-count-when-issuing-licenses}

비즈니스 규칙에서 사용자의 컴퓨터 수를 추적해야 하는 경우 라이센스 서버 또는 도메인 서버는 사용자와 연결된 컴퓨터 ID를 저장해야 합니다.

컴퓨터 ID를 추적하는 가장 강력한 방법은 MachineId.getBytes() [](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 메서드에서 반환되는 값을 데이터베이스에 저장하는 것입니다. 새 요청이 수신되면 MachineId.matches()를 사용하여 요청의 컴퓨터 ID를 알려진 컴퓨터 ID와 [비교합니다](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 는 ID 비교를 수행하여 ID가 동일한 컴퓨터를 나타내는지 확인합니다. 이 비교는 시스템 ID가 적은 경우에만 실용적입니다. 예를 들어 도메인에 사용자가 5대의 컴퓨터가 허용되는 경우 데이터베이스를 검색하여 사용자의 사용자 이름과 연결된 컴퓨터 ID를 찾은 다음 비교를 위해 작은 데이터 세트를 얻을 수 있습니다.

이러한 비교는 익명 액세스를 허용하는 배포에는 적합하지 않습니다. 이 경우 MachineId. [getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 를 사용할 수 있습니다. 그러나 사용자가 Flash 및 Adobe AIR® 런타임의 콘텐츠에 액세스하는 경우 이 ID는 같을 수 없습니다.

>[!NOTE]
>
>사용자가 하드 드라이브를 다시 포맷하면 ID가 유지되지 않습니다.

## 재생 보호 {#replay-protection}

재생 보호 기능은 침입자가 라이센스 요청 메시지를 다시 재생하지 못하도록 하여 잠재적으로 클라이언트에 대한 서비스 거부(DoS) 공격을 발생시킵니다.

DoS 공격은 서비스의 합법적인 사용자가 해당 서비스를 사용하지 못하도록 하기 위한 공격자의 시도입니다. 예를 들어 롤백 카운터를 사용하는 재생 공격을 사용하여 DRM 클라이언트가 상태를 롤백했다고 판단하여 계정 일시 중단을 발생시킬 수 있습니다.

재생 보호에 대한 자세한 내용은 AbstractRequestMessage.getMessageId() [ 를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())참조하십시오.

## 신뢰할 수 있는 컨텐츠 패키저 화이트 리스트 유지{#maintain-a-whitelist-of-trusted-content-packagers}

화이트 리스트는 신뢰할 수 있는 엔티티 목록입니다.

컨텐츠 패키저의 경우, 엔티티는 컨텐츠 소유자가 비디오 파일을 패키지화(또는 암호화)하고 DRM 보호 컨텐츠를 생성하도록 신뢰하는 조직입니다. Adobe Primetime DRM을 배포할 때 신뢰할 수 있는 콘텐츠 패키저의 화이트 리스트를 유지 관리해야 합니다. 또한 라이선스를 발급하기 전에 DRM 보호 파일의 DRM 메타데이터에서 컨텐츠 패키저의 ID를 확인해야 합니다.

컨텐츠를 패키지한 엔티티에 대한 정보를 얻는 방법에 대한 자세한 내용은 V2ContentMetaData.getPackagerInfo() [를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo())참조하십시오.

## 인증 토큰 시간 초과{#timeout-for-authentication-tokens}

Adobe Primetime DRM SDK 파섹

인증 토큰 만료가 지정된 경우 인증 요청을 처리할 때 Primetime DRM SDK를 사용합니다. 만료되면 토큰이 더 이상 유효하지 않으므로 사용자가 라이선스 서버에 다시 인증해야 합니다.

인증 요청에 대한 자세한 내용은 AuthenticationHandler를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## 정책 옵션 재정의 {#overriding-policy-options}

라이센스를 발행하면 라이센스 서버가 정책에 지정된 사용 규칙을 무시할 수 있습니다.

정책에서 시작 날짜를 지정하면 해당 시작 날짜 이전에 라이센스가 생성되지 않습니다. 그러나 라이센스가 생성된 후 라이센스의 향후 시작 날짜를 설정할 수 있습니다. 클라이언트는 사용자가 시작 날짜를 피하기 위해 시스템 시간을 앞으로 이동할 수 없도록 할 수 없으므로 이 옵션을 신중하게 사용해야 합니다.