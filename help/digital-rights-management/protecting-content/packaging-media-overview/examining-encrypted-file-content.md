---
title: 암호화된 파일 내용을 검사하는 중
description: 암호화된 파일 내용을 검사하는 중
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 암호화된 파일 내용을 검사하는 중{#examining-encrypted-file-content}

Java API를 사용하여 암호화된 미디어 파일의 내용을 검사할 수 있습니다.

암호화된 파일 내용을 검사하려면 다음을 수행하십시오.

1. 개발 환경을 설정하고 모든 JAR 파일을 포함합니다. 다음을 참조하십시오 *SDK 설정* 을 참조하십시오.
1. 만들기 `MediaEncrypter` 인스턴스.
1. 암호화된 파일을 `MediaEncrypter.examineEncryptedContent` 메서드, 반환 `KeyMetaData` 개체.

1. 다음 내에 있는 정보를 Inspect: `KeyMetaData` 개체.

암호화된 파일에서 DRM 메타데이터를 추출하는 방법을 설명하는 샘플 코드는 다음을 참조하십시오. `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 참조 구현 명령줄 도구 [!DNL samples/] 디렉토리.
