---
uuid: 2d927ae8-4c4b-4b64-88b8-9c86430e226c
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 용어 설명 {#glossary}

특수한 정의가 필요한 자주 사용하는 용어.

## 컨텐츠 암호화 키 {#content-encryption-key}

유틸리티에서 생성된 CEK(컨텐츠 암호화 키)는 이후에 보호해야 하는 컨텐츠를 준비할 때 컨텐츠 패키저에서 사용됩니다.
이 유틸리티는 16바이트의 16진수 키를 생성합니다.
이 안내서에서는 CEK에 대한 다음과 같은 매개 변수 이름 및 값 이름의 변형을 메모 및 오류 메시지, 파일 및 명령 샘플로 보여 줍니다.

* 콘텐츠 키
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

CEK의 파일 이름은 다음과 같이 표시됩니다.

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

CEK 자체는 암호화될 뿐만 아니라 키 관리 시스템에 저장할 수 있습니다. 이 안내서는 저장소 인덱스를 CEK 저장소 ID CEKSID로 참조합니다. KEK(Key Encryption Key)라는 용어는 두 번째 수준의 암호화 키를 의미하며, 용어는 해당 암호화의 값을 `ek` 의미합니다.
일부 호출에서는 CEK와 CEK 스토리지 ID CEKSID를 모두 사용하고 저장소에서 검색한 CEK는 호출에서 제공된 CEK와 일치해야 합니다.
FairPlay가 있는 HLS Offline의 경우 만료되도록 설정할 `persistentContentKey` 수 있습니다.

## 컨텐츠 암호화 키 저장소 ID {#content-encryption-key-storage-id}

CEKSID(Content Encryption Key Storage ID)는 키 관리 시스템에서 컨텐츠 암호화 키를 검색하기 위한 ID입니다.

CEKSID는
* 키 ID
* 콘텐츠 ID
* `&kid`

## 고객 인증자 {#customer-authenticator}

Express의 API에 대한 요청의 인증 키 요청에는 토큰에 대한 요청이 포함될 수 있습니다.