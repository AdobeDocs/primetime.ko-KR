---
title: 암호화된 파일 내용을 검사하는 중
description: 암호화된 파일 내용을 검사하는 중
copied-description: true
exl-id: a8a61d1c-c259-4346-9a71-6741f70697ae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 암호화된 파일 내용을 검사하는 중 {#examining-encrypted-file-content}

Java API를 사용하여 FLV 또는 F4V 파일의 내용을 검사하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고에 언급된 모든 JAR 파일을 포함하십시오. [개발 환경 설정](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 을 참조하십시오.
1. 만들기 `MediaEncrypter` 인스턴스.
1. 암호화된 파일을 `MediaEncrypter.examineEncryptedContent` 메서드, 반환 `KeyMetaData` 개체.
1. 다음 내에 있는 정보를 Inspect: `KeyMetaData` 개체.

암호화된 파일에서 DRM 메타데이터를 추출하는 방법을 보여 주는 샘플 코드는 다음을 참조하십시오. `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리에서
