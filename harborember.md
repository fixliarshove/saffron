# LinkPilot 技术资源导航站

LinkPilot 是一个面向开发者与技术研究人员的轻量级外链资源聚合与导航系统。该项目定位于解决技术信息分散、优质外部资源难以统一管理与快速检索的问题，特别适用于需要持续跟踪特定领域数据源、比分直播、实时统计接口或运维监控面板的技术团队。LinkPilot 不生产数据，而是提供一套结构清晰、可私有化部署的资源索引框架，帮助用户将分散的第三方链接按业务场景分类、打标、健康检查与快速跳转，从而提升信息获取效率与团队协作透明度。

## 功能概览

- **多维度资源分类**：支持按地域、联赛、数据类型（如比分、赛程、射手榜、前瞻）自定义分类层级，便于构建符合业务视图的资源树。

- **链接健康度探测**：内置周期性 HTTP 状态检查与响应时间监控，自动标记异常链接，减少人工巡检成本。

- **快速检索与过滤**：提供基于关键词、标签、状态码、更新时间的多条件组合检索，支持毫秒级响应。

- **外链访问统计**：记录每个资源的点击次数、最后访问时间、来源 IP 归属地（聚合级别），辅助分析资源热度。

- **导入导出标准格式**：支持 JSON / YAML / CSV 格式的批量导入导出，便于与其他监控系统或数据中台对接。

- **权限分级管理**：内置管理员、编辑者、访客三级角色，控制资源增删改查与分类编辑权限。

- **自定义元数据扩展**：允许为每个链接附加自定义键值对元数据，如数据更新频率、维护人、备用镜像地址等。

## 应用场景

- **赛事数据聚合监控**：运维或数据分析团队可将多个洲际联赛的实时比分、统计、前瞻类外链集中纳入 LinkPilot，统一查看健康状态与数据新鲜度，替代零散的浏览器书签。

- **技术文档与工具导航**：研发部门可利用 LinkPilot 搭建内部文档门户，将 API 文档、CI/CD 仪表盘、日志查看器、监控图表等常用工具链接分类展示，新员工入职时可快速上手。

- **外部数据源灾备切换**：当主用数据源响应超时或返回异常状态码时，LinkPilot 的健康检查日志可辅助判断故障范围，并通过预先配置的备用链接列表快速切换，减少业务中断时间。

- **内容聚合站点辅助**：内容编辑或运营人员可将多个行业资讯源、数据发布页、社交媒体监控链接聚合至 LinkPilot，通过访问统计识别高价值信息渠道，优化内容采编流程。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL2 环境，基于 Node.js 18+ 与 SQLite 轻量数据库。

```bash
# 1. 克隆项目仓库
git clone https://github.com/linkpilot/linkpilot-core.git
cd linkpilot-core

# 2. 安装依赖（使用 npm）
npm install

# 3. 初始化配置与数据库
cp .env.example .env
npm run db:init

# 4. 启动开发服务器（默认监听 3000 端口）
npm run dev
```

