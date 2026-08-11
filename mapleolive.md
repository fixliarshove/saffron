# Vanguard Resource Hub

Vanguard Resource Hub is a lightweight, developer-oriented technical resource aggregation and navigation system designed for open-source contributors, technical researchers, and infrastructure operators who need to maintain structured access to a large and frequently evolving collection of external references, operational datasets, and real-time information endpoints. Unlike generic bookmark managers or CMS-based link collections, Vanguard treats external URLs as first-class assets with versioning, health checking, and metadata tagging, enabling teams to manage large-scale resource inventories in a reproducible, scriptable, and audit-friendly manner.

This project targets maintainers of documentation portals, DevOps engineers curating external dependency lists, and researchers who need to track multiple live data sources across different environments. It solves the problem of scattered, undocumented, or silently broken external references by providing a single source of truth for all external links, along with automated availability verification and structured export capabilities. The system is intentionally unopinionated about the nature of the resources it manages—it treats every URL as a first-class citizen with configurable categories, tags, and verification schedules, making it suitable for both internal enterprise use and public open-source documentation projects.

## 功能概览

- **URL Inventory Management** – Add, remove, and categorize external URLs with persistent storage and change history tracking. Each entry supports custom metadata fields including category, priority, and optional expiration date.

- **Automated Health Checking** – Periodically verify the accessibility and HTTP status of each managed URL, with configurable retry policies and timeout settings. Unreachable endpoints are flagged in the dashboard and exported reports.

- **Batch Import and Export** – Support for JSON, YAML, and CSV formats, enabling seamless integration with existing documentation pipelines and CI/CD workflows. Export filtered subsets by category or tag.

- **Tagging and Search** – Flexible tag system for organizing resources by domain, purpose, or team ownership. Full-text search across URL strings, titles, and description fields with relevance ranking.

- **Versioned Snapshots** – Maintain point-in-time snapshots of the entire resource list, allowing rollback to previous states and differential comparison between snapshots.

- **Webhook Notifications** – Send alerts to Slack, Discord, or generic HTTP endpoints when resources become unavailable or when new resources are added by team members.

- **RESTful API** – Full programmatic access to all management functions via a JSON API, with API key authentication and rate limiting for multi-user deployments.

- **Static Site Generator** – Generate a static HTML documentation page from the managed resource list, suitable for publishing as a standalone reference site without runtime dependencies.

## 应用场景

- **Documentation Portal Maintenance** – Technical writers and documentation engineers use Vanguard to maintain the external links section of large project documentation. The health check feature proactively notifies the team when external references go offline, allowing timely updates before users encounter broken links.

- **Operational Data Source Tracking** – DevOps teams managing monitoring dashboards and alerting systems rely on Vanguard to track the URLs of internal status pages, metrics endpoints, and health check targets. Automated verification ensures that all operational references remain valid during incident response.

- **Research Reference Management** – Academic and industrial researchers curate large collections of dataset URLs, API endpoints, and supplementary materials for reproducible experiments. Vanguard provides structured metadata and versioning to support citation accuracy and data provenance.

- **Open-Source Project Dependency Listing** – Maintainers of open-source projects use Vanguard to manage the "Resources" or "Related Links" sections of their README and documentation. The batch export feature simplifies synchronizing the resource list across multiple repository files and websites.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/vanguard-resource-hub/vanguard-core.git
cd vanguard-core

# Install dependencies using pipenv or pip
pip install -r requirements.txt

# Initialize the local database and configuration
python scripts/init_db.py --config config/default.yaml

# Run the development server
python app.py --host 0.0.0.0 --port 8080

