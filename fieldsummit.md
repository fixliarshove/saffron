# Terminus Resource Aggregator

Terminus Resource Aggregator is a high-performance, community-driven indexing platform designed for technical content curation and external resource orchestration. It addresses the growing need among developers, researchers, and technical writers to systematically catalog, validate, and surface distributed online references without introducing vendor lock-in or dependency on proprietary bookmarking ecosystems. The project targets power users who manage large external link inventories, perform periodic content audits, and require a lightweight, auditable metadata layer over raw URL collections. By treating external resources as first-class entities with version-aware annotations, Terminus transforms static link lists into maintainable knowledge graphs that integrate seamlessly with CI/CD pipelines and documentation generators.

## 功能概览

- **Bulk Resource Ingestion** – Import up to 10,000 external links per batch via CLI or RESTful API, with automatic deduplication and origin timestamping.
- **Schema Validation Engine** – Enforce custom metadata schemas (e.g., content type, language, availability status) for each indexed URL, with JSON Schema v7 support.
- **Periodic Liveness Probes** – Schedule HEAD/GET checks to detect broken or redirected links; export dead-link reports in CSV and JSON formats.
- **Tag-Based Classification** – Assign hierarchical tags to resources; support faceted search and filter combinations via indexed metadata fields.
- **Batch Export Pipelines** – Generate markdown table snippets, static site JSON feeds, or sitemap.xml from selected resource subsets, ready for downstream documentation builds.
- **Audit Trail Logging** – Record all ingestion, update, and deletion events in an append-only journal, facilitating compliance and rollback scenarios.
- **CLI Interactive Mode** – TUI-based interface for rapid manual curation, including inline URL editing, tag toggling, and note attachment.

## 应用场景

1. **Technical Documentation Maintenance** – Documentation teams use Terminus to manage external reference links across hundreds of versioned pages. When a dependency domain changes, the liveness probe triggers alerts, allowing proactive updates before end-users encounter 404 errors.

2. **Research Paper Bibliography Curation** – Academic researchers aggregate preprint servers, dataset repositories, and supplementary material links for multi-author projects. The tagging system enables per-chapter or per-experiment filtering, while batch export generates formatted reference sections for LaTeX and Markdown submissions.

3. **Open Source Community Resource Hub** – Community managers maintain a curated list of tutorials, tools, and discussion forums for their project ecosystem. The audit log tracks contributor-suggested additions, and the validation engine ensures every new entry meets quality criteria (e.g., HTTPS enforcement, domain allowlist).

4. **Localized Content Mirror Indexing** – Operators of regional content aggregators catalog external media sources that provide region-specific materials. The system records availability status and language metadata, enabling dynamic switching between primary and fallback sources in client applications.

5. **Compliance Link Inventory** – Legal and compliance teams track regulatory references, standards bodies, and official policy documents. The export pipeline generates periodic snapshots for internal audits, with timestamps proving when each resource was last verified.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/terminus-io/terminus-aggregator.git
cd terminus-aggregator

# Install dependencies (uses Python 3.11+ and Poetry)
poetry install --no-dev

# Initialize the local SQLite database and run the built-in ingestion example
poetry run terminus init --db-path ./data/terminus.db
poetry run terminus import --source ./examples/seed-urls.txt --batch-id 287

# Start the development web dashboard (optional)
poetry run terminus serve --port 8080
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.11 - 3.12 | 核心运行时；类型提示与异步特性依赖于 3.11+ |
| SQLite | 3.35.0+ | 内置数据库引擎；支持 JSON 函数和窗口操作以优化查询 |
| Poetry | 1.6.0+ | 依赖管理与打包工具；用于锁定精确版本并生成 requirements.txt |
| aiohttp | 3.9.0+ | 异步 HTTP 客户端；用于并发探活与资源抓取 |
| pydantic | 2.5.0+ | 数据验证与设置管理；负责 schema 解析与配置校验 |
| click | 8.1.0+ | CLI 命令框架；提供子命令、选项和交互式提示 |
| jinja2 | 3.1.0+ | 模板引擎；用于生成导出的 markdown 报告与静态页面 |
| pyyaml | 6.0.0+ | YAML 序列化；支持自定义标签集与导入模板定义 |
| rich | 13.7.0+ | 终端美化输出；用于 TUI 模式下的彩色表格与进度条 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user-guide/ | 如何进行批量导入、配置探针策略、使用标签系统以及导出数据？ |
| 运维指南 | docs/operations/ | 如何部署生产环境、调优数据库连接池、设置日志轮转及监控指标？ |
| 开发者文档 | docs/developer/ | 如何扩展自定义校验器、添加新的导出格式、参与核心模块重构？ |
| API 参考 | docs/api/ | RESTful 端点的请求/响应结构、认证方式、分页参数及错误码含义？ |
| 设计决策 | docs/design/ | 为何选择 SQLite 作为默认存储、探针调度算法的权衡、索引策略的考量？ |
| 贡献规范 | docs/contributing/ | 代码风格、提交信息格式、PR 审查流程以及测试覆盖率要求？ |

## 资源列表

本批次（第 287/455 批）收录以下外部资源链接，按内容主题分类整理。所有链接保持用户提供的原始形态，未做协议补全或域名规范化处理。

### 视频与媒体类资源

- <code>shipinzaixianmianfeiguankanw.org.cn</code>

### 字幕与语言资源

- <code>zhongwenzimurenqiwuma.org.cn</code>
- <code>zhongchuzaixianzhongwenzimu.org.cn</code>
- <code>youmazhongwenzimu.org.cn</code>
- <code>zaixianguankanzhongwenzimu1.org.cn</code>
- <code>zhongwenzimuzaixianmianfeikan1.org.cn</code>
- <code>zhongwenzaixianzimumianfeigaoqing1.org.cn</code>

