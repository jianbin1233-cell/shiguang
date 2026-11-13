# 拾光 · Notes（Android 项目）

这是第一版拾光便签/日记应用的 Android 打包工程。网页应用已放在 `www/`，使用 Capacitor 7 生成 Android 原生 WebView 容器。

## 当前已包含
- 便签/日记新增、编辑、删除
- 置顶、收藏、分类、心情
- 标题/正文搜索
- 浅色、深色、自动跟随系统
- 当前设备本地存储
- JSON 导出与导入
- Capacitor Android 工程配置
- GitHub Actions 自动构建 APK 工作流

## 重要：APK 状态
此压缩包是**可构建的 Android 项目源码**，不是已经编译、签名并验证的 APK。当前交付环境没有 Android SDK/Gradle，因此没有在本机生成 APK。项目上传到 GitHub 后，工作流会在云端安装 Android 构建工具并生成 Debug APK。

## 最简单的 APK 构建方式（推荐）
1. 解压本项目 ZIP。
2. 登录 GitHub，创建一个新的空仓库，例如 `shiguang-notes`。
3. 在仓库页面选择 **Add file → Upload files**，上传解压后文件夹里的全部文件和文件夹（包括 `.github` 隐藏目录）。
   - 如果手机端看不到 `.github`，建议先在电脑上上传，或用 Git 客户端上传整个项目。
4. 提交到 `main` 分支。
5. 打开仓库的 **Actions** 页面，选择 **Build Android APK**。
6. 等待任务显示绿色成功（约数分钟，视 GitHub 构建队列而定）。
7. 打开该次运行页面，在 **Artifacts** 下载 `shiguang-android-debug-apk`，解压后得到 `app-debug.apk`。
8. 将 APK 传到 Android 手机并安装。首次安装时，按系统提示允许该来源安装应用。

## 本地构建（电脑已安装 Android Studio 时）
需要 Node.js 20+、JDK 21、Android SDK：
```bash
npm install
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug
```
APK 输出位置：
`android/app/build/outputs/apk/debug/app-debug.apk`

## 数据说明
记录保存在应用本地 WebView 存储空间。卸载应用或清除应用数据可能导致记录丢失；请定期在“我的 → 导出 JSON”中备份。导出的 JSON 可通过“从备份恢复”导入。

## 后续发布
Debug APK 适合个人测试。若要公开发布或长期分发，需要进一步配置正式签名密钥、版本号、隐私政策和发布版构建（Release/AAB）。
