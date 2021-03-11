---
title: 암호화된 파일 컨텐츠 검사
description: 암호화된 파일 컨텐츠 검사
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 암호화된 파일 내용 검사 중 {#examining-encrypted-file-content}

Java API를 사용하여 FLV 또는 F4V 파일의 내용을 검사하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내에 [개발 환경 설정](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)에 언급된 모든 JAR 파일을 포함합니다.
1. `MediaEncrypter` 인스턴스를 만듭니다.
1. 암호화된 파일을 `MediaEncrypter.examineEncryptedContent` 메서드에 전달하여 `KeyMetaData` 객체를 반환합니다.
1. Inspect에서 `KeyMetaData` 개체 내의 정보를 표시합니다.

암호화된 파일에서 DRM 메타데이터를 추출하는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리의 `com.adobe.flashaccess.samples.mediapackager.ExamineContent`을 참조하십시오.
