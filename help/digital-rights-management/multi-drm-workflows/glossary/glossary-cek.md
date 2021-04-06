---
title: 용어 설명
description: 특별한 정의가 필요한 자주 사용하는 용어.
exl-id: 4e7874f7-c5c0-4f2c-ada2-a0da3ed4d4bf
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 용어 {#glossary}

특별한 정의가 필요한 자주 사용하는 용어.

## 콘텐츠 암호화 키 {#content-encryption-key}

유틸리티로 생성된 CEK(Content Encryption Key)는 이후에 Content Packager에서 보호해야 하는 컨텐츠를 준비할 때 사용됩니다.
이 유틸리티는 16바이트 길이의 16진수 키를 생성합니다.
이 안내서에서는 CEK에 대한 다음과 같은 매개 변수 이름 및 값 이름의 변형을 메모 및 오류 메시지, 파일 및 명령 샘플로 보여 줍니다.

* 콘텐트 키
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

CEK의 파일 이름은 다음과 같이 표시됩니다.

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

CEK 자체는 암호화될 뿐만 아니라 키 관리 시스템에 저장할 수 있습니다. 이 안내서는 저장소 인덱스를 CEK 저장소 ID CEKSID라고 합니다. 키 암호화 키(KEK)라는 용어는 두 번째 수준의 암호화 키를 참조하며, `ek` 용어는 해당 암호화의 값을 나타냅니다.
일부 호출에서는 CEK와 CEK 스토리지 ID CEKSID를 모두 사용하고 저장소에서 검색한 CEK는 호출에서 제공된 CEK와 일치해야 합니다.
FairPlay가 있는 HLS Offline의 경우 만료되도록 설정할 수 있는 `persistentContentKey`도 있습니다.

## 콘텐츠 암호화 키 저장소 ID {#content-encryption-key-storage-id}

CEKSID(Content Encryption Key Storage ID)는 키 관리 시스템에서 컨텐츠 암호화 키를 검색하는 데 사용되는 ID입니다.

CEKSID는
* 키 ID
* 콘텐츠 ID
* `&kid`

## 고객 인증자 {#customer-authenticator}

Express의 API에 대한 요청의 인증 키 요청에는 토큰 요청이 포함될 수 있습니다.
