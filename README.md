# Skills

适用于 Codex 的自建 skills 仓库。

这里收录的 skills 以真实项目实践为基础，都是经过实际测试、能够跑通关键流程的生产级 skills。它们默认面向 Codex 使用，但也可以根据不同 agent 的 skill 机制做适配，迁移到任何支持 skills 的 agent 工作流中。

欢迎访问，也欢迎持续关注后续新增的 skills。

## 仓库定位

- 面向 Codex 的可复用自建 skills
- 优先沉淀已经在真实业务中验证过的流程
- 关注生产可用性，而不只是概念性示例
- 尽量保持参数化设计，方便迁移到不同项目和不同 agent

## 当前已有 Skills

### `volcengine-docker-cd`

面向 Docker 持续交付场景的生产级 skill，适用于将任意项目构建为 Docker 镜像，并发布到火山引擎镜像仓库，再通过远端 `docker compose` 完成部署与回滚。

当前覆盖能力包括：

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

## 后续规划

这个仓库后续会持续补充更多我自己创建并在实际流程中跑通过的 skills，逐步沉淀成一套可直接复用的个人工作流能力库。

后续新增的 skills 可能会覆盖：

- CI/CD 自动化
- 云端部署与运维
- 图像生成与多模态工作流
- API 中台与服务封装
- Agent 协作流程设计

## 使用方式

如果你使用的是 Codex，可以将对应 skill 放入本地 skills 目录后直接调用。

如果你使用的是其他支持 skills 的 agent，也可以参考这里的目录结构、`SKILL.md` 组织方式和引用文档设计，按各自 agent 的规范做适配。
