---
description: 'null'
seo-description: 'null'
seo-title: 플레이어에서 XSTS 토큰 설정
title: 플레이어에서 XSTS 토큰 설정
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: c37061c116b8a6bc8ce085dc89dc8aadd0a2e490

---


# Xbox360으로 스트리밍(선택 사항) {#streaming-to-xboc360}

Primetime DRM은 Xbox360 플랫폼에서 사용할 수 있습니다. 그러나 보호된 스트리밍 사용 사례만 지원되며 전체 DRM 정책 권한은 지원되지 않습니다. 장치 도메인 그룹과 같은 비스트리밍 DRM 정책 권한은 지원되지 않습니다. 콘텐츠를 재생하려고 할 때 Xbox360은 지원되지 않는 권한을 무시합니다.

Xbox에 대해 지원되는 Primetime DRM 정책 권한은 다음과 같습니다.
* 디지털 출력 보호
* 라이선스 오프라인 캐싱 종료 날짜
* 라이선스 시작 날짜
* 라이선스 종료 날짜
* 재생 창 지속 시간(초)

iOS, Android 또는 데스크탑과 같은 다른 Primetime 플랫폼용으로 이미 패키지된 경우 Xbox360으로 스트리밍하기 위해 콘텐츠를 다시 패키지화할 필요가 없습니다.

Xbox360의 한 가지 단점은 M3U8에서 EXT-X-KEY 태그가 나타날 때마다 항상 키 서버에 연결되어야 한다는 것입니다. DRM 정책 설정(policy.requireKeyServer)을 사용하면 iOS Primetime 비디오 플레이어에서 로컬 호스트에서 AES 암호 해독 키를 검색할 수 있는 iOS와 달리 Xbox는 항상 원격 키 서버에서 암호 해독 키를 검색합니다. localhost에서 AES 암호 해독 키를 검색하도록 Xbox 앱에 지시할 수 있는 DRM 정책이 없습니다. 이러한 요구 사항으로 인해 EXT-X-KEY 항목은 Primetime Cloud DRM 끝점을 가리키는 M3U8에 있어야 합니다. 이 URL은 OfflinePackager.jar 구성 파일 config_hls.xml에서 &lt;key_url>을 통해 설정됩니다.

컨텐츠를 한 번 패키지하여 모든 Primetime 타겟으로 스트리밍하고 iOS 장치가 원격 키 서버에서 키를 검색하지 않도록 구성하는 경우 속성 정책이 있는 DRM 정책(예: policy_ios_localkeyserver.pol)을 사용하여 컨텐츠를 패키지할 수 있습니다. iOS 장치가 AES 키를 로컬로 검색하는 동안 Xbox 장치는 이 속성을 무시하고 암호 해독 키를 위해 Primetime Cloud DRM 키 서버에 연결합니다.

>!참고
>
>모든 Xbox360 요청은 사용자 정의 인증/>권한 부여를 사용해야 합니다. 이는 Xbox360 플랫폼에서 Xbox Live >는 >인증 목적으로 Xbox 보안 토큰 서버(XSTS) 토큰을 사용하기 때문입니다.
>Primetime Cloud DRM 라이선스 서버는 XSTS 토큰을 사용하여 Xbox 디바이스와 사용자가 라이선스 요청을 수행할 때 무결성을 >확인합니다. 그러나 XSTS 토큰의 유효성을 검사하려면 >고객의 개인 Xbox Live 공급업체 키가 필요합니다. Primetime Cloud DRM >은(는) 저장되지 않습니다. 이로 인해 Primetime Cloud DRM이 Xbox 360 클라이언트의 라이선스 요청을 받은 경우 Primetime Cloud DRM은 XSTS 토큰을 Primetime 고객의 백엔드 > 인증/권한 부여 서버로 전달합니다. Primetime 고객의 서버
>그런 다음 XSTS 토큰을 구문 분석하여 고객의 애플리케이션 게시자 키를 사용하여 >서명되었는지 확인합니다.
>Xbox360 클라이언트에서 XSTS 토큰을 전달하려면 MediaPlayer.RequestKeyAttribute >event에 대한 응답으로 토큰을 >동기식으로 설정합니다. 자세한 내용은 여기에 설명되어 있습니다.플레이어에서 **XSTS 토큰을 설정합니다.** 샘플 백엔드 인증/권한 부여 서버 >가 사용자 정의 인증 > 권한 부여 디렉토리의 소프트웨어 릴리스에 포함되어 있습니다.XSTS 토큰의 유효성 검사에 대해 여기에서 자세히 설명합니다.Xbox **Live XSTS 토큰 유효성 검사.**


