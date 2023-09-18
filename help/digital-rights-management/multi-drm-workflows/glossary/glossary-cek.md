---
title: 용어집
description: 특수 정의가 필요한 자주 사용하는 용어입니다.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 용어집 {#glossary}

특수 정의가 필요한 자주 사용하는 용어입니다.

## 컨텐츠 암호화 키 {#content-encryption-key}

유틸리티에서 생성된 콘텐츠 암호화 키(CEK)는 이후 콘텐츠 패키지에서 보호해야 하는 콘텐츠를 준비할 때 사용됩니다.
이 유틸리티는 16바이트 길이의 16진수로 키를 생성합니다.
이 안내서에서는 참고 및 오류 메시지, 파일 및 명령 샘플에서 CEK에 대한 매개 변수 이름과 값 이름의 다음과 같은 변형을 보여 줍니다.

* 콘텐츠 키
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

CEK의 파일 이름은 다음과 같이 표시됩니다.

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

CEK 자체는 암호화될 뿐만 아니라 키 관리 시스템에 저장될 수 있다. 이 안내서에서는 저장소 인덱스를 CEK 저장소 ID CEKSID로 참조합니다. 키 암호화 키(KEK)라는 용어는 두 번째 수준의 암호화 키를 의미하며, `ek` 는 해당 암호화의 값을 나타냅니다.
일부 호출은 CEK와 CEK 저장소 ID CEKSID를 모두 사용하며 저장소에서 검색된 CEK는 호출에 제공된 CEK와 일치해야 합니다.
FairPlay를 사용하는 HLS Offline의 경우 `persistentContentKey` 만료되도록 설정할 수 있습니다.

## 컨텐츠 암호화 키 저장소 ID {#content-encryption-key-storage-id}

컨텐츠 암호화 키 저장소 ID(CEKSID)는 키 관리 시스템에서 컨텐츠 암호화 키를 검색하기 위한 ID입니다.

CEKSID는
* 키 ID
* 컨텐츠 ID
* `&kid`

## 고객 인증자 {#customer-authenticator}

Expressplay API 요청에 대한 인증을 위한 키입니다. 요청에는 토큰에 대한 요청이 포함될 수 있습니다.
