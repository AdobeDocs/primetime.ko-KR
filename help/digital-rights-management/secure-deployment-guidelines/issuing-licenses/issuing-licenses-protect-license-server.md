---
description: 라이선스를 안전하게 발급하고 있는지 확인해야 합니다. 라이선스 서버를 보호하기 위한 다음 모범 사례를 고려하십시오.
title: 라이센스 서버 보호
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# 라이센스 서버 보호 {#protecting-the-license-server}

라이선스를 안전하게 발급하고 있는지 확인해야 합니다. 라이센스 서버를 보호하기 위한 다음 모범 사례를 고려하십시오.

## 로컬에서 생성된 CRL 사용 {#consuming-locally-generated-crls}

로컬에서 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인하십시오.

다음 API는 목록이 변경되지 않았으며 올바른 라이선스 서버에서 서명했는지 확인합니다.

* 호출 [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) 서명을제공하기 전에 확인하려면 [해지 목록](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 모든 API에

  자세한 내용은 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* 호출 [PolicyUpdateList.verifySign](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) 을(를) 제공하기 전에 서명을 확인하려면 `PolicyUpdateList` 모든 API에

  자세한 내용은 [정책 업데이트 목록](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Adobe에 의해 게시된 CRL 사용{#consuming-crls-published-by-adobe}

SDK는 Adobe에서 게시한 CRL을 주기적으로 다운로드합니다. 이러한 파일에 대한 액세스가 차단되거나 이러한 CRL을 적용할 수 없도록 해야 합니다.

SDK에는 Adobe CRL을 검색할 때 오류를 무시하는 구성 옵션이 있으며 이 옵션은 개발 환경에서만 적용할 수 있습니다. 프로덕션 환경에서는 라이선스 서버가 Adobe에서 CRL을 검색해야 합니다. 라이선스 서버가 유효한 CRL을 가져올 수 없는 경우 오류가 발생했습니다.

## Adobe에 의해 게시된 항목을 보완하기 위해 CRL 생성{#generating-crls-to-supplement-those-published-by-adobe}

Adobe Primetime DRM을 사용하여 Adobe에 의해 게시된 시스템 CRL을 보완하는 CRL을 생성할 수 있습니다.

Primetime DRM SDK는 Adobe CRL을 확인하고 시행합니다. 그러나 CRL을 Primetime DRM SDK에 전달하여 추가 컴퓨터 자격 증명을 취소하는 CRL을 생성하여 추가 클라이언트 컴퓨터를 허용하지 않을 수 있습니다. 라이센스를 발급하면 SDK가 Adobe CRL과 CRL을 확인합니다.

CRL을 생성하려면 다음을 참조하십시오 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## 롤백 감지 {#rollback-detection}

Adobe Primetime Adobe DRM 구현에서 클라이언트가 상태(예: 재생 창 간격)를 유지해야 하는 비즈니스 규칙을 사용하는 경우 서버에서 롤백 카운터를 추적하고 AIR 또는 SWF 허용 목록을 사용하는 것이 좋습니다.

롤백 카운터는 클라이언트의 대부분의 요청에서 서버로 전송됩니다. Primetime DRM 구현에서 롤백 카운터가 필요하지 않은 경우 무시할 수 있습니다. Adobe 그렇지 않으면 서버에서 를 사용하여 가져온 임의의 컴퓨터 ID를 저장하는 것이 좋습니다. [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())및 데이터베이스의 현재 카운터 값입니다.

롤백 카운터를 증가시키고 추적하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 및 롤백 감지입니다.

## 라이선스를 발급할 때 컴퓨터 개수 {#machine-count-when-issuing-licenses}

비즈니스 규칙에서 사용자의 컴퓨터 수를 추적해야 하는 경우 라이선스 서버 또는 도메인 서버는 사용자와 연결된 컴퓨터 ID를 저장해야 합니다.

시스템 ID를 추적하는 가장 강력한 방법은 가 반환하는 값을 저장하는 것입니다. [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 데이터베이스의 메서드입니다. 새 요청이 수신되면 을 사용하여 요청의 시스템 ID를 알려진 시스템 ID와 비교합니다 [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 는 ID를 비교하여 ID가 동일한 컴퓨터를 나타내는지 여부를 확인합니다. 이 비교는 적은 수의 컴퓨터 ID가 있는 경우에만 실용적입니다. 예를 들어, 사용자에게 도메인에 5개의 시스템이 허용된 경우, 데이터베이스에서 사용자의 사용자 이름과 연결된 시스템 ID를 검색하고 비교할 작은 데이터 세트를 얻을 수 있습니다.

익명 액세스를 허용하는 배포에 대해서는 이 비교가 실용적이지 않습니다. 이 경우, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 를 사용할 수 있습니다. 그러나 이 ID는 사용자가 Flash 및 Adobe AIR® 런타임 시 콘텐츠에 액세스하는 경우 동일할 수 없습니다.

>[!NOTE]
>
>사용자가 하드 드라이브를 다시 포맷하는 경우 ID가 유지되지 않습니다.

## 재생 보호 {#replay-protection}

재생 보호는 공격자가 라이선스 요청 메시지를 재생하지 못하도록 하여 클라이언트에 대한 서비스 거부(DoS) 공격을 야기할 수 있습니다.

DoS 공격은 공격자가 서비스의 합법적인 사용자가 해당 서비스를 사용하지 못하도록 시도하는 것입니다. 예를 들어 롤백 카운터를 사용하는 재생 공격은 DRM 클라이언트가 상태를 롤백했다고 생각하도록 라이선스 서버를 &quot;트릭&quot;하는 데 사용할 수 있으며, 이로 인해 계정이 일시 중단됩니다.

재생 보호에 대한 자세한 내용은 다음을 참조하십시오. [AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## 신뢰할 수 있는 컨텐츠 패키지 허용 목록 유지 {#maintain-a-allowlist-of-trusted-content-packagers}

허용 목록은 신뢰할 수 있는 엔티티 목록입니다.

콘텐츠 패키지자의 경우 엔티티는 콘텐츠 소유자가 신뢰하는 조직으로 비디오 파일을 패키지(또는 암호화)하고 DRM 보호 콘텐츠를 만듭니다. Adobe Primetime DRM을 배포할 때 신뢰할 수 있는 콘텐츠 패키지 허용 목록을 유지 관리해야 합니다. 또한 라이선스를 발급하기 전에 DRM 보호 파일의 DRM 메타데이터에서 콘텐츠 패키지 ID를 확인해야 합니다.

콘텐츠를 패키지한 엔티티에 대한 정보를 얻는 방법에 대해 알아보려면 를 참조하십시오. [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## 인증 토큰 시간 제한{#timeout-for-authentication-tokens}

Adobe Primetime DRM SDK에서 생성한 모든 인증 토큰에는 애플리케이션 보안을 보호하기 위한 시간 제한 간격이 있습니다.

인증 토큰에 대한 만료는 인증 요청을 처리할 때 Primetime DRM SDK를 사용하여 지정합니다. 토큰이 만료되면 더 이상 유효하지 않으므로 사용자는 라이선스 서버를 사용하여 다시 인증해야 합니다.

인증 요청에 대한 자세한 내용은 다음을 참조하십시오. [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## 정책 옵션 재정의 {#overriding-policy-options}

라이선스를 발급할 때 라이선스 서버는 정책에 지정된 사용 규칙을 재정의할 수 있습니다.

정책에서 시작 날짜를 지정하면 해당 시작 날짜 이전에 라이센스가 생성되지 않습니다. 그러나 라이센스가 생성된 후 라이센스에서 미래 시작 일자를 설정할 수 있습니다. 이 옵션은 클라이언트가 사용자가 시작 날짜를 우회하기 위해 시스템 시간을 앞으로 이동하는 것을 방지할 수 없으므로 주의하여 사용해야 합니다.
