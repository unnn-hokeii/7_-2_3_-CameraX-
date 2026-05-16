# Android 实验 2_3：构建 CameraX 应用
**实验完成时间**：2026年5月16日  
**实验者**：unnn-hokeii  
**GitHub 仓库地址**：https://github.com/unnn-hokeii/7_-2_3_-CameraX-

---

## 一、实验目的
1.  掌握 Android Jetpack CameraX 框架的核心概念与基本使用方法
2.  实现 CameraX 四大核心用例：预览(Preview)、拍照(ImageCapture)、录像(VideoCapture)、图像分析(ImageAnalysis)
3.  理解 CameraX 与 Activity 生命周期自动绑定的机制优势
4.  掌握 Android 应用权限申请与动态权限处理方法
5.  熟悉 Android Studio 完整开发流程：项目创建、依赖配置、代码编写、调试测试、版本控制
6.  学习使用 Git 进行代码管理并上传至 GitHub 仓库

---

## 二、实验环境
| 软件/硬件 | 版本/型号 |
|-----------|-----------|
| 操作系统 | macOS Sonoma (M2 芯片) |
| Android Studio | 2024.2.1 |
| Gradle | 8.9 |
| Android Gradle Plugin (AGP) | 8.7.0 |
| Kotlin | 1.9.24 |
| CameraX | 1.4.0 |
| 测试设备 | Pixel 6 模拟器 (Android 17 API 37) |
| 最低支持 API | 21 |

---

## 三、实验内容与步骤
### 3.1 项目创建与基础配置
1.  在 Android Studio 中创建 Empty Activity 项目，选择 Kotlin 语言
2.  配置 ViewBinding 功能，简化布局文件访问
3.  在 `libs.versions.toml` 中添加 CameraX 相关依赖
4.  配置 Java 8 编译选项，支持 Lambda 表达式等现代语法

### 3.2 权限配置
在 `AndroidManifest.xml` 中添加实验所需的全部权限：
- 相机硬件特性声明
- 相机权限
- 录音权限（用于录像）
- 存储权限（适配不同 Android 版本）

### 3.3 布局设计
编写 `activity_main.xml` 布局文件，包含：
- `PreviewView`：用于显示相机实时预览画面
- 两个功能按钮："TAKE PHOTO"（拍照）和 "START CAPTURE"（录像）

### 3.4 核心功能实现
1.  **权限动态申请**：在应用启动时检查并请求相机和录音权限
2.  **相机初始化**：获取 `ProcessCameraProvider` 实例，绑定生命周期
3.  **Preview 用例**：将相机预览画面显示到 `PreviewView` 上
4.  **ImageCapture 用例**：实现拍照功能，将照片保存到系统相册
5.  **VideoCapture 用例**：实现视频录制功能，支持开始/停止控制
6.  **ImageAnalysis 用例**：实现实时图像亮度分析，每秒输出亮度值到 Logcat

### 3.5 测试与调试
1.  运行应用到 Android 模拟器
2.  依次测试所有功能，记录运行效果
3.  截取所有关键界面截图
4.  解决实验过程中遇到的各种问题

### 3.6 代码提交与文档编写
1.  使用 Git 进行版本控制
2.  将完整代码上传至 GitHub 仓库
3.  编写详细的 README 文档
4.  上传所有实验截图到仓库

---

## 四、核心功能说明
### 4.1 实时预览 (Preview)
- 将摄像头采集的画面实时显示在界面上
- 自动适配屏幕方向和分辨率
- 与 Activity 生命周期绑定，自动管理相机的打开和关闭

### 4.2 拍照功能 (ImageCapture)
- 点击 "TAKE PHOTO" 按钮触发拍照
- 自动处理图像旋转和裁剪
- 将照片保存到系统相册的 `CameraX-Image` 文件夹
- 拍照成功后显示 Toast 提示

### 4.3 录像功能 (VideoCapture)
- 点击 "START CAPTURE" 开始录像，按钮文字变为 "STOP CAPTURE"
- 点击 "STOP CAPTURE" 停止录像
- 将视频保存到系统相册的 `CameraX-Video` 文件夹
- 录像成功后显示 Toast 提示

### 4.4 图像分析 (ImageAnalysis)
- 后台实时处理相机每一帧画面
- 计算并输出图像的平均亮度值
- 每秒输出一次结果到 Logcat
- 不影响预览和拍照功能的正常运行

