# NovaLink 技术资源聚合门户

NovaLink 是一个面向开发人员与技术研究者的外链资源汇聚平台，专为需要快速检索、分类管理与批量验证互联网公开技术资源（如文档站、数据接口、社区论坛、工具站点）的团队或个人设计。项目通过结构化的资源索引机制，解决技术信息碎片化、链接失效频繁、跨域访问记录困难等实际问题，可作为内部知识库的外延模块或独立运维的技术导航子站点。

本项目不生成或托管任何实质内容，仅提供资源录入、标签过滤、可用性拨测与访问跳转中转功能，适用于技术文档维护团队、开源社区运营者及科研数据采集人员。

## 功能概览

- **资源批量导入** 支持通过 CSV 或 JSON 格式批量提交外链记录，自动解析协议头与域名主体，完成合法性预检。

- **状态监控面板** 内置基于 HTTP HEAD 请求的异步拨测任务，可配置周期（最短 5 分钟）检测各资源可达性，超时或 4xx/5xx 响应自动标记异常。

- **分类标签系统** 允许为每条资源标记多个自定义标签（如「API文档」「社区论坛」「数据源」「工具库」），并支持标签组合筛选与全文模糊检索。

- **访问统计看板** 记录每个外链的点击次数、最后访问时间、平均响应耗时，提供趋势折线图与 TOP 访问排行。

- **用户收藏夹** 注册用户可将常用资源加入个人收藏夹，支持分组管理（如「工作」「研究」「归档」）及批量导出为书签文件。

- **链接可用性历史** 持久化存储每次拨测结果，提供单资源可用性日历视图，便于排查周期性故障或服务商稳定性。

- **OPML 订阅导出** 将分类下的资源列表一键导出为标准 OPML 格式，兼容主流 RSS 阅读器与播客客户端。

- **Webhook 告警** 当资源连续三次拨测失败时，向配置的钉钉、飞书或通用 Slack 风格 Webhook 推送告警消息。

## 应用场景

- **技术团队内部知识库增强** 将团队日常依赖的 API 文档、运维看板、代码仓库、CI/CD 控制台等分散链接统一录入 NovaLink，通过标签区分开发/测试/生产环境，避免收藏夹混乱与链接遗忘。

- **开源社区资源导航站** 社区维护者可利用 NovaLink 构建项目周边生态导航页，聚合第三方工具、教程文章、视频课程及插件市场链接，通过状态监控自动下架失效资源，提升访客体验。

- **数据采集任务调度辅助** 数据工程师可将频繁访问的公开数据接口或爬虫入口注册至平台，利用访问耗时统计识别响应缓慢的服务端，辅助判断采集窗口与超时重试策略。

- **研究文献数字归档** 学术研究人员将论文中引用的在线数据集、实验代码仓库、预印本服务器等网址统一托管，便于复查链接活性并在论文修订期快速生成可访问性报告。

## 快速开始

以下命令适用于 Linux/macOS 及 Windows WSL 环境，建议使用 Node.js 20.x LTS 或更高版本。

```bash
# 克隆项目主仓库
git clone https://github.com/novalink-dev/novalink-core.git

# 进入项目工作目录
cd novalink-core

# 安装依赖（使用 npm 或 yarn）
npm install

# 复制示例环境变量配置并依据实际数据库连接信息修改
cp .env.example .env

# 初始化数据库表结构（SQLite 默认，可切换至 PostgreSQL）
npm run db:migrate

# 以开发模式启动服务（默认监听 3000 端口）
npm run dev
```

访问 http://localhost:3000 即可进入引导设置页面，首次运行需创建管理员账户并导入初始资源分类模板。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Node.js | 20.10.0 或更高 | 运行时环境，建议使用 LTS 版本 |
| npm | 10.2.0 或更高 | 包管理器，或使用 yarn 1.22+ 替代 |
| SQLite | 3.39.0 或更高 | 默认嵌入式数据库，适用于小规模部署（< 5000 条资源） |
| PostgreSQL | 15.0 或更高 | 可选生产级数据库，支持大规模并发与流复制 |
| Redis | 7.0 或更高 | 可选缓存与任务队列中间件，用于拨测任务调度 |
| 系统内存 | 至少 512 MB | 不含数据库进程，建议生产环境 2 GB 以上 |
| 存储空间 | 至少 1 GB | 用于存储拨测日志与统计历史，建议定期归档 |

## 文档导航

| 层面 | 目录/章节 | 回答的问题 |
| :--- | :--- | :--- |
| 用户手册 | `/docs/user/quick-start.md` | 如何注册账号、导入第一批资源、设置标签分类？ |
| 用户手册 | `/docs/user/monitoring.md` | 拨测周期如何配置？异常阈值与告警规则怎样设定？ |
| 管理员指南 | `/docs/admin/deployment.md` | 生产环境如何部署到云服务器？如何切换 PostgreSQL 与 Redis？ |
| 管理员指南 | `/docs/admin/backup.md` | 资源库与拨测历史数据如何备份与恢复？ |
| 开发者文档 | `/docs/dev/api-reference.md` | 对外提供的 RESTful API 有哪些？鉴权方式与参数格式为何？ |
| 开发者文档 | `/docs/dev/contributing.md` | 代码风格规范、提交信息格式、PR 流程要求是什么？ |
| 运维手册 | `/docs/ops/troubleshooting.md` | 常见启动报错、拨测超时、数据库连接池耗尽如何处理？ |

## 资源列表

### 体育赛事数据类

<code>lanqiubifeng.org.cn</code>

<code>lanqiubifenh.org.cn</code>

<code>zuqiubifenziboa.org.cn</code>

