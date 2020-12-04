---
seo-title: 암호화된 파일 컨텐츠 검사
title: 암호화된 파일 컨텐츠 검사
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 암호화된 파일 내용 검사 중 {#examining-encrypted-file-content}

Java API를 사용하여 FLV 또는 F4V 파일의 내용을 검사하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내에 개발 환경 설정[에 언급된 모든 JAR 파일을 포함합니다.](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)
1. `MediaEncrypter` 인스턴스를 만듭니다.
1. 암호화된 파일을 `MediaEncrypter.examineEncryptedContent` 메서드에 전달하여 `KeyMetaData` 개체를 반환합니다.
1. Inspect에 있는 `KeyMetaData` 개체 내의 정보를 표시합니다.

암호화된 파일에서 DRM 메타데이터를 추출하는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리의 `com.adobe.flashaccess.samples.mediapackager.ExamineContent`을 참조하십시오.
