---
title: 플레이어에서 XSTS 토큰 설정
description: 플레이어에서 XSTS 토큰 설정
copied-description: true
exl-id: 1b83baac-e6a6-4e84-8ea5-07bd7e4afd9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# Xbox360으로 스트리밍(선택 사항) {#streaming-to-xboc360}

Primetime DRM은 Xbox360 플랫폼에서 사용할 수 있습니다. 그러나 DRM 정책 권한의 전체 세트가 아니라 보호된 스트리밍 사용 사례만 지원됩니다. 장치 도메인 그룹과 같은 비스트리밍 DRM 정책 권한은 지원되지 않습니다. 콘텐츠를 재생하려고 할 때 Xbox360에서 지원되지 않는 권한을 무시합니다.

Xbox에서 지원되는 Primetime DRM 정책 권한은 다음과 같습니다.
* 디지털 출력 보호
* 라이선스 오프라인 캐싱 종료 일자
* 라이선스 시작일
* 라이선스 종료일
* 재생 기간(초)

iOS, Android 또는 Desktop과 같은 다른 Primetime 플랫폼용으로 이미 패키징되어 있다면, Xbox360으로 스트리밍하기 위해 콘텐츠를 다시 패키징할 필요가 없을 수도 있습니다.

Xbox360에서 주의해야 할 점은 M3U8에서 EXT-X-KEY 태그가 발생할 때마다 항상 키 서버에 연결해야 한다는 것입니다. DRM 정책 설정(policy.requireKeyServer)이 iOS Primetime 비디오 플레이어가 localhost에서 AES 암호 해독 키를 검색하는 iOS과 달리 Xbox는 항상 원격 키 서버에서 암호 해독 키를 검색하려고 시도합니다 . Xbox 앱이 localhost에서 AES 암호 해독 키를 검색하도록 지시할 수 있는 DRM 정책 권한은 없습니다. 이 요구 사항 때문에 EXT-X-KEY 항목은 Primetime Cloud DRM 끝점을 가리키는 M3U8에 있어야 합니다. 이 URL은 다음을 통해 설정됩니다. &lt;key_url> OfflinePackager.jar 구성 파일 config_hls.xml.

콘텐츠를 한 번 패키징하여 모든 Primetime 대상으로 스트리밍하고 원격 키 서버에서 키를 검색하지 않도록 iOS 장치를 구성하려면 policy.requireKeyServer=false 속성(예: policy_ios_localkeyserver.pol)이 있는 DRM 정책을 사용하여 콘텐츠를 패키징할 수 있습니다. iOS 디바이스는 AES 키를 로컬로 검색하는 반면 Xbox 디바이스는 이 속성을 무시하고 암호 해독 키를 위해 Primetime Cloud DRM 키 서버에 연결됩니다.

>!참고
>
>모든 Xbox360 요청에는 사용자 지정 인증/>자격 부여가 필요합니다.이는 Xbox360 플랫폼에서 Xbox Live는 >인증을 위해 XSTS(Xbox 보안 토큰 서버) 토큰을 사용하기 때문입니다.
>Primetime Cloud DRM 라이선스 서버는 XSTS 토큰을 사용하여 >Xbox 장치 및 라이센스 요청을 수행하는 사용자의 무결성을 확인합니다. 그러나 XSTS 토큰의 유효성을 검사하려면 Primetime Cloud DRM이 저장하지 않는 >고객의 개인 Xbox Live 공급업체 키가 필요합니다. 이러한 이유로 Primetime Cloud DRM이 >Xbox 360 클라이언트로부터 라이센스 요청을 받으면 Primetime Cloud DRM은 >XSTS 토큰을 Primetime 고객의 백엔드 >인증/자격 부여 서버로 전달합니다. Primetime 고객의 서버
>그런 다음 XSTS 토큰을 구문 분석하고 유효성을 검사하여 고객의 애플리케이션 게시자 키를 사용하여 >서명되었는지 확인합니다.
>Xbox360 클라이언트에서 XSTS 토큰을 전달하려면 다음에서 자세히 설명하는 MediaPlayer.RequestKeyAttribute >이벤트에 대한 응답으로 토큰을 >동기적으로 설정합니다. **플레이어에서 XSTS 토큰을 설정합니다.** 샘플 백엔드 인증/권한 부여 서버 >는 사용자 정의 인증 >및 권한 부여 디렉토리의 소프트웨어 릴리스에 포함되어 있습니다.XSTS 토큰의 유효성 확인에 대해서는 다음에서 자세히 설명합니다. **Xbox Live XSTS 토큰 유효성 검사.**


