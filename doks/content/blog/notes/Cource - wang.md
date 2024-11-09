## git

## [gradle](https://docs.gradle.org/current/userguide/userguide.html)
![image.png](https://raw.githubusercontent.com/shenzaoyi/phot0_bed/main/img_windows20240924152305.png)

### gradle概念
![](https://raw.githubusercontent.com/shenzaoyi/phot0_bed/main/img_windows20240924141554.png)Gradle Build Tool 是一种快速、可靠且适应性强的开源[构建自动化](https://en.wikipedia.org/wiki/Build_automation)工具，具有优雅且可扩展的声明式构建语言。
### 教程
#### 初始化项目
*init*
```bash
gradle init --type java-application  --dsl groovy
```
*项目的结构*
```bash
----                 -------------         ------ ----
d-----         2024/9/23     21:35                .gradle // 缓存目录
d-----         2024/9/23     21:38                app // java应用程序源代码和构建配置
d-----         2024/9/23     21:33                gradle // 包含Gradle Wrapper的配置
														libs.versions.toml,定义依赖项的版本
-a----         2024/9/23     21:33       290 .gitattributes
-a----         2024/9/23     21:33       108 .gitignore
-a----         2024/9/23     21:33       8762 gradlew // mac or linux 执行构建的脚本
-a----         2024/9/23     21:33       2966 gradlew.bat // windows ...
-a----         2024/9/23     21:33       545 settings.gradle // 定义子项目列表
```
*Gradle Wrapper*
Gradle Wrapper 是启动 Gradle 构建的首选方式。Wrapper 会下载（如果需要）然后调用构建中声明的特定版本的 Gradle。
在新创建的项目中，首先查看 Gradle Wrapper 使用的文件。它由适用于 macOS 和 Linux 的 shell 脚本组成以及适用于 Windows 的批处理脚本。
这些脚本允许您运行 Gradle 构建，而无需在系统上安装 Gradle。它还有助于确保不同开发人员以及本地和 CI 计算机之间的构建使用相同版本的 Gradle。
```bash
./gradlew build
.\gradlew.bat build
```
1. 配置文件
```bash
rootProject.name = 'gradle_tutorial'
include('app')
// include app, app就是子项目(sub project)
```
3. 构建脚本： 定义插件，依赖，任务等
```gradle
plugins {
    // Apply the application plugin to add support for building a CLI application in Java.
    id 'application'
}
repositories {
    // Use Maven Central for resolving dependencies.
    mavenCentral()
}
dependencies {
    // Use JUnit Jupiter for testing.
    testImplementation libs.junit.jupiter
    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
    // This dependency is used by the application.
    implementation libs.guava
}
java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(21)
    }
}
application {
    // Define the main class for the application.
    mainClass = 'org.example.App'
}
tasks.named('test') {
    // Use JUnit Platform for unit tests.
    useJUnitPlatform()
}
```
#### [任务](https://docs.gradle.org/current/userguide/more_about_tasks.html#sec:developing_tasks)
任务代表构建执行的一些**独立工作单元，例如编译类、创建 JAR、生成 Javadoc 或将档案发布到存储库。**
```bash
./gradlew tasks // 查看所有任务
./gradlew tasks --all
./gradlew test // 调用test任务并检查输出
```
**开发任务**
在开发 Gradle 任务时，
1. 使用现有的 Gradle 任务类型，例如`Zip`、`Copy`或`Delete`
2. 创建自己的 Gradle 任务类型，例如`MyResolveTask`或`CustomTaskUsingToolchains`。
任务类型只是 Gradle[`Task`](https://docs.gradle.org/current/javadoc/org/gradle/api/Task.html)类的子类。
对于 Gradle 任务，有三种状态需要考虑：
1. **注册**一个任务 - 在你的构建逻辑中使用一个任务（由你实现或由 Gradle 提供）。
2. **配置**任务——定义已注册任务的输入和输出。
3. **执行**任务——创建自定义任务类（即自定义类类型）。

ps: 
gradle默认安装目录在C:/Users/<name>/.gradle,记得删除。