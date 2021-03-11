---
title: 플레이어에서 XSTS 토큰 설정
description: 플레이어에서 XSTS 토큰 설정
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---


# Xbox360으로의 스트리밍(옵션) {#streaming-to-xboc360}

Primetime DRM은 Xbox360 플랫폼에서 사용할 수 있습니다. 그러나 전체 DRM 정책 권한이 아닌 보호된 스트리밍 사용 사례만 지원됩니다. 장치 도메인 그룹과 같은 비스트리밍 DRM 정책 권한은 지원되지 않습니다. 콘텐츠를 재생하려고 할 때 Xbox360에서 지원되지 않는 권한이 무시됩니다.

Xbox에 대해 지원되는 Primetime DRM 정책 권한은 다음과 같습니다.
* 디지털 출력 보호
* 라이선스 오프라인 캐싱 종료 날짜
* 라이선스 시작 날짜
* 라이선스 종료 날짜
* 재생 창 지속 시간(초)

iOS, Android 또는 데스크탑과 같은 다른 Primetime 플랫폼용으로 이미 패키지화된 경우 콘텐츠를 Xbox 360으로 스트리밍하기 위해 다시 패키지화할 필요가 없습니다.

Xbox360의 한 가지 주의해야 할 점은 M3U8에서 EXT-X-KEY 태그가 나타날 때마다 항상 주요 서버에 연결되어 있어야 한다는 것입니다. DRM 정책 설정(policy.requireKeyServer)을 사용하여 iOS Primetime 비디오 플레이어에서 localhost에서 AES 암호 해독 키를 검색할 수 있는 iOS와 달리 Xbox는 항상 원격 키서버에서 암호 해독 키를 검색합니다. Xbox 앱에서 AES 암호 해독을 검색하도록 지시할 DRM 정책 권한이 없습니다.
키를 로컬 호스트에서 가져옵니다. 이러한 요구 사항으로 인해 EXT-X-KEY 항목은 Primetime Cloud DRM 끝점을 가리키는 M3U8에 있어야 합니다. 이 URL은 OfflinePackager.jar 구성 파일 config_hls.xml에서 &lt;key_url>을 통해 설정됩니다.

콘텐츠를 한 번 패키징하여 모든 Primetime 타겟으로 스트리밍하고 iOS 장치가 원격 키 서버에서 키를 검색하지 않도록 구성한 경우 속성 정책을 포함하는 DRM 정책(예: policy_ios_localkeyserver.pol)을 사용하여 콘텐츠를 패키징할 수 있습니다. iOS 장치는 AES 키를 로컬로 검색할 수 있지만 Xbox 장치는 이 속성을 무시하고 Primetime Cloud DRM 키 서버에 연결을 합니다
암호 해독 키에 사용할 수 있습니다.

>!참고
>
>모든 Xbox360 요청은 사용자 정의 인증/>권한 부여를 사용해야 합니다. 이는 Xbox360 플랫폼에서는 Xbox Live >에서 인증 목적을 위해 Xbox Secure Token Server(XSTS) 토큰을 사용하기 때문입니다.
>Primetime Cloud DRM 라이선스 서버는 XSTS 토큰을 사용하여 Xbox 디바이스와 사용자가 Xbox 디바이스의 무결성을 검증하고 라이선스 요청을 확인합니다. 그러나 XSTS 토큰의 유효성을 검사하려면 Primetime Cloud DRM >에 저장되지 않는 >고객의 Xbox Live 공급업체 키가 필요합니다. 이러한 이유로 Primetime Cloud DRM이 Xbox 360 클라이언트의 라이선스 요청을 받은 경우, Primetime Cloud DRM >은(는) XSTS 토큰을 Primetime 고객의 백엔드 > 인증/권한 부여 서버로 전송합니다. Primetime 고객의 서버
>그런 다음 XSTS 토큰을 구문 분석하여 고객의 애플리케이션 게시자 키를 사용하여 >서명되었는지 확인합니다.
>Xbox360 클라이언트에서 XSTS 토큰을 전달하려면 MediaPlayer.RequestKeyAttribute >event에 대한 응답으로 토큰을 >동기적으로 설정합니다. 자세한 내용은 다음 항목을 참조하십시오.**플레이어에서 XSTS 토큰을 설정합니다.** 샘플 백엔드 인증/권한 부여 서버 >가 사용자 정의 인증 > 권한 부여 디렉토리의 소프트웨어 릴리스에 포함되어 있습니다.XSTS 토큰에 대한 유효성 검사에 대해 여기에서 자세히 설명합니다. **Xbox Live XSTS 토큰 확인.**