## 플레이어에서 XSTS 토큰 설정 {#set-the-xsts-token-in-your-player}

Xbox360에서는 다음에 대한 응답으로 토큰을 비동기적으로 설정합니다. `MediaPlayer.RequestKeyAttribute` 이벤트.

XSTS 토큰을 설정합니다.

소프트웨어와 함께 번들로 제공되는 샘플 앱은 플레이어에서 XSTS 토큰을 설정하는 방법을 보여 줍니다. 다음은 샘플 플레이어의 관련 코드 조각입니다.

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

XSTS 요청의 경우 `customerSpecificAuthToken` 필드에는 Base64로 인코딩된 XSTS 토큰이 포함됩니다. 샘플 `XSTSValidator` 코드는 Base64 디코딩 토큰을 검사하여 `EncryptedAssertion` 요소. 그러나 다른 방법을 사용하여 이러한 요청과 Xbox 이외의 요청을 구분할 수 있습니다. 예를 들어 다른 URL을 사용할 수 있습니다.

응답 메시지에서 반환된 정책은 Xbox 키 요청과 함께 제공된 DRM 메타데이터의 원래 정책을 덮어씁니다. Xbox 클라이언트는 일부 정책 기능만 지원하며 이 필드만 원래 정책을 무효화합니다.

토큰 암호 해독 및 유효성 검사를 지원하는 데 필요한 추가 설정 단계가 있습니다. 다음을 로드해야 합니다. [!DNL xsts_partner_cert.pfx] 및 [!DNL x_secure_token_service.part.xboxlive.com.cer] 자격 증명을 JKS 형식 키 저장소로 가져와서 백엔드 권한 부여 서버에 시스템 속성으로 제공합니다 `xsts-keystore`. 기본적으로 파트너는 [!DNL .pfx] 에 별칭이 있습니다. `xsts`, 토큰 유효성 검사 인증서에 별칭이 있음 `xsts-verify-cert`. 시스템 속성을 사용하여 재정의할 수도 있습니다. 마지막으로 시스템 속성이 있습니다 `xsts-keystore-password` 에는 기본값이 없으며 키 저장소 암호가 포함되어 있습니다. 에서 읽는 시스템 속성 `XSTSValidator` 코드는 아래에 요약되어 있습니다.

| 시스템 속성 | 기본값 | 댓글 |
|---|---|---|
| xsts-keystore | xsts.jks | 유효성 검사기에서 사용하는 JKS 형식 키 저장소입니다. |
| xsts-keystore-password |  | 키 저장소의 암호 |
| xsts-alias | xsts | 키 저장소에서 암호 해독 키를 검색하는 데 사용되는 앨리어스 |
| xsts-verify-cert-alias | xsts-verify-cert | 키 저장소에서 유효성 검사 인증서를 검색하는 데 사용되는 앨리어스 |

## XSTS 유효성 검사기에 대한 JKS 만들기{#create-jks-for-an-xsts-validator}

1. Partner에 있는 Private Cert의 별칭 이름 확인 [!DNL .pfx] 파일.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 전환 [!DNL .pfx] 끝 [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (여기서 `<alias>` 는 1단계에서 검색한 비공개 인증서의 별칭 이름입니다.)
1. 가져오기 [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] Tomcat 홈 디렉터리에서 다음을 정의합니다. `-Dxsts-keystore-password=****` Tomcat용

If [!DNL xsts_partner_cert.pfx] 및 [!DNL xsts.jks] 다른 암호를 사용하고 있습니다. `xsts` 의 암호 `jks` 그들을 같게 만들려고.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
