# HyperLink Nexus

HyperLink Nexus 是一个面向技术社区与开发者生态的垂直领域外链资源聚合系统。项目定位于对分散在多个独立域名下的实时数据页面、比分看板、赛事信息流进行统一收录、结构化索引与稳定性监控。目标用户包括数据应用开发者、信息聚合平台运维人员、以及需要对接第三方实时数据源的技术团队。本项目不提供数据源本身，而是通过人工审核与自动化校验结合的方式，维护一份高可用、低延迟的外链资源清单，解决外部数据源分散、域名频繁变更、访问可用性不可见等实际问题。

## 功能概览

- 外链资源注册与管理：支持手动录入和批量导入外部数据页面 URL，自动解析域名类别与响应类型。

- 可用性主动探测：每五分钟对已收录的域名执行 TCP 连接检测与 HTTP HEAD 请求，记录响应时间与状态码。

- 响应内容校验：针对特定路径返回的 JSON 或纯文本结构进行关键字匹配，初步判断数据完整性。

- 变更通知机制：当探测到域名解析变更、证书过期或连续三次超时时，通过系统日志与预留接口输出告警。

- 资源标签分类：每个外链可附加多个功能标签，例如实时比分、历史数据、统计面板，便于后续检索。

- 历史可用性报表：按日、周、月维度生成每个域名的平均响应时间与丢包率趋势，辅助运维决策。

- 只读 API 输出：对外提供 JSON 格式的资源列表与实时状态，供下游数据管道或看板系统调用。

- 管理员操作审计：所有资源增删改操作记录操作人、时间与变更前后内容，满足内部合规要求。

## 应用场景

- 数据看板运维团队：通过 HyperLink Nexus 统一管理多个外部实时数据页面地址，当某个域名响应异常时自动标记，减少人工巡检成本，提升看板数据加载成功率。

- 赛事信息聚合服务：开发者在构建多源赛事信息聚合应用时，利用本系统提供的稳定外链清单作为数据抓取源，避免硬编码域名导致后期维护困难。

- 网络质量监控前置机：将本系统部署在边缘节点，持续探测各外链域名的网络延迟与丢包情况，将探测结果作为上层调度策略的输入参数。

- 内部知识库外链治理：技术团队使用本系统对内部文档中引用的第三方实时数据链接进行周期性可用性检查，及时清理失效链接，保障文档质量。

## 快速开始

以下步骤适用于 Linux 或 macOS 开发环境，建议使用 Python 3.10 及以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/example/hyperlink-nexus.git
cd hyperlink-nexus

# 创建并激活 Python 虚拟环境
python3 -m venv venv
source venv/bin/activate

# 安装项目依赖
pip install -r requirements.txt

# 初始化本地 SQLite 数据库
python scripts/init_db.py

# 导入示例资源记录
python scripts/load_sample_resources.py

# 启动可用性探测 Worker（前台运行，便于观察日志）
python worker.py --interval 300

# 另开终端，启动 REST API 服务（默认监听 8000 端口）
python api_server.py --host 127.0.0.1 --port 8000
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 或更高 | 核心运行环境，用于异步探测及 API 服务 |
| aiohttp | 3.9.0 或更高 | 异步 HTTP 客户端，用于并发探测外部链接 |
| sqlite3 | 系统内置 | 本地元数据存储，无需额外安装 |
| dns.resolver | dnspython 2.4.0 | 用于解析域名 A 记录，辅助检测 DNS 变更 |
| pyOpenSSL | 23.0.0 或更高 | 用于校验 HTTPS 证书有效性及过期时间 |
| uvicorn | 0.24.0 或更高 | ASGI 服务器，用于运行 FastAPI 接口 |
| pydantic | 2.5.0 或更高 | 数据模型校验，保证配置与 API 输入输出一致性 |
| python-dotenv | 1.0.0 或更高 | 加载环境变量，区分开发与生产配置 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 运维部署 | docs/deployment.md | 如何在生产环境使用 Docker Compose 或 Kubernetes 部署全套探测与 API 服务 |
| 探测规则 | docs/probing_rules.md | 如何自定义探测超时时间、重试次数、关键字匹配规则以及告警阈值 |
| API 参考 | docs/api_reference.md | 所有对外 RESTful 接口的路径、请求参数、响应结构与状态码含义 |
| 资源管理 | docs/resource_management.md | 如何通过命令行工具或管理界面添加、禁用、更新外链资源及其标签 |

