# LarkSuite CLI Skills Overview

这份说明基于飞书官方 `larksuite/cli` 项目的 README 整理，只保留上游仓库地址和一份简短概述，不包含 `lark-*` skills 本体源码。

## Source Repository

- GitHub: [larksuite/cli](https://github.com/larksuite/cli)
- Clone URL: `https://github.com/larksuite/cli.git`
- README: [README.zh.md](https://github.com/larksuite/cli/blob/main/README.zh.md)

## Overview

`larksuite/cli` 是飞书 / Lark 官方维护的命令行工具项目，用于通过统一的 CLI 方式操作飞书开放平台能力。除了命令行工具本身，它还提供一组面向 AI agent 的配套 skills，帮助 agent 在飞书场景下完成配置、认证、文档、消息、日历、云盘、表格等常见任务。

从官方 README 的定位来看，这套 skills 更适合以下场景：

- 让 AI agent 通过标准命令调用飞书能力
- 在交互式授权完成后访问用户侧资源
- 将飞书开放平台的常见操作拆分成可复用的 skill
- 在不同业务域之间复用统一的认证、权限和安全规则

## Main Skill Areas

官方 README 中给出的 skills 主要覆盖这些方向：

- `lark-shared`
- `lark-calendar`
- `lark-im`
- `lark-doc`
- `lark-drive`
- `lark-sheets`
- `lark-base`
- `lark-task`
- `lark-mail`
- `lark-contact`
- `lark-wiki`
- `lark-event`

其中：

- `lark-shared` 负责应用配置、认证登录、身份切换、权限管理和安全规则，是其他 skills 的共享基础。
- `lark-im` 负责消息发送、回复、群聊管理和聊天相关操作。
- `lark-doc`、`lark-drive`、`lark-sheets` 负责云文档、云盘和电子表格相关能力。
- `lark-calendar`、`lark-task`、`lark-mail` 分别覆盖日历、任务和邮箱场景。
- `lark-contact`、`lark-wiki`、`lark-event` 则补足通讯录、知识空间和事件订阅场景。

## Agent Usage Note

官方 README 里把 AI Agent 的使用流程拆成四步：

1. 安装 CLI
2. 安装 `larksuite/cli` skills
3. 配置应用凭证
4. 完成用户授权并验证登录状态

也就是说，这套 skills 不是单独存在的文档集合，而是和 `lark-cli` 本体、飞书应用配置、用户授权流程一起组成完整工作链路。

## Repository Note

本仓库当前只保留这份“上游源码地址 + README 概述”说明，用于追溯来源和快速理解能力边界。

本仓库当前**不镜像**这些飞书官方 skills，也**不复制**其源码目录。
