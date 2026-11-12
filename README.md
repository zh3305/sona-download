# Sona 客户端下载

GitHub Pages 托管静态下载页，GitHub Releases 托管安装包，零服务器成本。

| 用途 | 地址 |
| :-- | :-- |
| 下载页 | https://zh3305.github.io/sona-download/ |
| Release 列表 | https://github.com/zh3305/sona-download/releases |
| APK 永久直链 | `https://github.com/zh3305/sona-download/releases/latest/download/app-release.apk` |

## 发布新版本

### 1. 构建

```bash
cd H:\Code_Poject\HYIM\mobile
flutter build apk --release
sha256sum build/app/outputs/flutter-apk/app-release.apk
```

### 2. 发 Release

```bash
export MSYS_NO_PATHCONV=1
export HTTP_PROXY=http://127.0.0.1:11991 HTTPS_PROXY=http://127.0.0.1:11991

gh release create v<版本> "H:/Code_Poject/HYIM/mobile/build/app/outputs/flutter-apk/app-release.apk" \
  --title "Sona v<版本>" --notes "<更新说明>"
```

### 3. 更新页面（仅版本信息变化时需要）

下载链接用的是 `releases/latest/download/` 固定路径，**发新版不用改**。
只有版本号、体积、SHA-256 变了才需要改 `index.html`，然后提交推送，Pages 自动重建。

## 约定

- **资产名必须保持 `app-release.apk`**，否则页面上的 latest 直链会 404
- 图标用**内联 SVG**，不用 emoji（emoji 跨系统渲染不一致）
- 未发布的端（Windows / iOS）用 `aria-disabled="true"` 置灰，不做假链接

## 坑

- **`gh api /repos/...` 在 Git Bash 下会被路径改写** → 必须先 `export MSYS_NO_PATHCONV=1`
- **必须走代理访问 GitHub** → 否则报 `SSL_ERROR_SYSCALL`（代理 `http://127.0.0.1:11991`）
- **216MB 上传约 8~10 分钟**，期间无任何输出属正常，别当卡死

## 拆分包（未启用）

`flutter build apk --split-per-abi` 会与 `mobile/android/app/build.gradle` 里的
`ndk { abiFilters "arm64-v8a", "x86_64" }` 冲突，需先调整该配置。
当前发布通用包（216MB，双架构）。

> 完整流程与排错记录见主仓库 `.agentdocs/devops/client-distribution.md`
