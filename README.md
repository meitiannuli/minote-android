# 小米便签（Android Studio 版）

基于小米便签开源代码迁移到 Android Studio 的可构建、可维护版本。

## 项目简介

本项目源自小米便签（MiNotes）开源代码，原项目结构较旧，无法直接在现代
Android Studio 中构建运行。本仓库在保留原有功能的前提下，完成了向标准
Android Studio 工程结构的迁移，使其可以正常编译、调试和二次开发。

## 项目来源

- 原始代码：小米便签开源版本（`Notes-master`）
- 迁移目标：可在 Android Studio 中构建、运行、维护

## 相比原版的改动

1. **构建系统**
   新增 Gradle Kotlin DSL 构建配置（`build.gradle.kts`、`settings.gradle.kts`、
   `gradle/wrapper/` 等），替代原有的旧式构建方式。

2. **项目结构**
   整合为标准 Android Studio 工程结构，源码与资源归入 `app/` 模块。

3. **语法适配**
   将 `NotesListActivity`、`NoteEditActivity`、`GTaskASyncTask` 中的
   `switch-case`（用于判断 `R.id.xxx`）改为 `if-else`。
   原因：新版 Android Gradle Plugin 中 `R` 类字段不再是编译期常量，
   `switch-case` 无法通过编译。
   **改动为语义等价的语法转换，未修改任何业务逻辑。**

4. **依赖路径**
   `httpclient`、`httpcore` 等依赖以本地 jar 方式引入，路径已由绝对路径改为
   相对路径，保证在不同机器上均可构建。

## 环境要求

- Android Studio（建议较新版本）
- JDK 17 或以上
- Gradle（由 `gradle/wrapper/` 提供，无需单独安装）

## 构建与运行

```bash
# 命令行构建 Debug 版
./gradlew assembleDebug

# 或在 Android Studio 中
# 直接打开项目，等待 Gradle 同步完成后点击 Run
```

## 分支说明

- `main`：稳定版本
- `develop`：日常开发、调试与功能扩展

开发新功能时，建议从 `develop` 切出 `feature/xxx` 分支，完成后合并回 `develop`。

## 仓库地址

- GitHub：https://github.com/meitiannuli/minote-android
- 头歌：https://bdgit.educoder.net/pk8v7jyo9/minote-android-edu

## 已知事项

- `MainActivity.java` 及 `AndroidManifest.xml` 末尾的部分内容为
  Android Studio 模板残留，未生效，后续可清理。
- `httpcomponents-client-4.5.14-bin/` 中包含 `javadoc/` 文档，非运行必需，
  可后续精简。
- 构建时可能出现 `android.nonFinalResIds` 的 deprecation 警告，属正常现象，
  不影响构建与运行。

## 致谢

原始代码版权归小米及原项目作者所有。本项目仅用于学习、研究与个人维护。