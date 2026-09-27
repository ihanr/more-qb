# more-qb

针对 `qbittorrent-nox@shoo.service` 的多实例脚本适配版。

来源：[RinehartZ/seedbox-tools](https://github.com/RinehartZ/seedbox-tools/blob/main/Tools/more_qb.sh)。保留上游主体逻辑，只修改原服务文件路径、服务名称及相关提示。

## 适用环境

- `/etc/systemd/system/qbittorrent-nox@.service` 存在。
- 模板中明确设置 `User=shoo`，原实例为 `qbittorrent-nox@shoo.service`。
- 原配置为 `/home/shoo/.config/qBittorrent/qBittorrent.conf`。

## 使用

在目标 Linux 服务器上以 root 执行以下一键下载安装命令，无需 GitHub 登录：

```bash
wget -O more_qb.sh https://raw.githubusercontent.com/ihanr/more-qb/main/more_qb.sh && bash more_qb.sh -n 2 -w 9091 -b 23334
```

脚本会下载到当前目录的 `more_qb.sh`（同名文件会被覆盖），只有下载成功才会执行。

这会新增 qb2、qb3，WebUI 端口为 9091、9092，BT 端口为 23334、23335。

**不要对已有 qb2、qb3 的服务器重复运行。** 上游逻辑会覆盖同名服务及实例配置，并在执行期间停止原服务。请确认端口未占用并先备份配置。

该版本不是通用服务自动识别器。未改动上游的配置复制、权限、错误处理和启动流程；语法检查不等于真实 systemd/qB 运行验证。