---

## 五、运行效果与截图
所有实验截图已保存在仓库的 `screenshots/` 文件夹中：

| 截图文件名 | 内容说明 |
|------------|----------|
| 01_permission_request.png | Android Studio 请求麦克风权限界面 |
| 02_camera_preview.png | 相机实时预览界面 |
| 03_photo_captured.png | 拍照成功并查看照片界面 |
| 04_photo_share.png | 照片保存界面 |
| 05_video_recording.png | 录像中界面（按钮显示 STOP CAPTURE） |
| 06_logcat_luminosity.png | Logcat 实时亮度分析日志 |
| 07_build_success.png | 项目编译成功界面 |
| 08_github_repository.png | GitHub 仓库主页 |

✅ **所有功能均正常运行**：
- 应用启动无崩溃
- 权限请求正常
- 相机预览流畅
- 拍照保存成功
- 录像保存成功
- 图像分析正常输出

---

## 六、项目结构
CameraXDemo/
├── app/
│   ├── src/main/
│   │   ├── java/com/example/cameraxdemo/
│   │   │   └── MainActivity.kt          # 主Activity，所有功能实现
│   │   ├── res/
│   │   │   ├── layout/
│   │   │   │   └── activity_main.xml    # 主布局文件
│   │   │   ├── values/
│   │   │   │   ├── colors.xml           # 颜色配置
│   │   │   │   ├── strings.xml          # 字符串资源
│   │   │   │   └── themes.xml           # 应用主题
│   │   │   └── mipmap-*/                # 应用图标
│   │   └── AndroidManifest.xml          # 应用清单文件
│   └── build.gradle.kts                 # 模块级构建配置
├── gradle/
│   └── libs.versions.toml               # 依赖版本管理
├── screenshots/                          # 实验截图文件夹
│   ├── 01_permission_request.png
│   ├── 02_camera_preview.png
│   ├── 03_photo_captured.png
│   ├── 04_photo_share.png
│   ├── 05_video_recording.png
│   ├── 06_logcat_luminosity.png
│   ├── 07_build_success.png
│   └── 08_github_repository.png
├── build.gradle.kts                      # 项目级构建配置
├── gradle.properties                     # Gradle 属性配置
├── settings.gradle.kts                   # 项目设置
└── README.md                             # 本说明文档

---

## 七、实验中遇到的问题与解决方法
1.  **应用启动崩溃：主题不匹配**
    - 错误信息：`You need to use a Theme.AppCompat theme (or descendant) with this activity`
    - 解决方法：修改 `AndroidManifest.xml` 中的 `android:theme` 属性，使用正确的 AppCompat 主题

2.  **编译失败：Manifest 语法错误**
    - 错误信息：`Error parsing AndroidManifest.xml`
    - 解决方法：检查并修复 XML 标签语法错误，确保所有标签正确闭合

3.  **GitHub 推送失败：认证错误**
    - 错误信息：`Password authentication is not supported for Git operations`
    - 解决方法：切换为 SSH 协议，生成并添加 SSH 密钥到 GitHub 账户

4.  **Google 相册无法打开**
    - 问题：虚拟机无法连接 Google 服务器，导致 Google 相册无法使用
    - 解决方法：使用系统自带的文件应用查看保存的照片和视频，不影响实验结果

---

## 八、实验总结
本次实验成功基于 Android Jetpack CameraX 框架实现了一个完整的相机应用，包含实时预览、拍照、录像和图像分析四大核心功能。通过本次实验，我深入理解了 CameraX 框架的设计思想和优势，掌握了 Android 相机开发的基本流程和最佳实践。

在实验过程中，我遇到了多个常见的 Android 开发问题，通过查阅文档和调试代码，逐一解决了这些问题，提升了自己的问题解决能力。

CameraX 作为 Google 官方推荐的相机开发框架，大大简化了 Android 相机开发的难度，提供了良好的设备兼容性和一致的 API 接口，是未来 Android 相机应用开发的首选方案。

---

## 九、提交说明
- ✅ 完整项目代码已上传至 GitHub 仓库
- ✅ 所有实验截图已上传至仓库 `screenshots/` 文件夹
- ✅ 详细的 README 文档已编写完成
- ✅ 所有实验要求的功能均已实现并测试通过
