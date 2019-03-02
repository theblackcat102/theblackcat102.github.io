
# Firebase Android build Exception Error

最近興致勃勃的在專案加入Firebase 整合NoSQL 資料時，將gradle 都設置好以後，點擊同步Gradle 時出現了Exception Error 問題….@@

gradle Console 出現Error 如下

    FAILURE: Build failed with an exception.

    * What went wrong:
    Execution failed for task ‘:app:transformResourcesWithMergeJavaResForDebug’.
    > com.android.build.api.transform.TransformException: com.android.builder.packaging.DuplicateFileException: Duplicate files copied in APK META-INF/LICENSE
     File1: /Users/theblackcat/.gradle/caches/modules-2/files-2.1/com.fasterxml.jackson.core/jackson-annotations/2.2.2/285cb9c666f0f0f3dd8a1be04e1f457eb7b15113/jackson-annotations-2.2.2.jar
     File2: /Users/theblackcat/.gradle/caches/modules-2/files-2.1/com.fasterxml.jackson.core/jackson-core/2.2.2/d20be6a5ddd6f8cfd36ebf6dea329873a1c41f1b/jackson-core-2.2.2.jar
     File3: /Users/theblackcat/.gradle/caches/modules-2/files-2.1/com.fasterxml.jackson.core/jackson-databind/2.2.2/3c8f6018eaa72d43b261181e801e6f8676c16ef6/jackson-databind-2.2.2.jar

    * Try:
    Run with — stacktrace option to get the stack trace. Run with — info or — debug option to get more log output.

感覺跟Firebase 只用到的 fasterxml 插件有關係。然而Gradle Build Message 卻是如下：

    Error:Execution failed for task ‘:app:transformResourcesWithMergeJavaResForDebug’.
    > com.android.build.api.transform.TransformException: com.android.builder.packaging.DuplicateFileException: Duplicate files copied in APK META-INF/LICENSE
     File1: /Users/theblackcat/.gradle/caches/modules-2/files-2.1/com.fasterxml.jackson.core/jackson-annotations/2.2.2/285cb9c666f0f0f3dd8a1be04e1f457eb7b15113/jackson-annotations-2.2.2.jar
     File2: /Users/theblackcat/.gradle/caches/modules-2/files-2.1/com.fasterxml.jackson.core/jackson-core/2.2.2/d20be6a5ddd6f8cfd36ebf6dea329873a1c41f1b/jackson-core-2.2.2.jar
     File3: /Users/theblackcat/.gradle/caches/modules-2/files-2.1/com.fasterxml.jackson.core/jackson-databind/2.2.2/3c8f6018eaa72d43b261181e801e6f8676c16ef6/jackson-databind-2.2.2.jar

這端“Duplicate files copied in APK META-INF/LICENSE”的意思是感覺似乎是檔案出現衝突？

於是我將 .gradle/caches 清空，再次build gradle 也一樣噴出一樣的Exception Error…

那麼如果exclude 他們呢？在app:gradle 中的android 底下添加這段：

    android{
    ...
        packagingOptions {
              exclude 'META-INF/NOTICE' // will not include NOTICE file
              exclude 'META-INF/LICENSE' // will not include LICENSE file
              exclude 'META-INF/notice'
              exclude 'META-INF/notice.txt'
              exclude 'META-INF/license'
              exclude 'META-INF/license.txt'
    }

再次build 以後，問題消失了，並且firebase 能順利操作。

雖然不知道這方法到底正確不正確，算是一個小繞道吧？但總算解決了檔案衝突的問題。