### 内容专题资源

- <code>nannvchuangshangdapuke.org.cn</code>
- <code>xiaojirushuimitaozaixian.org.cn</code>
- <code>guochanheisizaixianguankan.org.cn</code>

## 项目结构

```
terminus-aggregator/
├── src/
│   ├── core/                     # 核心数据模型与数据库抽象层
│   │   ├── models.py             # SQLAlchemy ORM 定义（Resource, Tag, ProbeLog）
│   │   ├── database.py           # 连接池管理、迁移脚本入口
│   │   └── validators.py         # URL 规范化、schema 校验器链
│   ├── ingestion/                # 批量导入管道
│   │   ├── parsers.py            # 支持 TXT, CSV, JSONL 格式解析
│   │   ├── dedupe.py             # 基于内容指纹与规范化 URL 的去重逻辑
│   │   └── batch_processor.py    # 分块事务处理，支持断点续传
│   ├── probes/                   # 主动探活子系统
│   │   ├── scheduler.py          # asyncio 定时任务调度器
│   │   ├── http_checks.py        # 并发 HEAD/GET 请求，超时与重试策略
│   │   └── reporter.py           # 生成死链报告与可用性趋势统计
│   ├── export/                   # 导出管道
│   │   ├── markdown.py           # 生成表格片段与资源列表章节
│   │   ├── static_site.py        # 输出静态 HTML 目录树
│   │   └── sitemap.py            # 生成符合 sitemap 协议的 XML
│   ├── cli/                      # 命令行交互层
│   │   ├── main.py               # click 入口，注册所有子命令
│   │   ├── tui.py                # 基于 rich 的交互式面板
│   │   └── config.py             # 配置文件加载（支持 YAML/ENV）
│   └── web/                      # 可选 Web 仪表板（FastAPI）
│       ├── app.py                # 路由注册与中间件
│       ├── dependencies.py       # 依赖注入（DB session, config）
│       └── templates/            # Jinja2 模板
├── tests/                        # 单元测试与集成测试（pytest）
│   ├── unit/
│   └── integration/
├── scripts/                      # 运维辅助脚本
│   ├── backup_db.sh
│   └── migrate_tags.py
├── data/                         # 运行时数据目录（SQLite 文件，探针缓存）
├── docs/                         # 完整文档（参见上述文档导航）
├── pyproject.toml                # Poetry 项目配置
├── README.md                     # 本文件
└── LICENSE                       # MIT 许可证
```

## 贡献指南

1. **查阅议题与项目看板** – 访问 GitHub Issues 和 Projects 面板，查找带有 `help wanted` 或 `good first issue` 标签的任务。对于新功能提议，请先创建一个议题并附上用例说明，等待核心维护者反馈后再进行开发。

2. **派生仓库并创建特性分支** – 将主仓库派生至个人账户，然后克隆派生仓库。使用语义化分支命名，例如 `feat/add-graphql-export` 或 `fix/probe-timeout-handling`。确保分支基于最新的 `main` 分支。

3. **编写测试与代码** – 所有新逻辑必须附带对应的单元测试或集成测试，测试覆盖率不得低于 85%。代码风格遵循 `black` 与 `isort` 的默认配置，并确保 `mypy` 严格模式通过。提交前运行 `poetry run pre-commit run --all-files` 自动执行 lint 检查。

4. **提交变更并推送** – 提交信息采用 Conventional Commits 格式（`type(scope): description`），正文说明变更动机和影响范围。推送后打开 Pull Request，并填写 PR 模板中的检查清单。核心维护者将在 3 个工作日内进行审查。

5. **参与审查迭代** – 根据审查意见进行修改，保持 PR 分支与 main 分支同步（rebase 而非 merge）。当所有 CI 流水线（测试、lint、构建）通过且获得至少两名核心成员批准后，您的贡献将被合并。

## 常见问题

**问：生产环境是否必须使用 SQLite？能否使用 PostgreSQL 或 MySQL？**

答：SQLite 是默认内置存储，适合单机部署和小规模数据（< 50 万条资源）。对于高并发写入或多实例部署场景，我们提供 PostgreSQL 适配器（通过 `src/core/adapters/postgres.py`）。您只需修改配置文件中的 `database.url` 为 `postgresql://...`，系统会自动切换连接池和方言支持。MySQL 兼容性目前处于实验阶段，不建议在生产中使用。

**问：探活检查是否会触发目标网站的限流或封禁？**

答：默认探活使用 `HEAD` 方法，且每个目标域名的并发请求数限制为 2，间隔时间不低于 10 秒。您可以通过 `probes.rate_limit` 配置项调整请求频率。对于敏感站点，建议在配置中添加 `exclude_domains` 列表，或使用 `--dry-run` 模式模拟检查而不发送实际请求。此外，所有请求均携带 `User-Agent: Terminus-Probe/1.0` 标识，便于站点管理员识别和联系。

**问：如何迁移已有的书签或收藏夹数据？**

答：Terminus 内置了转换器模块（`src/ingestion/converters/`），支持从浏览器书签 HTML 导出文件、Pinboard JSON 备份、以及 Raindrop.io CSV 格式的直接转换。您可以使用 `terminus convert --from bookmarks.html --to seed-urls.txt` 生成中间格式，再通过 `terminus import` 导入。对于自定义格式，请参考 `docs/developer/import-format.md` 编写映射规则。

## 许可证

MIT License. See the LICENSE file for full text.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:28
