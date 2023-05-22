---
title: 사용 모델 데모 활성화
description: 사용 모델 데모 활성화
copied-description: true
exl-id: 5d546f1a-ebf6-4c93-9a73-fa812cd71086
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# 사용 모델 데모 활성화{#enable-the-usage-model-demo}

1. 사용자 지정 속성 지정 `RI_UsageModelDemo=true` 포장 시간에.

   Media Packager 명령줄 도구를 사용하여 콘텐츠를 패키지하는 경우 다음을 입력합니다.

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>패키징 시간에 선택적 데모 모드를 활성화하지 않으면 라이센스 서버가 처리하는 첫 번째 유효한 DRM 정책을 기반으로 라이센스가 발급됩니다.
