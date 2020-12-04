---
seo-title: 암호화된 파일 컨텐츠 검사
title: 암호화된 파일 컨텐츠 검사
uuid: 1b3318f6-0850-43f2-9127-c72ea81a1bdf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 암호화된 파일 내용 검사{#examining-encrypted-file-content}

Java API를 사용하여 암호화된 미디어 파일의 내용을 검사할 수 있습니다.

암호화된 파일 컨텐츠를 검사하려면

1. 개발 환경을 설정하고 모든 JAR 파일을 포함합니다. 프로젝트에 대한 *SDK* 설정을 참조하십시오.
1. `MediaEncrypter` 인스턴스를 만듭니다.
1. 암호화된 파일을 `MediaEncrypter.examineEncryptedContent` 메서드에 전달하여 `KeyMetaData` 개체를 반환합니다.

1. Inspect에 있는 `KeyMetaData` 개체 내의 정보를 표시합니다.

암호화된 파일에서 DRM 메타데이터를 추출하는 방법을 설명하는 샘플 코드는 참조 구현 명령줄 도구 [!DNL samples/] 디렉토리의 `com.adobe.flashaccess.samples.mediapackager.ExamineContent`을 참조하십시오.
