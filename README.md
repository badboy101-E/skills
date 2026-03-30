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
| [`github-skill-publish`](./github-skill-publish) | Git / GitHub / Skills | 将本地自建 skill 发布到 GitHub skills 仓库，并同步维护仓库 README 与索引 | 仓库检查、克隆、SSH 推送、README 更新、技能目录维护、鉴权排障 |
| [`codeup-project-ci-bootstrap`](./codeup-project-ci-bootstrap) | CI / Codeup / Bootstrap | 基于本地已创建项目目录，自动创建中心版 Codeup 远程仓库，初始化 Git，并生成最小 CI 起步文件 | Codeup 建仓、`.env` 读取、Git 初始化、SSH 远程绑定、初始提交与首推、CI 基础骨架生成 |

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

### `github-skill-publish`

这是一个面向 GitHub skills 仓库发布场景的生产级 skill，适用于把本地已经完成的 Codex skill 发布到 GitHub 仓库，并保持仓库级 README 与技能目录可持续维护。

覆盖能力包括：

- 检查目标 GitHub 仓库与默认分支
- 克隆 skills 仓库到本地工作区
- 将本地 skill 目录复制进目标仓库
- 切换 Git 远程到 SSH 并验证 `ssh -T git@github.com`
- 提交并推送新的 skill
- 更新仓库首页 README 与技能目录索引
- 排查 HTTPS/SSH 鉴权、远程地址与推送失败问题

适用场景包括：

- 将新创建的 skill 发布到 GitHub skills 仓库
- 维护一个持续增长的自建 skills 仓库
- 统一 skill 发布流程与仓库首页说明
- 基于 SSH 方式完成 GitHub 推送

### `codeup-project-ci-bootstrap`

这是一个面向中心版 Codeup 的生产级 CI 起步 skill，适用于在你已经手动创建好本地项目目录之后，自动完成远程私有仓库创建、本地 Git 初始化、最小 CI 基础文件生成，以及首次推送。

覆盖能力包括：

- 基于当前本地目录名推导并规范化远程仓库名
- 从项目根目录 `.env` 读取 `YUNXIAO_TOKEN`
- 调用中心版 Codeup OpenAPI 创建远程私有仓库
- 初始化本地 Git 仓库并设置 `main`
- 生成最小 CI 起步文件，例如 `README.md`、`.gitignore`、`.env.example`、`ci/README.md` 和基础脚本
- 配置 SSH 远程并完成首次提交与推送
- 排查 `.env` 缺失、`organization_id` 缺失、仓库重名、SSH 推送失败等问题

适用场景包括：

- 在 Codeup 中为新项目自动创建远程仓库
- 为新项目建立最小可用的 CI 起步结构
- 把“本地新项目目录”快速变成可进入 CI/CD 的仓库
- 为后续接入 Docker/CD 流程打基础

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