# Alternatively, run with Docker
docker build -t vanguard-hub .
docker run -p 8080:8080 -v $(pwd)/data:/app/data vanguard-hub
```

After starting the server, access the web interface at `http://localhost:8080` and use the default admin credentials (admin / changeme) to log in. It is strongly recommended to change the default password immediately after the first login. For production deployments, review the `config/production.yaml` template for security settings including HTTPS enforcement, session management, and database backend configuration.

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行时，建议使用 3.11 或 3.12 以获得最佳性能 |
| SQLite | 3.35 及以上 | 默认嵌入式数据库，用于单机部署；生产环境可替换为 PostgreSQL |
| Redis | 6.0 及以上 | 可选，用于缓存和分布式锁；若禁用则健康检查并发度受限 |
| Node.js | 18.x 或 20.x LTS | 仅用于构建静态站点前端资源；若仅使用 API 模式可跳过 |
| Docker | 20.10 及以上 | 用于容器化部署和开发环境一致性，非强制但强烈推荐 |
| curl / wget | 任意现代版本 | 健康检查模块调用系统工具进行 HTTP 探测，需确保已安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user/` | 如何添加资源、配置标签、查看健康状态、生成静态站点？ |
| 管理员指南 | `docs/admin/` | 如何部署生产环境、配置 HTTPS、调优数据库连接池、设置备份策略？ |
| API 参考 | `docs/api/` | 所有 REST 端点的请求/响应格式、认证方式、分页参数、错误码含义？ |
| 贡献者文档 | `docs/contributor/` | 代码风格要求、测试框架使用方法、PR 提交流程、新增功能的设计模板？ |

## 资源列表

### 实时比分与数据源类

- <code>qiutanzuqiubifenjiubanw.org.cn</code>
- <code>zuqiushishifen.org.cn</code>
- <code>beidanbifenjishizuqiubifen.org.cn</code>
- <code>xinqiubifen.org.cn</code>
- <code>7mbifenzuqiubifenjishi.org.cn</code>
- <code>bifenzuqiujishi.org.cn</code>
- <code>500bifenzuqiujishi.org.cn</code>
- <code>qiutanzuqiushoujiban.org.cn</code>
- <code>zuqiubaba.org.cn</code>
- <code>zuqiubifenqiutanbifenjishi.org.cn</code>

## 项目结构

```
vanguard-core/
├── app/
│   ├── __init__.py                 # 应用工厂模式初始化
│   ├── routes/
│   │   ├── api_v1.py               # REST API 路由定义 (资源 CRUD)
│   │   ├── web_ui.py               # 管理界面路由 (Flask/Werkzeug)
│   │   └── health.py               # 健康检查触发器与回调端点
│   ├── models/
│   │   ├── resource.py             # URL 资源 ORM 模型 (SQLAlchemy)
│   │   ├── snapshot.py             # 快照版本模型及 diff 逻辑
│   │   └── tag.py                  # 标签与资源关联模型
│   ├── services/
│   │   ├── checker.py              # 异步健康检查调度器 (APScheduler)
│   │   ├── exporter.py             # JSON/YAML/CSV 导出服务
│   │   └── static_gen.py           # 静态 HTML 站点生成器 (Jinja2)
│   └── utils/
│       ├── validators.py           # URL 格式校验与规范化工具
│       ├── webhook.py              # 通用 Webhook 发送客户端
│       └── logging.py              # 结构化日志配置 (JSON 格式)
├── config/
│   ├── default.yaml                # 默认配置 (开发环境)
│   ├── production.yaml.template    # 生产环境配置模板
│   └── logging.yaml                # 日志级别与输出目标配置
├── scripts/
│   ├── init_db.py                  # 数据库初始化与迁移脚本
│   ├── import_batch.py             # 批量导入外部列表 (CSV/JSON)
│   └── export_snapshot.py          # 命令行快照导出工具
├── tests/
│   ├── unit/                       # 单元测试 (pytest)
│   ├── integration/                # 集成测试 (需本地 Redis)
│   └── fixtures/                   # 测试用静态数据样本
├── static/                         # 前端静态资源 (CSS/JS)
├── templates/                      # Jinja2 模板 (管理界面)
├── docker-compose.yml              # 完整栈编排 (app + redis + postgres)
├── Dockerfile                      # 多阶段构建镜像定义
├── requirements.txt                # Python 依赖锁
├── pyproject.toml                  # 项目元数据与构建配置
├── README.md                       # 本文件
└── LICENSE                         # MIT 许可证文本
```

## 贡献指南

1.  **Fork 仓库并创建功能分支** – 从主仓库 fork 到个人账户，然后基于 `main` 分支创建一个描述性的新分支，例如 `feature/add-http3-checker` 或 `fix/snapshot-rollback-error`。请确保分支名称简洁且反映变更内容。

2.  **遵循代码规范与测试要求** – 所有 Python 代码必须通过 `black` 和 `flake8` 格式化检查，并附带充分的单元测试覆盖新增或修改的逻辑。运行 `pytest tests/` 确保所有现有测试通过。对于新增功能，需在 `docs/contributor/` 下补充相应的设计说明。

3.  **提交变更并签署开发者原产地证书 (DCO)** – 每个提交消息必须包含 `Signed-off-by: Your Name <email>` 行，表示您同意 Developer Certificate of Origin 条款。提交信息应使用祈使语气，简明描述变更内容和动机。

4.  **创建 Pull Request 并等待审查** – 推送分支到您的 fork 仓库，然后向主仓库的 `main` 分支发起 PR。在 PR 描述中详细说明变更背景、测试结果和影响范围。至少需要两名维护者批准后方可合并。CI 流水线将自动运行测试和代码检查，请确保所有检查均为绿色状态。

5.  **更新文档与资源列表** – 若您的变更涉及新增配置项、API 端点或用户可见行为，请同步更新 `README.md` 和 `docs/` 下的相关手册。如果变更影响了外部资源列表的格式或管理方式，请在本文件末尾的“资源列表”章节中反映最新状态。

## 常见问题

**Q: 健康检查模块如何区分临时性故障和永久性失效？**

A: 检查器默认采用三重策略：每个 URL 在单次检查周期内最多重试 3 次，间隔 5 秒；若连续 3 个检查周期（默认每 10 分钟一个周期）均失败，则标记为“持续不可达”并触发 Webhook 通知。用户可以在配置文件中调整 `checker.retry_count`、`checker.retry_interval` 和 `checker.failure_threshold` 参数以适应不同外部服务的稳定性特征。对于已知的维护窗口，可以手动为特定 URL 设置暂停检查的时间窗口。

**Q: 是否可以管理需要认证或带有动态令牌的外部资源？**

A: 当前版本原生支持基础认证（用户名/密码）和自定义请求头（如 API Key）。对于 OAuth2 或动态令牌场景，建议通过前置代理（如 nginx 或 Cloudflare Workers）在中间层完成认证，然后将代理后的稳定端点纳入 Vanguard 管理。项目路线图中包含对 OAuth2 客户端凭证流程的原生支持，预计在 2.0 版本中实现。

**Q: 静态站点生成器输出的 HTML 是否包含所有资源元数据？**

A: 是的，生成的静态页面包含每个 URL 的标题、描述、标签、类别和最后一次健康检查状态。页面使用纯 CSS 实现响应式布局，无外部 JavaScript 依赖，因此即使完全离线打开也能完整展示所有信息。生成器还支持自定义模板，用户可以通过替换 `templates/static/` 下的文件来调整输出样式和布局结构。

## 许可证

MIT License

Copyright (c) 2026 Vanguard Resource Hub Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
