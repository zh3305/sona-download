# Sona 客户端下载

静态下载页：GitHub Pages 托管页面，GitHub Releases 托管安装包。

- 页面地址：https://zh3305.github.io/sona-download/
- 仓库 Releases：https://github.com/zh3305/sona-download/releases

## 发新版本

1. `gh release create vX.Y.Z --title "Sona vX.Y.Z" --notes "..." <安装包>`
2. 更新 `index.html` 里的版本号、体积与 SHA-256
3. 提交推送，Pages 自动更新

页面上的 Android 下载按钮用的是 `releases/latest/download/` 固定路径，只要上传的资产名保持 `app-release.apk`，新版本无需改页面。