<code>zuqiubifenzibob.org.cn</code>

<code>zuqiubifenziboc.org.cn</code>

<code>zuqiubifenzibod.org.cn</code>

<code>zuqiubifenziboe.org.cn</code>

### 亚洲地区赛事信息类

<code>ajiasaicheng.asia</code>

<code>bajiazhugongbang.asia</code>

<code>baxizuqiujiajiliansai.asia</code>

## 项目结构

```
novalink-core/
├── src/
│   ├── api/                     # REST API 路由及控制器
│   │   ├── v1/                  # API 版本 v1 端点
│   │   │   ├── resources.js     # 资源增删改查接口
│   │   │   ├── tags.js          # 标签管理接口
│   │   │   ├── monitoring.js    # 拨测状态查询与手动触发
│   │   │   └── auth.js          # JWT 认证与刷新令牌
│   │   └── middleware/          # 鉴权、日志、限流中间件
│   ├── core/                    # 核心业务逻辑层
│   │   ├── crawler/             # 拨测引擎实现（HTTP 客户端池）
│   │   │   ├── checker.js       # 单资源可用性检测
│   │   │   └── scheduler.js     # 基于 node-cron 的任务调度
│   │   ├── exporter/            # OPML / JSON / CSV 导出模块
│   │   └── stats/               # 访问计数与响应耗时聚合计算
│   ├── db/                      # 数据库迁移与模型定义（Sequelize/Knex）
│   │   ├── migrations/          # 按时间戳命名的 schema 变更脚本
│   │   └── seeders/             # 初始分类与默认标签种子数据
│   ├── services/                # 外部服务集成（Redis、Webhook 客户端）
│   │   ├── cache.js             # 缓存读写策略（LRU + Redis 后备）
│   │   └── alert.js             # 钉钉/飞书 Webhook 告警适配
│   ├── ui/                      # 服务端渲染视图（EJS 模板）及静态资源
│   │   ├── views/               # 控制台页面、登录注册、仪表盘
│   │   └── public/              # CSS、客户端 JavaScript、图标字体
│   ├── utils/                   # 通用工具函数（URL 解析、时间格式化、校验器）
│   └── app.js                   # Express 应用入口，中间件挂载与路由注册
├── tests/                       # 单元测试与集成测试（Jest + Supertest）
│   ├── unit/                    # 拨测逻辑、URL 规范化、缓存策略测试
│   └── integration/             # API 端到端测试与数据库事务回滚测试
├── config/                      # 环境相关配置文件（development, production, test）
│   ├── database.js              # 数据库连接池参数与方言配置
│   └── monitoring.js            # 拨测并发数、超时阈值、重试策略
├── scripts/                     # 运维辅助脚本（数据迁移、批量导入、日志轮转）
├── docs/                        # 完整文档（详见文档导航章节）
├── .env.example                 # 环境变量模板（含 JWT_SECRET, DB_URL, REDIS_URL）
├── docker-compose.yml           # 本地开发所需 PostgreSQL + Redis 容器编排
├── Dockerfile                   # 生产环境多阶段构建镜像定义
├── package.json                 # 项目依赖、脚本命令与元信息
├── README.md                    # 项目总览（本文件）
└── LICENSE                      # MIT 许可协议文本
```

## 贡献指南

1. 阅读项目行为准则（CODE_OF_CONDUCT.md）并在提交前签署贡献者许可协议（CLA），确保代码可被合规合并。

2. 从 GitHub Issues 中认领标记为「help wanted」或「good first issue」的任务，或新建 Issue 描述您希望修复的问题或新增功能，等待维护者确认。

3. 派生项目仓库至个人账户，在派生副本中创建以 `feature/` 或 `fix/` 为前缀的分支，遵循约定式提交规范（如 `feat: add batch import retry mechanism`）。

4. 编写或更新对应的单元测试用例，确保新代码覆盖率不低于 85%，并运行 `npm run lint` 与 `npm run test` 通过全部检查项。

5. 向主仓库的 `develop` 分支发起 Pull Request，填写 PR 模板中的检查清单，等待至少两名维护者 Code Review 后即可合并。

## 常见问题

**问：导入大量资源（超过 1000 条）时页面提示超时，应该如何处理？**

答：建议使用命令行导入脚本 `npm run import:bulk -- --file=data.json`，该脚本绕过 HTTP 请求超时限制，直接写入数据库，并每 200 条自动提交一次事务。若仍需通过 Web 界面导入，可调整 `config/monitoring.js` 中的 `bulkImportTimeout` 参数（单位毫秒），或分批拆分文件后再次尝试。

**问：拨测任务占用过多内存，导致 Node 进程 OOM 退出，如何优化？**

答：请检查 `config/monitoring.js` 中的 `concurrency` 并发数，默认值为 50，可降低至 20 或 10。同时启用 Redis 作为任务队列后端（配置 `REDIS_URL`），此时拨测任务将转移至 Redis Bull 队列执行，显著减少主进程内存占用。若仍存在压力，建议将拨测独立部署为 Worker 子进程，参考 `docs/ops/scaling.md` 中的水平扩展方案。

**问：如何将现有 SQLite 数据完整迁移至 PostgreSQL 生产库？**

答：项目根目录下提供了迁移脚本 `scripts/migrate-sqlite-to-pg.js`。执行前请确保 PostgreSQL 数据库已创建并配置于 `.env` 的 `DB_URL` 中。运行 `node scripts/migrate-sqlite-to-pg.js --source=./data/novalink.db`，脚本会自动迁移资源表、标签表、用户表及拨测历史记录，迁移完成后建议手动抽查若干记录以验证外键约束完整性。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