访问 `http://localhost:3000` 即可进入导航站首页。首次启动将自动生成管理员账号，默认用户名 `admin`，密码随机生成并输出在终端日志中，请及时修改。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，建议使用 nvm 管理多版本 |
| npm | 9.x 或以上 | 包管理器，用于安装项目依赖 |
| SQLite | 3.39+ | 嵌入式数据库，无需额外安装，项目内集成驱动 |
| Git | 2.30+ | 用于克隆仓库及版本管理 |
| 系统内存 | 最低 512MB，推荐 1GB+ | 生产环境建议 2GB 以上以支持健康检查并发 |
| 可用磁盘空间 | 200MB 以上 | 主要用于存储数据库文件及日志 |
| 操作系统 | Linux (Ubuntu 20.04+), macOS 12+, Windows 11 WSL2 | 开发与生产均以 Linux 环境为优先测试平台 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/` | 如何添加链接、分类、编辑元数据、查看统计与健康状态？ |
| 管理员指南 | `/docs/admin-guide/` | 如何配置角色权限、调整健康检查周期、导入导出批量数据？ |
| 开发文档 | `/docs/developer-guide/` | 如何扩展自定义分类器、新增元数据字段、编写插件或钩子函数？ |
| API 参考 | `/docs/api-reference/` | 所有 RESTful 接口的请求/响应格式、鉴权方式、分页参数详解 |
| 部署运维 | `/docs/deployment/` | 如何通过 Docker / PM2 / systemd 部署到生产服务器，以及日志轮转策略 |
| 常见集成 | `/docs/integrations/` | 如何与 Prometheus、Grafana、Slack 或钉钉机器人集成告警通知 |

## 资源列表

### 足球赛事比分类

- <code>qiutanjishibifenmobile.asia</code>
- <code>jinrizuqiubifenyucetuijian.asia</code>
- <code>500shoujibanbifen.asia</code>

### 澳大利亚足球超级联赛（澳超）数据专类

- <code>aodaliyazuqiuchaojiliansaizhugongbang.top</code>
- <code>aodaliyazuqiuchaojiliansaizhibo.top</code>
- <code>aodaliyazuqiuchaojiliansaisheshoubang.top</code>
- <code>aodaliyazuqiuchaojiliansaiqianzhan.top</code>
- <code>aodaliyazuqiuchaojiliansaijishibifen.top</code>

### 其他联赛统计类

- <code>aochaozhugongbang.asia</code>

### 综合数据平台类

- <code>dszuqiushengpingfu.cn</code>

## 项目结构

```
linkpilot-core/
├── src/                                # 核心源代码目录
│   ├── controllers/                    # 控制器层，处理 HTTP 请求与响应
│   │   ├── linkController.js           # 链接增删改查及健康检查触发
│   │   └── categoryController.js       # 分类树管理
│   ├── services/                       # 业务逻辑层
│   │   ├── healthCheckService.js       # 定时健康检查与状态更新
│   │   ├── statsService.js             # 访问统计与聚合计算
│   │   └── importExportService.js      # 批量导入导出处理
│   ├── models/                         # 数据模型层（SQLite ORM 映射）
│   │   ├── LinkModel.js                # 链接表结构及索引定义
│   │   ├── CategoryModel.js            # 分类表及父子关系
│   │   └── UserModel.js                # 用户与角色权限模型
│   ├── middleware/                     # 中间件
│   │   ├── auth.js                     # JWT 鉴权与角色校验
│   │   └── logger.js                   # 访问日志与错误日志记录
│   ├── utils/                          # 工具函数
│   │   ├── urlValidator.js             # URL 格式校验与域名黑名单
│   │   └── metaParser.js               # 从目标页面提取标题/描述等元信息
│   └── app.js                          # Express 应用入口及路由挂载
├── config/                             # 配置文件目录
│   ├── default.yaml                    # 默认配置（端口、检查间隔、超时）
│   └── production.yaml                 # 生产环境覆盖配置
├── db/                                 # 数据库相关
│   ├── migrations/                     # 版本迁移脚本（按日期命名）
│   └── seed.js                         # 初始分类与示例数据填充
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # 服务层与模型层单测
│   └── integration/                    # API 接口测试
├── docs/                               # 完整文档（参见文档导航章节）
├── logs/                               # 运行时日志输出目录（gitignore）
├── public/                             # 静态资源（前端样式、图标）
├── .env.example                        # 环境变量示例文件
├── Dockerfile                          # 容器化构建文件
├── package.json                        # npm 项目清单
└── README.md                           # 本文档
```

## 贡献指南

1.  **问题与建议提交**：请先在 GitHub Issues 中搜索是否已有相同提议。新建 Issue 时请使用提供的模板，清晰描述问题复现步骤、环境信息及期望行为，并附上相关日志片段。

2.  **分支开发流程**：从 `main` 分支切出 `feature/xxx` 或 `fix/xxx` 命名的新分支进行开发。提交信息请遵循 Conventional Commits 规范（如 `feat: add batch import progress bar`），确保每个提交原子化且可回滚。

3.  **代码风格与测试**：JavaScript 代码须通过 ESLint 配置（基于 Airbnb 风格）检查，并确保所有新增功能包含单元测试或集成测试，测试覆盖率不低于 80%。运行 `npm run test` 和 `npm run lint` 通过后方可提交。

4.  **拉取请求（PR）**：提交 PR 时需关联对应的 Issue 编号，并填写 PR 模板中的变更摘要、测试结果及影响范围说明。至少需要一名核心维护者 Approve 方可合并。

5.  **文档同步更新**：任何影响用户使用或管理员操作的功能变更，须同步更新 `/docs` 下对应章节以及本 README 中相关描述，确保文档与代码保持一致。

## 常见问题

**问：健康检查误报频繁，如何调整超时或重试策略？**

答：可在 `config/default.yaml` 中修改 `healthCheck.timeout`（毫秒）和 `healthCheck.retries`（次数）参数。若目标站点存在反爬机制，可在环境变量中配置 `HEALTH_CHECK_USER_AGENT` 自定义请求头。调整后重启服务生效，无需重新初始化数据库。

**问：导入大量链接（超过 1000 条）时页面卡顿或超时怎么办？**

答：推荐使用命令行导入模式，执行 `npm run cli:import -- --file ./data.json --format json`，该模式绕过 HTTP 层直接操作数据库，并支持分批提交事务。同时请确认 SQLite 的 `cache_size` 和 `mmap_size` 配置已根据机器内存调整，具体参考部署文档中的性能调优章节。

**问：能否与现有的 LDAP 或 OAuth2 认证系统集成？**

答：LinkPilot 从 2.0 版本开始支持自定义认证适配器。您可在 `src/middleware/auth.js` 中替换 `verifyToken` 函数实现，或通过配置 `AUTH_PROVIDER` 环境变量为 `ldap` 或 `oauth2`，并补充对应的 `config/ldap.yaml` 或 `config/oauth2.yaml` 配置文件。具体步骤参考开发文档中的“外部认证集成”部分。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