## 플레이어에서 XSTS 토큰 설정 {#set-the-xsts-token-in-your-player}

Xbox 360에서는 `MediaPlayer.RequestKeyAttribute` 이벤트에 대한 응답으로 토큰을 비동기식으로 설정합니다.

XSTS 토큰을 설정합니다.

소프트웨어와 함께 번들로 제공되는 샘플 앱은 플레이어에서 XSTS 토큰을 설정하는 방법을 보여줍니다. 다음은 샘플 플레이어의 관련 코드 조각입니다.

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

XSTS 요청의 경우 `customerSpecificAuthToken` 필드에 Base64 인코딩 XSTS 토큰이 포함됩니다. 샘플 `XSTSValidator` 코드는 Base64 디코딩된 토큰을 검사하여 `EncryptedAssertion` 요소가 있는지 확인합니다.그러나 다른 방법을 사용하여 이러한 요청과 Xbox가 아닌 요청을 구분할 수 있습니다. 예를 들어 다른 URL을 사용할 수 있습니다.

응답 메시지에서 반환된 정책은 Xbox 키 요청과 함께 제공된 DRM 메타데이터의 원래 정책을 덮어씁니다. Xbox 클라이언트는 정책 기능의 하위 집합만 지원되며, 이 필드만 원래의 정책을 재정의할 수 있습니다.

토큰 암호 해독 및 유효성 검사를 지원하는 데 필요한 추가 설정 단계가 있습니다. JKS 형식 키 저장소에 [!DNL xsts_partner_cert.pfx] 및 [!DNL x_secure_token_service.part.xboxlive.com.cer] 자격 증명을 로드해야 합니다. 그러면 백엔드 자격 부여 서버에 시스템 속성으로 제공할 수 `xsts-keystore`있습니다. 기본적으로 파트너는 [!DNL .pfx] 별칭을 `xsts`가지며 토큰 유효성 검사 인증서에 별칭이 `xsts-verify-cert`있습니다. 시스템 속성을 사용하여 이러한 설정을 재정의할 수도 있습니다. 마지막으로, 기본값이 `xsts-keystore-password` 없고 키 저장소 암호가 포함된 시스템 속성이 있습니다. 코드가 읽는 시스템 속성은 `XSTSValidator` 아래에 요약되어 있습니다.

| 시스템 속성 | 기본값 | 주석 |
|---|---|---|
| xsts-keystore | xsts.jks | 유효성 검사기에서 사용하는 JKS 형식 키 저장소입니다. |
| xsts-keystore-password |  | 키 저장소 암호 |
| xsts-alias | xsts | 키 저장소에서 암호 해독 키를 검색하는 데 사용되는 별칭 |
| xsts-verify-cert-alias | xsts-verify-cert | 키 저장소에서 유효성 검사 인증서를 검색하는 데 사용되는 별칭 |

## XSTS 유효성 검사기용 JKS 만들기{#create-jks-for-an-xsts-validator}

1. 파트너 [!DNL .pfx] 파일에 있는 개인 인증서의 별칭 이름을 확인합니다.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 변환 [!DNL .pfx] 대상 [!DNL .jks]

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (여기서 `<alias>` 는 1단계에서 발견한 개인 인증서의 별칭 이름입니다.)
1. 가져오기를 [!DNL x_secure_token_service.part.xboxlive.com.cer]참조하십시오.

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Tomcat 홈 [!DNL xsts.jks] 디렉토리에 넣고 Tomcat에 `-Dxsts-keystore-password=****` 대해 정의합니다.

다른 암호를 [!DNL xsts_partner_cert.pfx] 사용하고 [!DNL xsts.jks] 있는 경우 암호를 `xsts` 업데이트하여 암호를 동일하게 `jks` 만듭니다.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
