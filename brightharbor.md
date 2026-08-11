# AquaLink 技术导航聚合

AquaLink 是一个面向开发人员与技术研究者的外链资源聚合系统，专注于对互联网中高价值技术社区、开源镜像站、学术论文库及代码托管平台进行结构化整理与可检索化呈现。项目定位为“技术入口的入口”，通过人工筛选与自动化可用性检测相结合的方式，为技术团队、独立开发者及科研人员提供稳定、可验证的外部资源跳转服务。项目本身不存储任何第三方内容，仅提供元数据索引与链接健康度监控，解决技术调研过程中资源分散、链接失效、检索成本高等实际问题。

## 功能概览

- **多级分类索引**：按地域、语言、技术栈、内容形态对收录资源进行标签化分类，支持快速过滤。

- **链接存活检测**：后台定时任务对已收录 URL 进行 HTTP 状态码检查，自动标记异常链接并生成报告。

- **用户自定义收藏夹**：登录用户可将外部链接归入个人收藏夹，支持备注标签与访问时间戳。

- **全文检索与模糊匹配**：基于链接标题、描述、分类标签及域名关键词进行轻量级全文搜索。

- **访问统计与热度排序**：记录各链接被点击的次数与最后访问时间，支持按热度、更新时间、新增时间排序。

- **批量导入与导出**：支持通过 CSV 或 JSON 格式批量导入外部链接列表，同时支持导出为 Markdown 或 HTML 书签格式。

- **链接变更追踪**：对已收录链接的页面标题、描述等元信息进行周期性比对，发现变更时生成通知。

- **只读 API 接口**：提供 RESTful 风格的公开 API，供第三方工具查询链接分类与状态信息。

## 应用场景

- **技术团队内部知识库构建**：团队负责人可通过 AquaLink 整理团队常用开发文档、镜像站、依赖仓库地址，统一入口并减少重复查找时间。

- **开源项目 README 外链维护**：开源项目维护者可使用 AquaLink 托管项目相关的外部参考链接，避免在 README 中维护大量冗长 URL，同时利用存活检测功能主动发现失效引用。

- **技术调研与竞品分析**：研究人员在调研特定领域（如国产操作系统、海外学术资源）时，可借助分类索引快速定位相关站点，并通过访问热度判断资源活跃程度。

- **个人开发环境初始化辅助**：开发者在新环境配置时，可通过 AquaLink 导出的书签列表一键获取常用工具下载页、配置文档及社区论坛地址。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境，请确保已安装 Git 与 Node.js 18.x 及以上版本。

```bash
# 克隆项目仓库
git clone https://git.aqualink.dev/community/aqualink-core.git
cd aqualink-core

# 安装项目依赖
npm install

# 复制环境变量模板并修改数据库连接
cp .env.example .env
# 编辑 .env 文件，设置 DATABASE_URL 与 PORT

# 执行数据库迁移与初始数据填充
npx prisma migrate deploy
npm run seed

# 以开发模式启动服务
npm run dev
```

服务默认监听 3000 端口，访问 http://localhost:3000 即可进入链接管理面板。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用官方预编译二进制 |
| PostgreSQL | 14.x 或 15.x | 主数据库，用于存储链接元数据与用户信息 |
| Redis | 7.x | 缓存层，用于链接状态检测结果与访问计数 |
| Git | 2.30 以上 | 版本控制，用于克隆与提交更新 |
| PM2 | 5.x | 生产环境进程守护（可选，开发环境可跳过） |
| Nginx | 1.20 以上 | 反向代理与静态资源服务（生产环境推荐） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | /docs/user/getting-started.md | 如何注册、登录、添加第一个链接并创建分类 |
| 管理员指南 | /docs/admin/link-health.md | 如何配置链接存活检测策略、查看异常报告 |
| 开发指南 | /docs/dev/api-reference.md | API 端点列表、请求格式、鉴权方式 |
| 部署运维 | /docs/ops/deployment-checklist.md | 生产环境变量配置、SSL 证书、备份策略 |
| 数据模型 | /docs/dev/data-schema.md | 数据库表结构、字段含义与关联关系 |
| 贡献规范 | /docs/community/coding-standards.md | 代码风格、提交信息格式、PR 流程 |

## 资源列表

### 综合类资源

<code>guochanyoudayouhuang.org.cn</code>

<code>wuyerenqi.org.cn</code>

<code>yazhouchengrenyiquerqu.org.cn</code>

<code>oumeizhongchu.org.cn</code>

### 专题类资源

<code>tiantianyue.org.cn</code>

<code>yirenjiujiu.org.cn</code>

<code>sihujingpin.org.cn</code>

<code>guochanrihanoumei.org.cn</code>

### 专项类资源

