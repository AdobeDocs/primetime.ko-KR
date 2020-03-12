---
seo-title: 사용 모델 데모 활성화
title: 사용 모델 데모 활성화
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 사용 모델 데모 활성화{#enable-the-usage-model-demo}

1. 패키징 `RI_UsageModelDemo=true` 시 사용자 지정 속성을 지정합니다.

   Media Packager 명령줄 도구를 사용하여 컨텐츠를 패키지하는 경우 다음을 입력합니다.

   ```
   java -jar AdobeMediaPackager.jar [
   
<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true

```
>[!NOTE] {class="- topic/note "}
>
>If you do not activate the optional demo mode at packaging time, the license server issues a license based on the first valid DRM policy it processes.