## 플레이어 {#set-the-xsts-token-in-your-player}에서 XSTS 토큰을 설정합니다.

Xbox360에서는 `MediaPlayer.RequestKeyAttribute` 이벤트에 대한 응답으로 토큰을 비동기식으로 설정합니다.

XSTS 토큰을 설정합니다.

소프트웨어에 번들로 포함된 샘플 앱은 플레이어에서 XSTS 토큰을 설정하는 방법을 보여줍니다. 다음은 샘플 플레이어의 관련 코드 조각입니다.

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

## Xbox Live XSTS 토큰 유효성 검사 {#xbox-live-xsts-token-validation}

XSTS 요청의 경우 `customerSpecificAuthToken` 필드에 Base64 인코딩된 XSTS 토큰이 포함됩니다. 샘플 `XSTSValidator` 코드는 Base64 디코딩된 토큰에 `EncryptedAssertion` 요소가 있는지 검사합니다.그러나 다른 방법을 사용하여 이러한 요청과 Xbox 이외의 요청을 구분할 수 있습니다. 예를 들어 다른 URL을 사용할 수 있습니다.

응답 메시지에서 반환된 정책은 Xbox 키 요청과 함께 제공된 DRM 메타데이터의 원래 정책을 덮어씁니다. Xbox 클라이언트는 정책 기능의 하위 집합만 지원되며, 이 필드들은 원래 정책을 대체할 유일한 것입니다.

토큰 암호 해독 및 유효성 검사를 지원하는 데 필요한 추가 설정 단계가 있습니다. [!DNL xsts_partner_cert.pfx] 및 [!DNL x_secure_token_service.part.xboxlive.com.cer] 자격 증명을 JKS 형식 키 저장소에 로드해야 합니다. 이 키 저장소를 시스템 속성 `xsts-keystore`으로 백엔드 자격 부여 서버에 제공합니다. 기본적으로 파트너 [!DNL .pfx]의 별칭은 `xsts`이고 토큰 유효성 검사 인증서의 별칭은 `xsts-verify-cert`입니다. 시스템 속성을 사용하여 이러한 속성을 재정의할 수도 있습니다. 마지막으로, 기본값이 없고 키 저장소 암호를 포함하는 시스템 속성 `xsts-keystore-password`이 있습니다. `XSTSValidator` 코드로 읽은 시스템 속성은 아래에 요약되어 있습니다.

| 시스템 속성 | 기본값 | 주석 |
|---|---|---|
| xsts-keystore | xsts.jks | 유효성 검사기에서 사용하는 JKS 형식 키 저장소입니다. |
| xsts-keystore-password |  | 키 저장소에 대한 암호 |
| xsts-alias | xsts | 키 저장소에서 암호 해독 키를 검색하는 데 사용된 별칭 |
| xsts-verify-cert-alias | xsts-verify-cert | 키 저장소에서 유효성 검사 인증서를 검색하는 데 사용되는 별칭 |

## XSTS 유효성 검사기용 JKS 만들기{#create-jks-for-an-xsts-validator}

1. 파트너 [!DNL .pfx] 파일에 있는 개인 인증서의 별칭 이름을 확인합니다.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. [!DNL .pfx]을(를) [!DNL .jks](으)로 변환합니다.

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   여기서 `<alias>`은 1단계에서 발견한 개인 인증서의 별칭 이름입니다.
1. [!DNL x_secure_token_service.part.xboxlive.com.cer]을(를) 가져옵니다.

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. [!DNL xsts.jks]을(를) Tomcat 홈 디렉토리에 배치하고 Tomcat에 대해 `-Dxsts-keystore-password=****`을 정의합니다.

[!DNL xsts_partner_cert.pfx] 및 [!DNL xsts.jks]에서 다른 암호를 사용하는 경우 `jks`에서 `xsts` 암호를 업데이트하여 동일하게 만듭니다.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
