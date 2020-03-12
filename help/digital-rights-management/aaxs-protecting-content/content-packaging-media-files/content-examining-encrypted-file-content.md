---
seo-title: 암호화된 파일 컨텐츠 검사
title: 암호화된 파일 컨텐츠 검사
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 암호화된 파일 컨텐츠 검사 {#examining-encrypted-file-content}

Java API 파섹

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 [설정에 언급된 모든 JAR 파일을](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 포함합니다.
1. 인스턴스를 `MediaEncrypter` 만듭니다.
1. 암호화된 파일을 `MediaEncrypter.examineEncryptedContent` 메서드로 전달하여 `KeyMetaData` 개체를 반환합니다.
1. 개체 내의 정보를 `KeyMetaData` 검사합니다.

암호화된 파일에서 DRM 메타데이터를 추출하는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 &quot;samples&quot; `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 디렉토리에서 을 참조하십시오.
