---
description: '라이선스를 안전하게 발급해야 합니다. 라이센스 서버를 보호하기 위한 이러한 모범 사례를 고려합니다. '
seo-description: '라이선스를 안전하게 발급해야 합니다. 라이센스 서버를 보호하기 위한 이러한 모범 사례를 고려합니다. '
seo-title: 라이센스 서버 보호
title: 라이센스 서버 보호
uuid: 7b5de17d-d0a7-41df-9651-4ff51c9965c6
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---


# 라이센스 서버 보호 {#protecting-the-license-server}

라이선스를 안전하게 발급해야 합니다. 라이센스 서버를 보호하기 위한 다음 우수 사례를 고려하십시오.

## 로컬에서 생성된 CRL 소비 {#consuming-locally-generated-crls}

로컬에서 생성된 CRL(인증서 해지 목록) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인합니다.

다음 API는 목록이 훼손되지 않았고 목록이 올바른 라이센스 서버에서 서명되었는지 확인합니다.

* API에 [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) .verifySignature를 [호출하여](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 서명을 확인합니다.

   자세한 내용은 RevocationListFactory [를 참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* PolicyUpdateList.verifySignature [를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) 호출하여 API에 서명을 제공하기 전에 서명 `PolicyUpdateList` 을 확인합니다.

   자세한 내용은 PolicyUpdateList를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Adobe에서 게시한 CRL 사용{#consuming-crls-published-by-adobe}

SDK는 Adobe가 게시한 CRL을 정기적으로 다운로드합니다. 이러한 파일에 대한 액세스가 차단되거나 이러한 CRL의 적용이 차단되지 않도록 해야 합니다.

SDK에는 Adobe CRL을 검색할 때 오류를 무시하는 구성 옵션이 있으며, 이 옵션은 개발 환경에서만 적용할 수 있습니다. 프로덕션 환경에서 라이센스 서버는 Adobe에서 CRL을 검색해야 합니다. 라이센스 서버에서 유효한 CRL을 가져올 수 없는 경우 오류가 발생했습니다.

## Adobe에서 게시한 CRL을 보완하기 위해 CRL 생성{#generating-crls-to-supplement-those-published-by-adobe}

Adobe Primetime DRM을 사용하여 Adobe에서 게시한 시스템 CRL을 보완하는 CRL을 만들 수 있습니다.

Primetime DRM SDK는 Adobe CRL을 확인하고 적용합니다. 그러나 CRL을 Primetime DRM SDK에 전달하여 추가 시스템 자격 증명을 호출하는 CRL을 만들어 추가 클라이언트 컴퓨터를 허용하지 않을 수 있습니다. 라이센스를 발급하면 SDK가 Adobe CRL과 CRL을 확인합니다.

CRL을 생성하려면 RevocationListFactory를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## 롤백 감지 {#rollback-detection}

Adobe Primetime DRM의 구현에서 클라이언트가 상태(예: 재생 창 간격)를 유지해야 하는 비즈니스 규칙을 사용하는 경우 서버가 롤백 카운터를 계속 추적하고 AIR 또는 SWF 목록 허가를 사용하는 것이 좋습니다.

롤백 카운터는 클라이언트의 대부분의 요청에 따라 서버로 전송됩니다. Primetime DRM을 구현할 때 롤백 카운터가 필요하지 않은 경우 무시할 수 있습니다. 그렇지 않은 경우, 서버가 [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())및 데이터베이스의 현재 카운터 값을 사용하여 얻은 임의의 컴퓨터 ID를 저장하는 것이 좋습니다.

롤백 카운터를 증가시키고 추적하는 방법에 대한 자세한 내용은 ClientState 및 [롤백](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 검색을 참조하십시오.

## 라이선스 발행 시 컴퓨터 수 {#machine-count-when-issuing-licenses}

비즈니스 규칙에서 사용자의 컴퓨터 수를 추적해야 하는 경우 라이선스 서버 또는 도메인 서버는 사용자와 연관된 컴퓨터 ID를 저장해야 합니다.

컴퓨터 ID를 추적하는 가장 강력한 방법은 데이터베이스에 [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) 메서드에서 반환되는 값을 저장하는 것입니다. 새 요청을 받으면 MachineId.matches()를 사용하여 요청의 컴퓨터 ID를 알려진 컴퓨터 ID와 [비교합니다](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) 는 ID를 비교하여 ID가 동일한 컴퓨터를 나타내는지 확인합니다. 이 비교는 시스템 ID가 적은 경우에만 실용적입니다. 예를 들어 도메인에 5대의 컴퓨터가 허용되는 경우 데이터베이스를 검색하여 사용자의 사용자 이름과 연결된 시스템 ID를 찾은 다음 비교를 위해 작은 데이터 세트를 얻을 수 있습니다.

이러한 비교는 익명 액세스를 허용하는 배포에는 적합하지 않습니다. 이 경우 [MachineId.getUniqueID()를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) 사용할 수 있습니다. 그러나 사용자가 Flash 및 Adobe AIR® 런타임의 콘텐츠에 액세스하는 경우 이 ID는 같을 수 없습니다.

>[!NOTE]
>
>사용자가 하드 드라이브를 다시 포맷하면 ID가 유지되지 않습니다.

## 재생 보호 {#replay-protection}

재생 보호 기능은 침입자가 라이센스 요청 메시지를 다시 재생하지 못하도록 하여 잠재적으로 클라이언트에 대한 서비스 거부(DoS) 공격을 야기합니다.

DoS 공격은 서비스의 합법적인 사용자가 해당 서비스를 사용하지 못하도록 하기 위한 공격자의 시도입니다. 예를 들어, 롤백 카운터를 사용하는 재생 공격을 사용하여 라이센스 서버를 DRM 클라이언트가 해당 상태를 롤백하여 계정 일시 중단을 발생시킬 수 있다고 생각하도록 &quot;트릭&quot;할 수 있습니다.

재생 보호에 대한 자세한 내용은 AbstractRequestMessage.getMessageId() [ 를 참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## 신뢰할 수 있는 컨텐츠 패키저 허용 목록 유지 관리{#maintain-a-allowlist-of-trusted-content-packagers}

허용 목록은 신뢰할 수 있는 엔티티 목록입니다.

컨텐츠 패키저의 경우, 개체는 컨텐츠 소유자가 비디오 파일을 패키지화(또는 암호화)하고 DRM으로 보호된 컨텐츠를 만드는 것으로 신뢰하는 조직입니다. Adobe Primetime DRM을 배포할 때는 신뢰할 수 있는 콘텐츠 패키저의 허용 목록을 유지해야 합니다. 또한 라이선스를 발급하기 전에 DRM 보호 파일의 DRM 메타데이터에서 컨텐츠 패키저 ID를 확인해야 합니다.

컨텐츠를 패키지한 엔터티에 대한 정보를 얻는 방법을 알아보려면 [V2ContentMetaData.getPackagerInfo()를 참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## 인증 토큰에 대한 시간 초과{#timeout-for-authentication-tokens}

Adobe Primetime DRM SDK로 생성된 모든 인증 토큰은 애플리케이션 보안을 보호하기 위해 시간 초과 간격이 있습니다.

인증 요청을 처리할 때 인증 토큰 만료가 Primetime DRM SDK를 사용하십시오. 만료되면 토큰이 유효하지 않으므로 사용자가 라이선스 서버에 다시 인증해야 합니다.

인증 요청에 대한 자세한 내용은 AuthenticationHandler를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## 정책 옵션 무시 {#overriding-policy-options}

라이센스를 발행하면 라이센스 서버가 정책에 지정된 사용 규칙을 무시할 수 있습니다.

정책에서 시작 날짜를 지정하면 해당 시작 날짜 이전에 라이센스가 생성되지 않습니다. 그러나 라이센스가 생성된 후 라이센스에서 향후 시작 날짜를 설정할 수 있습니다. 클라이언트는 사용자가 시작 날짜를 피하기 위해 시스템 시간을 앞으로 이동할 수 없도록 할 수 없기 때문에 이 옵션은 주의해서 사용해야 합니다.