# jitsi-meet-plugin
## 解决汉化问题
更换SDK依赖，手动编译jitsi-meet-sdk,并更新为公有库，在jitsi-meet库中依赖新编译的sdk
## 中文支持文档
持续更新中
## 安卓sdk生成与集成
Jitsi Meet SDK for Android 依赖的第三方 React Native模块由 NPM 以源代码或二进制形式下载。这些需要组装到 Maven 工件中，然后发布到您本地的 Maven 存储库。提供了一个脚本来促进这一点。从 jitsi-meet 项目存储库的根目录，运行：

```./android/scripts/release-sdk.sh /tmp/repo```
/tmp/repo在此示例中，这将构建 SDK 及其所有依赖项并将其发布到指定的 Maven 存储库 ( )。

您现在可以使用这些工件了。在您的项目中，将您在上面使用的 Maven 存储库 ( /tmp/repo) 添加到您的顶级build.gradle文件中：

```allprojects {
    repositories {
        maven { url "file:/tmp/repo" }
        google()
        jcenter()
    }
}

```
```maven { url "https://github.com/jitsi/jitsi-maven-repository/raw/master/releases" }```发布所有子项目时，您可以使用本地存储库替换 Jitsi 存储库 ( ) 。如果您没有这样做，则必须添加两个存储库。确保首先列出您的本地存储库！

然后，将依赖项定义org.jitsi.react:jitsi-meet-sdk到build.gradle模块的文件中：

```implementation ('org.jitsi.react:jitsi-meet-sdk:+') { transitive = true }```
请注意，不需要显式添加其他依赖项，因为它们将作为jitsi-meet-sdk
