# Homarr for LazyCat

A modern and easy to use dashboard. 40+ integrations. 20K+ icons built in. Authentication out of the box. No YAML, drag and drop configuration.

上游：https://github.com/homarr-labs/homarr

## 使用

要求懒猫微服 1.5.0 或更新版本，目标架构 amd64。首次访问按上游向导创建管理员和仪表盘。保留手动登录，不注入文件选择器。

原 Compose 的 Docker socket 通过构建配置的 Compose 扩展挂载，数据持久化到 `/lzcapp/var/appdata`（容器 `/appdata`）。Socket 提供宿主 Docker 管理能力，请仅授权可信用户。目标微服需存在 `/var/run/docker.sock`，实际 socket 权限和管理操作需安装后确认。不要通过此工具随意改动微服管理的系统容器。

加密密钥由懒猫 `stable_secret` 生成后计算 SHA256，得到 64 位十六进制密钥，不在仓库中保存明文密钥，同一微服上的同一应用重启和升级后保持稳定。迁移到其他微服时必须同时迁移原密钥与数据。

## 构建与发布

```sh
mkdir -p dist
lzc-cli project release -o dist/application.lpk
lzc-cli lpk info dist/application.lpk
```

只发布喵喵商店，不发布官方商店。使用 `ghcr.1ms.run` 镜像，并在自动更新时验证目标架构摘要与 GHCR 一致。初始版本为 `1.77.0`，每天跟踪三段式稳定版本。

工作流引用组织级 `APPSTORE_URL`、`APPSTORE_TOKEN` 与可选的 `PRIVATE_STORE_GROUP_CODES`。发布文件为 `community.lazycat.app.homarr-v<version>.lpk`，喵喵商店引用 GitHub Release 下载地址和 SHA256。

本地打包和工作流校验不能替代微服实机验证。图标取自上游 v1.77.0，应用代码及许可证见上游仓库。
