# RCC 发行下载

此仓库用于发布 RCC 安装脚本、二进制安装包、校验文件、使用说明和必要许可证。开发源码在独立私有仓库维护。

RCC 在服务器运行 Claude Code；用户电脑保存项目文件并执行项目工具。每位用户使用自己的服务器账号，电脑分别登记为独立设备。

## Linux 安装

首个正式版本：[rcc-v0.1.0](https://github.com/jayus71/rcc-releases/releases/tag/rcc-v0.1.0)。支持 **Linux amd64，Debian 12 / Ubuntu 24.04，glibc ≥ 2.36**。

在本人普通用户终端执行，无需 GitHub 登录：

```sh
(f=$(mktemp) && trap 'rm -f "$f"' EXIT && curl -fsSL --proto '=https' --proto-redir '=https' --max-redirs 10 https://github.com/jayus71/rcc-releases/releases/download/rcc-v0.1.0/install.sh -o "$f" && sh "$f")
```

安装前需要：

- Python 3、OpenSSH client、bash、util-linux、curl，以及可用的 user-systemd；安装器会提示缺少的依赖。
- 维护者提供的 HTTPS 服务地址及本人长期 **RCC 登录密钥**，运行端已开通本人账号并完成官方 Claude 授权。
- 配套运行端。此版本源码为 `9028140aa20c4ebf76a0ddb625f160ef5d72f793`；维护者应核对运行端产品兼容性。

按提示输入服务地址和个人密钥；密钥无回显，不要拼入命令行或公开发送。安装完成后重新打开终端，进入具体项目目录运行：

```sh
cd /path/to/your/project
rcc
```

项目文件、Bash、Git和计算在工作节点执行；官方Claude及其凭据保存在运行端。请在具体项目目录启动，不使用HOME根目录作为执行项目。换电脑时运行相同安装入口，再用本人RCC密钥接入；每台电脑保存独立设备身份。

## 升级与记忆

升级可重新运行相同入口，默认保留设备身份、节点配置和项目，安装器在原登记路径更新其管理的helper。使用过自定义 `--prefix` / `--bin-dir` 的用户，升级时须继续传入相同参数。

本版包含默认项目原生记忆保存和重开加载，以及运行端本人skills资料的只读访问。记忆按项目隔离，不自动跨项目同步。个人skills内容由用户或维护者在运行端安装，**不包含在公开下载包内**；skills脚本仍按工作节点Bash路由执行。

## Windows / WSL2 状态

提供 `install.ps1` 作为Windows x64到WSL2 Linux的入口，但**真实Windows/WSL2完整用户流程尚未验收**，当前正式验收范围为上述Linux平台。WSL需先准备Linux发行版、普通用户及user-systemd，安装完成后在Linux文件系统的项目目录使用。原生Windows/macOS及 `/mnt/c` 项目不在当前支持范围；详见包内 `WINDOWS-WSL2.md`。

## 下载与校验

[发行页面](https://github.com/jayus71/rcc-releases/releases/tag/rcc-v0.1.0)提供七项资产：Linux包、Shell/PowerShell入口、安装器元数据、发行元数据、SHA256SUMS及发行说明。入口固定本版包URL、source及SHA256，不会在安装中途切换版本。

`rcc-v0.1.0-linux-amd64.tar.gz` 的SHA256：

```text
342b734843466dd8bf1b3228cb324745b94f40c9fbd204594d5d5b7e87026dd9
```

正式版本通过 GitHub Releases 提供，附固定版本及 SHA256 校验信息。此仓库不存放开发历史、内部测试证据、用户配置、登录密钥或 Claude 凭据。

RCC 基于 MIT 许可的 AgentReach。发行包保留原版权声明及所用依赖的必要许可证，见 LICENSE 及各版本随附许可文件。