## 资源列表

本项目维护的资源清单如下，按功能用途划分小节。每个链接均保留用户原始输入格式，不做任何协议或域名前缀修改。

实时比分数据类

<code>90bifenjishizuqiubifenwang.org.cn</code>

<code>7mzuqiubifenjishibifenguanwang.org.cn</code>

<code>jishibifenzuqiubifenw.net.cn</code>

综合比分面板类

<code>bifen500w.net.cn</code>

<code>bifenwangw.net.cn</code>

<code>bifenzhibow.net.cn</code>

赛事进程与统计类

<code>500jishibifenwanchang.net.cn</code>

<code>90bifenjishizuqiubifenwang.net.cn</code>

<code>500bifen.net.cn</code>

备用及专项数据类

<code>beidanbifenjishi.net.cn</code>

## 项目结构

```
hyperlink-nexus/
├── api/                              # REST API 路由与请求模型
│   ├── __init__.py
│   ├── routes/
│   │   ├── resources.py              # 资源增删改查接口
│   │   └── status.py                 # 实时状态查询接口
│   └── schemas/
│       └── resource.py               # Pydantic 数据模型定义
├── core/                             # 核心业务逻辑
│   ├── __init__.py
│   ├── probe/
│   │   ├── http_checker.py           # 异步 HTTP 探测实现
│   │   ├── dns_resolver.py           # DNS 解析与缓存
│   │   └── certificate_validator.py  # SSL 证书校验
│   └── registry/
│       ├── resource_manager.py       # 资源注册表 CRUD
│       └── tag_engine.py             # 标签分类与检索
├── data/                             # 本地持久化存储
│   ├── resources.db                  # SQLite 数据库文件
│   └── migrations/                   # 数据库版本升级脚本
│       └── v1_initial_schema.sql
├── scripts/                          # 运维与工具脚本
│   ├── init_db.py                    # 初始化数据库表结构
│   ├── load_sample_resources.py      # 加载示例外链数据
│   └── export_report.py              # 导出可用性统计报表
├── tests/                            # 单元测试与集成测试
│   ├── test_http_checker.py
│   ├── test_dns_resolver.py
│   └── test_api_routes.py
├── worker.py                         # 定时探测 Worker 主入口
├── api_server.py                     # FastAPI 服务启动脚本
├── requirements.txt                  # Python 依赖清单
├── .env.example                      # 环境变量配置模板
└── README.md                         # 项目说明文档（本文件）
```

## 贡献指南

1. 在 GitHub 仓库中 fork 本项目，并基于 main 分支创建以 feature/ 或 fix/ 为前缀的本地开发分支，分支命名需与所修改功能模块对应。

2. 新增探测协议或扩展资源管理能力时，请先在 docs/ 目录下补充相应的设计说明文档，明确修改点、数据流变动以及对现有 API 的影响范围。

3. 所有新增代码需在 tests/ 目录下补充对应的单元测试或集成测试用例，保证测试覆盖率不低于 80%，并确保原有测试全部通过后方可发起 Pull Request。

4. 提交信息请遵循 Conventional Commits 规范，采用 feat:、fix:、docs:、refactor: 等类型前缀，并简要描述本次变更的问题背景与解决方式。

5. 合并请求需要至少一位项目维护者进行代码审查，审查通过后由维护者执行 squash merge 操作，并同步更新 CHANGELOG.md 中的版本记录。

## 常见问题

Q: 探测 Worker 是否支持分布式部署以应对大量外链？

A: 支持。您可以将 SQLite 数据库替换为 PostgreSQL，并启动多个 Worker 实例，通过数据库行级锁或 Redis 分布式锁来避免重复探测同一资源。具体配置可参考 docs/deployment.md 中的分布式章节。

Q: 如果某个外链域名频繁变动，系统如何应对？

A: 系统提供域名别名管理功能，您可以在资源编辑界面为该资源添加多个备用域名，Worker 在探测时会按优先级依次尝试，直到获得成功响应或全部失败。同时，DNS 解析结果会记录历史，便于回溯。

Q: 是否可以自定义告警通知方式，例如邮件或企业微信？

A: 当前版本仅输出结构化日志和内部告警事件队列。您可以在 core/notify/ 目录下实现自定义通知适配器，并将适配器注册到 Worker 的告警管道中，后续版本将提供更丰富的内置通知插件。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
