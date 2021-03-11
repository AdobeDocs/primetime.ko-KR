---
description: DRM을 구현하려면 컨텐츠 암호화 키 또는 컨텐츠를 암호화하는 CEK, ExpressPlay 서버와의 통신 보호를 위한 고객 인증자, 키 관리 시스템에 저장된 컨텐츠 암호화 키를 식별하는 CEKSID 등 특정 인증서와 키가 필요합니다.
title: 키, ID 및 인증자
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# 키, ID 및 Authenticator{#keys-ids-and-authenticators}

DRM을 구현하려면 컨텐츠 암호화 키 또는 컨텐츠를 암호화하는 CEK, ExpressPlay 서버와의 통신 보호를 위한 고객 인증자, 키 관리 시스템에 저장된 컨텐츠 암호화 키를 식별하는 CEKSID 등 특정 인증서와 키가 필요합니다.

보호된 콘텐츠를 패키징, 라이선스 부여 및 재생하려면 다음 항목이 필요합니다.

## 콘텐츠 암호화 키 {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

CEK(Content Encryption Key)는 컨텐츠 암호화에 사용되는 16바이트 문자열입니다.

**CEK는 무엇입니까?** - CEK는 패키지 사용자가 콘텐츠를 암호화하는 데 사용하는 키입니다. 16바이트 16바이트 16진수 인코딩된 문자열입니다.

**CEK는 어디에서 오나요?** - 사용자(콘텐트 공급자)는 OpenSSL 또는 메모장++과 같은 도구를 사용하여 이 키를 직접 만듭니다. 예:

```
openssl rand 16 -hex > cek_hex_file
```

또는 (Adobe Offline Packager의 경우):

1. 위나 다른 도구를 사용하여 16바이트 16바이트 16진수 인코딩 문자열을 생성합니다. 다음과 같이 표시됩니다.

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. 메모장++을 열고 16바이트 16바이트 16진수 문자열에 붙여 넣습니다.
1. 이 값을 Base64로 16진수 ASCII에서 인코딩하여 [!DNL keyfile.bin]을(를) 만듭니다. ( [](../../multi-drm-workflows/quick-start/package-your-content.md)에서 다룹니다.)

**같은 키, 다른 이름?** - 예, 다음과 같은 다른 곳에서 다른 이름으로 지칭되는 CEK를 볼 수 있습니다.

* ** [!DNL [somefile].bin]** - Adobe Offline Packager가 CEK를 [!DNL [somefile].bin];예: * [!DNL Keyfile.bin]* - Adobe Offline Packager에서 컨텐츠 패키징에 사용하는 컴퓨터의 파일 형식으로 사용하는 CEK입니다.

   임의 CEK 16진수 문자열을 &quot;Base64&quot;로 지정하고 파일(예: [!DNL keyfile.bin])로 저장합니다. 이 문자열은 대개 [!DNL offlinepkgr/] 아래의 [!DNL creds] 디렉토리에 있습니다. Packager 구성 파일(예: Widevine DRM을 위해 패키지하는 경우 [!DNL widevine.xml])에서 다음과 같이 구성 파일의 CEK를 참조하십시오.

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **컨텐츠 키**   `&contentKey=` - 호출(), 오류 메시지, 지원 티켓 및 기타 문서에서 컨텐츠 키라고 하는 CEK를 볼 수도 있습니다.

**언제/어디서 사용합니까?**

1. 우선 포장하는 시스템에서 CEK를 사용할 수 있어야 합니다. 패키징 툴은 CEK를 사용하여 컨텐츠를 암호화합니다.
1. 두 번째, CEK를 KMS(키 관리 시스템)의 일부 형식으로 저장해야 하며, 각 CEK는 자체 [컨텐트 암호화 키](../../multi-drm-workflows/glossary/glossary-cek.md)와 연결되어 있습니다. 고유한 KMS를 만들거나 [ExpressPlay의 키 저장소](https://www.expressplay.com/developer/key-storage/)를 사용할 수 있습니다. 이를 통해 스토어프론트(고객 권한 부여 및 라이선스 토큰 프로비저닝을 처리하는 권한 부여 서버)는 실제 CEK 대신 키 ID를 사용하여 KMS에서 고객을 위한 라이선스 토큰을 가져올 수 있습니다(훨씬 안전함).

## 콘텐츠 암호화 키 저장소 ID {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

CEKSID(Content Encryption Key Storage ID)는 암호화된 비디오 컨텐츠를 해독하는 저장된 키를 고유하게 식별합니다.

**CEKSID 소개** - CEKSID는 CEK(Content Encryption Key)의 고유 식별자입니다. CEK는 보호된 콘텐츠의 잠금을 해제하는 데 필요합니다.CEKSID는 저장된 CEK에 액세스하려면 필요합니다. 설정을 테스트할 때 라이선스 및 재생 검사와 동일한 정보를 사용하는 경우 패키징 시 무작위 CEKSID 및 CEK를 제공할 수 있습니다.

**어디서 오는 거죠?** - 사용자(컨텐츠 제공업체)는 이 ID를 직접 만들거나  [ExpressPlay의 키 ](https://www.expressplay.com/developer/key-storage/) 저장소 등의 서비스를 사용하여 각 CEK에 대한 CEKSID를 생성할 수 있습니다(두 ID 모두 저장). 또한 임의로 생성된 CEKSID를 사용하거나 비즈니스 모델에 맞는 제도를 사용할 수 있습니다. 예를 들어 임의의 16진수 문자열이 아닌 의미 있는 문자열인 CEKSID를 사용할 수 있습니다(ID 이름은 대상, 날짜, 시간 등으로 구성될 수 있음).

**CEKSID는 또 어떤 제품입니까?** - 컨텐츠 ID라고도  *합니다*.

## 고객 인증자 {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

고객 인증자는 ExpressPlay에서 관리자 계정을 설정할 때 얻은 키입니다. 인증자는 ExpressPlay 서버와 통신하는 데 사용됩니다.

**고객 인증자는 무엇입니까?** - 두 명의 고객 인증 기관은 ExpressPlay가 서비스를 등록할 때 등록한 ID 쌍(테스트, 제작 ID 1개)을 구성합니다. ExpressPlay 관리 페이지에서 언제든지 이용할 수 있습니다.
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**언제 사용하나요?** - 라이센스 서버,  [ExpressPlay 키 저장소](https://www.expressplay.com/developer/key-storage/) 및 기타 호출과 같이 ExpressPlay 서버 호출의 모든 호출에 이 매개 변수를 포함합니다.
