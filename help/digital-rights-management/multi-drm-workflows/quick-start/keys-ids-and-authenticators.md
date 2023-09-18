---
description: DRM을 구현하려면 콘텐츠를 암호화할 콘텐츠 암호화 키 또는 CEK, ExpressPlay 서버와의 통신을 보호하기 위한 고객 인증자, 키 관리 시스템에 저장된 콘텐츠 암호화 키를 식별하기 위한 CEKSID를 포함한 특정 인증서 및 키가 필요합니다.
title: 키, ID 및 인증자
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# 키, ID 및 인증자{#keys-ids-and-authenticators}

DRM을 구현하려면 콘텐츠를 암호화할 콘텐츠 암호화 키 또는 CEK, ExpressPlay 서버와의 통신을 보호하기 위한 고객 인증자, 키 관리 시스템에 저장된 콘텐츠 암호화 키를 식별하기 위한 CEKSID를 포함한 특정 인증서 및 키가 필요합니다.

보호된 콘텐츠를 패키지, 라이선스 및 재생하려면 다음 항목이 필요합니다.

## 컨텐츠 암호화 키 {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

콘텐츠 암호화 키(CEK)는 콘텐츠를 암호화하는 데 사용되는 16바이트 문자열입니다.

**CEK란 무엇입니까?** - CEK는 패키지 작성자가 콘텐츠를 암호화하는 데 사용하는 키입니다. 16바이트의 16진수로 인코딩된 문자열입니다.

**CEK는 어디에서 왔습니까?** - OpenSSL 또는 메모장++과 같은 도구를 사용하여 이 키를 직접 만듭니다. 예:

```
openssl rand 16 -hex > cek_hex_file
```

또는 (Adobe Offline Packager):

1. 위와 같이 또는 다른 도구를 사용하여 16바이트의 16진수로 인코딩된 문자열을 생성합니다. 다음과 같이 표시됩니다.

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. 메모장++ 열고 16바이트 16진수 문자열에 붙여넣습니다.
1. Base64에서 값을 인코딩하여 16진수 ASCII에서 이 값을 변환하여 [!DNL keyfile.bin]. (여기에 설명되어 있음) [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**같은 키, 다른 이름?** - 예, 다음과 같은 다른 위치에서 다른 이름으로 참조되는 CEK를 볼 수 있습니다.

* **!DNL 만들기 [somefile].bin]** - Adobe Offline Packager가 CEK를 [!DNL]로 참조합니다. [somefile].bin]; 예: * [!DNL Keyfile.bin]* - Adobe 오프라인 포장기에서 사용하는 CEK로, 콘텐츠를 포장하는 데 사용하는 시스템의 파일 형식입니다.

  임의의 CEK 16진수 문자열을 &quot;Base64&quot;하고 파일로 저장합니다(예: [!DNL keyfile.bin]), 일반적으로 다음 위치에 있음 [!DNL creds] 아래에 있는 디렉터리 [!DNL offlinepkgr/]. Packager 구성 파일(예: [!DNL widevine.xml] Widevine DRM에 대해 패키지하는 경우 다음과 같이 구성 파일에서 CEK를 참조합니다.

  ```
  <config>  
    <in_path>sample.mp4</in_path>  
    <out_type>dash</out_type>
    <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
    […] 
  </config> 
  ```

* **컨텐츠 키** - 호출에서 콘텐츠 키라고 하는 CEK가 표시될 수도 있습니다( `&contentKey=`), 오류 메시지, 지원 티켓 및 기타 설명서에서 확인할 수 있습니다.

**언제/어디서 사용해야 합니까?**

1. 먼저, 포장을 하고 있는 기계에 CEK가 설치되어 있어야 합니다. 패키징 도구는 CEK를 사용하여 콘텐츠를 암호화합니다.
1. 둘째, CEK를 KMS(키 관리 시스템)의 일부 형태로 저장해야 하며 각 CEK는 자체 CEK와 연결됩니다 [컨텐츠 암호화 키](../../multi-drm-workflows/glossary/glossary-cek.md). 고유한 KMS를 만들거나 [ExpressPlay의 주요 스토리지](https://www.expressplay.com/developer/key-storage/). 이렇게 하면 상점(고객 자격 부여 및 라이선스 토큰 프로비저닝을 처리하는 자격 부여 서버)이 실제 CEK 대신 키 ID를 사용하여 KMS에서 고객에 대한 라이선스 토큰을 가져올 수 있습니다(훨씬 안전함).

## 컨텐츠 암호화 키 저장소 ID {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

컨텐츠 암호화 키 저장소 ID(CEKSID)는 비디오 컨텐츠의 암호화된 부분을 해독하는 저장된 키를 고유하게 식별합니다.

**CEKSID란 무엇입니까?** - CEKSID는 CEK(콘텐츠 암호화 키)에 대한 고유 식별자입니다. CEK는 보호된 콘텐츠의 잠금을 해제해야 합니다. CEKSID는 저장된 CEK에 액세스해야 합니다. 설정을 테스트할 때 라이센스 및 재생 검사에 동일한 정보를 사용하는 한 패키징 시 임의의 CEKSID 및 CEK를 제공할 수 있습니다.

**어디에서 오셨나요?** - 귀하(콘텐츠 공급자)는 이 ID를 직접 생성하거나 다음과 같은 서비스를 사용할 수 있습니다. [ExpressPlay의 주요 스토리지](https://www.expressplay.com/developer/key-storage/) 각 CEK에 대해 CEKSID를 생성하고 두 가지를 모두 저장합니다. 또한 임의로 생성된 CEKSID를 사용하거나 비즈니스 모델에 맞는 스키마를 사용할 수 있습니다. 예를 들어, 임의의 16진수 문자열(ID 이름은 제목, 날짜, 시간 등으로 구성될 수 있음)이 아닌 의미 있는 문자열인 CEKSID를 사용할 수 있습니다.

**CEKSID는 또 뭐에요?** - 경우에 따라 *컨텐츠 ID*.

## 고객 인증자 {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

고객 인증자는 ExpressPlay에서 관리자 계정을 설정할 때 얻는 키입니다. 인증자는 ExpressPlay 서버와의 통신에 사용됩니다.

**고객 인증자는 무엇입니까?** - 두 고객 인증자는 ExpressPlay가 서비스에 등록할 때 등록하는 두 ID(테스트용, 프로덕션용)를 구성합니다. ExpressPlay 관리 페이지에서 언제든지 사용할 수 있습니다.
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**언제 사용해야 합니까?** - ExpressPlay 서버(예: 라이센스 서버)에 대한 모든 호출에 이를 포함합니다. [ExpressPlay 키 저장소](https://www.expressplay.com/developer/key-storage/), 기타 호출.
