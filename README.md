# 易控(Easycontrol)

## 修改版本说明

本仓库是 [mingzhixian/Easycontrol](https://github.com/mingzhixian/Easycontrol) 的修改版本，修改者 guchang233，日期 2026-11-15。授权协议仍是 **GPL-3.0**，许可证全文见 [LICENSE](LICENSE)，未作修改。

相对上游源码的改动：

- 上游公开仓库不含官方安装包里的激活模块（`:cloud`、`ActiveHelper`），README 要求自行注释相关代码。本修改版本已经去掉这些缺失引用，并关闭激活校验，安装后可以直接使用。
- `versionName` 为 `1.5.7-free`，用来标明这不是官方需要激活的安装包。

This is a modified version of mingzhixian/Easycontrol, changed by guchang233 on 2026-11-15. It remains licensed under GPL-3.0 (see LICENSE, unchanged). The activation gate is removed so a build from this tree runs without an activation key, and `versionName` is `1.5.7-free`.

## 注意
 Gitee和GitHub代码将保持同步，请自行选择。
- [Gitee地址](https://gitee.com/mingzhixianweb/easycontrol)
- [Github地址](https://github.com/mingzhixian/Easycontrol)

## 简介
本软件基于开源项目Scrcpy，对其进行了大量魔改，实现了其安卓客户端，并添加了一些功能，实现了安卓端控制安卓端。

## 功能特色
- 使用简单
- 支持音频传输
- 多设备连接
- 支持有线连接
- 多设备剪切板同步
- 多设备共享主控端物理键盘(需配合微信输入法或QQ输入法等输入中文)
- 启动迅速
- 低延迟
- 支持分辨率自适应
- 良好的旋转支持
- 支持小窗显示与全屏显示

## 使用说明
- [点击此处查看](https://gitee.com/mingzhixianweb/easycontrol/blob/master/HOW_TO_USE.md)

## 软件下载
- [点击此处查看](https://gitee.com/mingzhixianweb/easycontrol/releases)

## 激活
上游官方打包的安装包需要激活后才能使用，步骤见[此页面](https://gitee.com/mingzhixianweb/easycontrol/blob/master/DONATE.md)。本修改版本已关闭该校验，不需要激活。

## 截图
<center class="half">
 <img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/screenshot/1.jpg" width="150"/><img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/screenshot/2.jpg" width="150"/><img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/screenshot/3.jpg" width="150"/>
 <img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/screenshot/4.jpg" width="150"/><img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/screenshot/5.jpg" width="150"/><img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/screenshot/6.jpg" width="150"/>
 <img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/screenshot/7.jpg" width="150"/><img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/screenshot/8.jpg" width="150"/>
</center>

## 构建
请遵循 GPL-3.0。工程在 `easycontrol/`，使用 JDK 17 与 Android SDK 34。`local.properties` 不再入库，Gradle 使用环境变量 `ANDROID_HOME`。

上游去掉了官方打包加入的激活模块，所以原仓库直接编译会报错。本修改版本已经处理这些报错。

```bash
cd easycontrol
./gradlew :server:copyRelease
./gradlew :app:assembleRelease
```

第一条命令会把 server 的 release 包复制为 `app/src/main/res/raw/easycontrol_server.jar`（该文件不入库）。第二条命令生成已签名的 `app/build/outputs/apk/release/app-release.apk`。

签名：Actions 无法写入仓库 Secrets（接口返回 403），所以发布密钥放在 `easycontrol/keystore/easycontrol-release.jks`，密码在 `easycontrol/keystore.properties`。每次 CI 都用这一把密钥，签名保持不变，后续安装可以覆盖升级。

代价：私钥在公开仓库里，任何人都能打出相同签名的包。这个签名只保证升级连续性，不能证明安装包来自维护者。不要把这把密钥用到别的应用上。如果以后配置了四个 Secrets（`ANDROID_KEYSTORE_BASE64`、`ANDROID_KEYSTORE_PASSWORD`、`ANDROID_KEY_ALIAS`、`ANDROID_KEY_PASSWORD`），工作流会改用 Secrets，签名也会换成另一把，已安装的包将不能直接覆盖。

推送 `v*` tag，或手动运行 Actions 工作流 `Build release APK`，会把 `Easycontrol-1.5.7-free.apk` 传到 GitHub Release。推送到 `master` 只构建、不发布。

## 反馈
请在Github或Gitee提出Issue，或进入易控反馈群反馈BUG或建议。

<img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/other/qq_issue.webp" width="200px">
<img src="https://gitee.com/mingzhixianweb/easycontrol/raw/master/pic/other/wechat_issue.png" width="200px">

## 附加
- ADB协议说明(官方的文档写的真烂，感谢cstyan大佬) [点击前往](https://github.com/cstyan/adbDocumentation)
- Scrcpy官方地址 [点击前往](https://github.com/Genymobile/scrcpy)
- 易控车机版(第三方用户专为车机进行了调整优化) [点击前往](https://github.com/eiyooooo/Easycontrol_For_Car)