<code>rihanmadou.org.cn</code>

<code>oumeihouru.org.cn</code>

## 项目结构

```
aqualink-core/
├── config/                         # 运行时配置文件
│   ├── default.json                # 默认端口、日志级别、超时阈值
│   └── production.json             # 生产环境覆盖配置
├── src/
│   ├── api/                        # HTTP 路由层
│   │   ├── v1/                     # 当前稳定版 API
│   │   │   ├── links/              # 链接增删改查与状态查询
│   │   │   ├── categories/         # 分类树管理
│   │   │   └── auth/               # 登录注册与令牌刷新
│   │   └── v2/                     # 实验性 API（开发中）
│   ├── core/                       # 核心业务逻辑
│   │   ├── link-health/            # 链接存活检测引擎（定时任务）
│   │   ├── search/                 # 全文索引与查询解析
│   │   └── stats/                  # 点击统计与热度计算
│   ├── db/                         # 数据库相关
│   │   ├── migrations/             # Prisma 迁移脚本
│   │   ├── seed/                   # 初始分类与示例数据
│   │   └── repositories/           # 数据访问层封装
│   ├── middleware/                 # 请求拦截器
│   │   ├── auth.ts                 # JWT 验证
│   │   ├── logger.ts               # 访问日志
│   │   └── rate-limit.ts           # 接口限流
│   ├── models/                     # TypeScript 类型定义与验证器
│   └── utils/                      # 工具函数
│       ├── url-normalizer.ts       # URL 规范化与去重
│       └── html-parser.ts          # 页面标题与描述提取
├── tests/                          # 单元测试与集成测试
│   ├── unit/
│   └── integration/
├── scripts/                        # 运维辅助脚本
│   ├── health-check.sh             # 手动触发链接检测
│   └── backup-db.sh                # 数据库备份脚本
├── public/                         # 静态资源（仅限 favicon 与 robots.txt）
├── docs/                           # 文档源文件（参见文档导航）
├── .env.example                    # 环境变量模板
├── docker-compose.yml              # 本地开发环境容器编排
├── Dockerfile                      # 生产镜像构建文件
├── package.json                    # npm 依赖与脚本定义
└── README.md                       # 本文件
```

## 贡献指南

1. 查阅问题列表与项目看板，选取标记为 `good-first-issue` 或 `help-wanted` 的任务，在任务下留言说明认领意向，等待维护者确认。

2. 复刻主仓库至个人账号，将复刻后的仓库克隆到本地，并参照安装要求搭建开发环境。建议使用 `docker-compose up -d` 启动 PostgreSQL 与 Redis 容器以统一环境。

3. 新建功能分支，分支名称遵循 `feature/功能简述` 或 `fix/问题简述` 格式。提交代码前运行 `npm run lint` 与 `npm run test` 确保代码风格与测试用例通过。

4. 提交 Pull Request 至主仓库的 `develop` 分支，PR 描述中需关联对应任务编号，并说明变更范围与测试方式。PR 至少需要一位维护者审核，若 CI 流水线失败需及时修复。

5. 文档类变更（包括修正 README 中的链接或示例）同样欢迎提交 PR，但需确保文档中的外部 URL 均为可访问状态。

## 常见问题

**Q: 链接存活检测是否会频繁访问目标站点，导致被目标服务器封禁？**

A: 检测引擎默认采用间隔 24 小时的全量扫描策略，且单次请求超时设为 10 秒。对同一域名的并发请求数限制为 2 个，同时 User-Agent 设置为项目标识符并带有联系方式信息。若目标站点声明了 robots.txt 中的 Crawl-delay 指令，引擎将自动适配延迟间隔。检测结果仅用于内部标记，不会对外公开显示具体状态码细节，仅展示“可访问”或“异常”两种状态。

**Q: 如何迁移已收藏的链接数据至另一台服务器？**

A: 可使用内置的导入导出功能。在管理面板的“设置 - 数据管理”中点击“导出所有链接”会生成包含完整元数据的 JSON 文件。在新服务器部署完成后，通过“导入”功能上传该文件并选择“覆盖”或“合并”模式。若需迁移数据库完整内容，建议直接使用 PostgreSQL 的 pg_dump 和 pg_restore 工具，迁移前需确保两端的 Prisma 迁移版本一致。

**Q: 项目是否支持添加需要登录或带有动态参数的链接？**

A: 支持。添加链接时可在“备注”字段中说明登录方式或参数示例。但链接存活检测仅针对静态 URL 的响应状态码进行判定，无法执行 JavaScript 或提交表单。对于需要会话鉴权的链接，系统会记录为“需人工验证”状态，并降低自动检测频率。用户可在收藏夹中为这类链接单独设置“跳过自动检测”标记。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:36
