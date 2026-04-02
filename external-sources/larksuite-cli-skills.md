# LarkSuite CLI Skills Source Note

这份说明只记录飞书官方 CLI skills 的源码来源与用途简介，不包含 `lark-*` skills 本体源码。

## Source Repository

- GitHub: [larksuite/cli](https://github.com/larksuite/cli)
- Clone URL: `https://github.com/larksuite/cli.git`

## What It Is

`larksuite/cli` 是飞书 / Lark 官方维护的 CLI 仓库。除了命令行工具本身，它还提供一组面向 AI agent 的配套 skills。

通过下面的安装命令：

```bash
npx skills add larksuite/cli -g -y
```

会安装一批围绕飞书各业务域的 skills，例如：

- `lark-im`
- `lark-doc`
- `lark-contact`
- `lark-calendar`
- `lark-drive`
- `lark-sheets`
- `lark-task`
- `lark-shared`

## Why This Note Exists

这里保留的是“上游源码地址 + 简单说明”，方便后续追溯来源、查看官方实现和更新安装方式。

本仓库当前**不镜像**这些飞书官方 skills，也**不复制**其源码目录，只保留来源说明。
