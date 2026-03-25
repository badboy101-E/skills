# Skills

适用于 Codex 的自建 skills 仓库。

这里收录的 skills 以真实项目实践为基础，都是经过实际测试、能够跑通关键流程的生产级 skills。它们默认面向 Codex 使用，也可以按不同 agent 的 skill 机制做适配，迁移到任何支持 skills 的 agent 工作流中。

欢迎访问，也欢迎持续关注后续新增的 skills。

## Overview

- 面向 Codex 的可复用自建 skills
- 优先沉淀已经在真实业务中验证过的流程
- 关注生产可用性，而不只是概念性示例
- 尽量保持参数化设计，方便迁移到不同项目和不同 agent

## Why This Repo

这个仓库不是用来堆放概念性模板，而是用来沉淀已经在真实项目中跑通过、可以直接复用和继续演进的技能资产。

这里的每个 skill 都尽量满足这些目标：

- 有明确使用场景
- 有真实跑通过的流程基础
- 能在生产环境或接近生产环境的任务里复用
- 保持可迁移、可扩展、可维护

## Skill Catalog

| Skill | 类型 | 适用场景 | 核心能力 |
| --- | --- | --- | --- |
| [`volcengine-docker-cd`](./volcengine-docker-cd) | CD / Docker / Deploy | 将任意项目构建为 Docker 镜像并发布到火山引擎镜像仓库，再通过远端 `docker compose` 完成部署与回滚 | 多架构构建、镜像推送、版本 tag 管理、远端部署、回滚、常见问题排查 |

## Current Skill Notes

### `volcengine-docker-cd`

这是一个面向 Docker 持续交付场景的生产级 skill，适用于将任意项目构建为 Docker 镜像，并发布到火山引擎镜像仓库，再通过远端 `docker compose` 完成部署与回滚。

覆盖能力包括：

- Docker 镜像构建与发布
- 多架构镜像发布建议，适配 `linux/amd64` 与 `linux/arm64`
- Volcengine 镜像仓库登录、打 tag、推送
- 远端服务器 `docker compose` 部署
- 基于镜像 tag 的版本控制与快速回滚
- 常见问题排查，例如架构不匹配、仓库鉴权失败、Compose 误拉远端镜像等

适用场景包括：

- 将本地项目发布到火山云镜像仓库
- 为 Linux 服务器生成标准化 Docker CD 流程
- 设计可回滚的镜像版本发布策略
- 输出适合生产环境的 Compose 部署方式

## Roadmap

这个仓库后续会持续补充更多我自己创建并在实际流程中跑通过的 skills，逐步沉淀成一套可直接复用的个人工作流能力库。

后续新增的 skills 可能会覆盖：

- CI/CD 自动化
- 云端部署与运维
- 图像生成与多模态工作流
- API 中台与服务封装
- Agent 协作流程设计

## Usage

如果你使用的是 Codex，可以将对应 skill 放入本地 skills 目录后直接调用。

如果你使用的是其他支持 skills 的 agent，也可以参考这里的目录结构、`SKILL.md` 组织方式和引用文档设计，按各自 agent 的规范做适配。

## Contributing Direction

后续这个仓库会持续补充更多我自己创建的其他 skills。每个新 skill 会尽量保持：

- 有明确的问题域
- 有实际验证过的使用路径
- 有可以直接复用的 `SKILL.md` 和配套参考文档
- 有面向真实工作流的落地价值
