# HyperLink Hub

HyperLink Hub 是一个面向技术内容创作者、开源社区运营者和信息聚合平台维护者的高性能外链资源管理与导航系统。该项目旨在解决复杂技术生态中资源分散、链接失效、引用不规范等问题，通过结构化的数据模型和标准化的输出接口，帮助用户建立可维护、可扩展、可审计的外部资源引用体系。

目标用户包括开源项目文档维护者、技术博客作者、在线教育平台运营方以及企业内部知识库管理员。HyperLink Hub 不提供具体的业务内容，而是作为一层轻量级的数据治理中间件，确保所有外链资源在项目生命周期内保持可访问性、版本一致性和分类清晰度。

## 功能概览

- **批量链接导入与去重** 支持从 CSV、JSON 及纯文本列表批量导入 URL，自动识别协议头、域名变体及冗余参数，生成唯一的资源指纹。

- **链接状态健康检查** 内置异步任务队列，定期对已收录的 URL 执行 HTTP 状态码检测，标记失效链接并生成告警日志。

- **分类标签与全文检索** 允许为每条资源添加多级标签和中文描述，基于倒排索引提供毫秒级的关键词检索能力。

- **多格式数据导出** 支持将资源列表导出为 Markdown 表格、HTML 目录、JSON API 响应或纯文本 sitemap，便于集成到不同发布平台。

- **版本历史与回滚** 每次对资源列表的增删改操作均生成快照，支持按时间点回溯到任意历史版本。

- **权限分级管理** 提供管理员、编辑者、访客三种角色，编辑操作留痕，访客只读访问。

- **自定义渲染模板** 允许用户编写 Jinja2 或 Mustache 模板，控制资源列表在最终文档中的展示样式和排序规则。

- **Webhook 变更通知** 当资源列表发生变更时，自动向配置的 Slack、钉钉或邮件地址推送差异摘要。

## 应用场景

- **开源项目 README 维护** 当项目需要引用大量第三方库、教程或社区论坛时，HyperLink Hub 可集中管理这些外链，避免 README 因链接冗长而可读性下降，同时自动检查链接有效性，防止文档中出现死链。

- **技术博客系列文章的资源附录** 对于连载性质的技术博客，作者可以维护一个全局的资源仓库，每篇文章只需引用资源 ID，最终由 HyperLink Hub 在构建时注入完整 URL，确保多篇文章间的链接引用风格统一。

- **企业内部知识库的合规审查** 企业法务或合规部门要求对知识库中的所有外部链接进行定期审计。HyperLink Hub 的版本历史和健康检查日志可直接作为审计证据，同时支持按域名或分类快速过滤链接，加速审查流程。

- **在线课程平台的参考资料管理** 在线课程中每节课可能包含数十个延伸阅读链接。使用 HyperLink Hub 后，课程编辑可以独立更新链接数据而不影响课程页面布局，学员也能通过统一的资源导航页访问所有参考资料。

- **社区聚合站点的每日更新** 运营一个技术新闻或资源聚合网站时，编辑团队每天需要添加大量新链接。HyperLink Hub 的多角色协作和 Webhook 通知功能可以配合 CI 流水线，实现资源提交后自动构建并部署站点。

## 快速开始

以下步骤将帮助您在本地环境中快速启动 HyperLink Hub 服务。

```bash
# 1. 克隆项目仓库
git clone https://github.com/hyperlink-hub/hyperlink-hub.git
cd hyperlink-hub

# 2. 安装 Python 依赖（推荐使用虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 下请使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化 SQLite 数据库并创建默认管理员账户
python manage.py initdb
python manage.py createadmin --username admin --password HyperLink123

# 4. 导入示例资源列表（包含本批次 10 个链接的示例数据）
python manage.py import --file samples/url_list_batch_30_455.json

# 5. 启动开发服务器
python manage.py runserver --port 8080
```

服务启动后，访问 `http://localhost:8080` 即可进入仪表盘。默认管理员账号为 `admin`，密码为 `HyperLink123`。首次登录后请立即修改密码。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.9 - 3.12 | 核心运行环境，不支持 3.8 以下版本 |
| SQLite | 3.35.0 及以上 | 内置数据库，用于存储资源元数据和版本快照 |
| Redis | 6.2 及以上 | 用于缓存健康检查结果和异步任务队列（生产环境必需） |
| Node.js | 18.x 或 20.x LTS | 仅用于前端静态资源构建（开发模式可选） |
| Git | 2.30 及以上 | 用于版本追踪和钩子脚本执行 |
| gunicorn | 21.x 及以上 | 生产环境推荐使用，Windows 下可替换为 waitress |
| certifi | 2023.x 及以上 | 用于 HTTPS 证书验证，确保链接检查的准确性 |
| requests | 2.31.x 及以上 | 执行 HTTP 健康检查的核心库 |
| Markdown | 3.5.x 及以上 | 用于生成 README 和文档导出模块 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `/docs/user-guide/` | 如何导入链接、配置健康检查、导出不同格式的资源列表 |
| 管理员指南 | `/docs/admin-guide/` | 如何管理用户权限、设置 Webhook、执行数据库备份与恢复 |
| 开发者文档 | `/docs/developer-guide/` | 如何扩展自定义检查器、编写新的导出插件、参与核心模块开发 |
| API 参考 | `/docs/api-reference/` | 所有 RESTful 接口的请求/响应示例，包括分页、过滤和错误码定义 |
| 部署指南 | `/docs/deployment/` | 如何在 Docker、Kubernetes 或传统虚拟机环境中部署生产服务 |
| 变更日志 | `/docs/changelog/` | 每个版本的新增功能、修复的缺陷和不兼容变更说明 |

## 资源列表

以下为本项目当前批次收录的全部外部资源链接。所有 URL 均来自用户原始数据，按类别组织以便查阅。每个 URL 严格保留原始格式，未做任何协议或域名改写。

### 国产影视资源类

- <code>guochangaoqingshipinzaixian.org.cn</code>
- <code>guochangaoqingshipinguankan.org.cn</code>

### 日漫在线观看类

- <code>rimanzaixianmianfeiguankan.org.cn</code>
- <code>rihanzaixianmianfeishipinw.org.cn</code>

### 中文字幕资源类

- <code>zhongwenzimumianfeibofang.org.cn</code>
- <code>zaixianzimumianfeiguankan.org.cn</code>
- <code>zaixianzimuguankanmianfei.org.cn</code>
- <code>zaixianzimugaoqingdianshiju.org.cn</code>

### 免费视频聚合类

- <code>mianfeishipinwangzhanzaixianguankan.org.cn</code>
- <code>oumeizaixianmianfeishipinw.org.cn</code>

## 项目结构

```
hyperlink-hub/
├── app/
│   ├── api/                           # RESTful API 路由与视图函数
│   │   ├── v1/                        # API 版本 1 的实现
│   │   │   ├── endpoints/             # 按资源类型拆分的路由模块
│   │   │   └── schemas/               # Pydantic 请求/响应数据模型
│   │   └── middleware/                # 认证、日志、跨域中间件
│   ├── core/                          # 核心业务逻辑层
│   │   ├── checker/                   # 链接健康检查引擎（含重试策略）
│   │   ├── importer/                  # 批量导入处理器（支持 CSV/JSON）
│   │   ├── exporter/                  # 多格式导出生成器
│   │   └── fingerprint/               # URL 去重与规范化算法
│   ├── models/                        # SQLAlchemy ORM 数据表定义
│   │   ├── resource.py                # 资源主表、标签表、分类表
│   │   ├── snapshot.py                # 版本快照与差异记录
│   │   └── user.py                    # 用户、角色、权限关联表
│   ├── templates/                     # 管理后台 Jinja2 页面模板
│   │   ├── dashboard/                 # 仪表盘、资源列表、详情页
│   │   └── auth/                      # 登录、密码重置、邀请注册页
│   └── static/                        # 前端 CSS、JavaScript、图标资源
├── docs/                              # 完整文档（见文档导航章节）
│   ├── user-guide/
│   ├── admin-guide/
│   ├── developer-guide/
│   ├── api-reference/
│   ├── deployment/
│   └── changelog/
├── tests/                             # 单元测试与集成测试用例
│   ├── unit/                          # 针对 core 模块的独立测试
│   └── integration/                   # API 端到端测试与数据库事务测试
├── scripts/                           # 运维辅助脚本
│   ├── backup_db.sh                   # 数据库自动备份脚本
│   └── migrate_legacy.py              # 旧版本数据迁移工具
├── config/                            # 环境配置文件（开发/测试/生产）
│   ├── development.toml
│   ├── staging.toml
│   └── production.toml
├── docker/                            # Docker 构建文件与 compose 配置
│   ├── Dockerfile
│   └── docker-compose.yml
├── .github/                           # GitHub Actions CI/CD 工作流定义
│   └── workflows/
│       ├── test.yml                   # 每次 push 运行测试套件
│       └── deploy.yml                 # 主分支合并后自动构建镜像
├── manage.py                          # 命令行入口（initdb、import、export 等）
├── requirements.txt                   # Python 生产依赖列表
├── requirements-dev.txt               # 开发额外依赖（pytest、black、mypy）
├── README.md                          # 项目总览（即本文档）
└── LICENSE                            # MIT 许可证全文
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于报告缺陷、提交代码、完善文档或提供使用案例。请遵循以下步骤参与本项目。

1. 查阅贡献者行为准则。所有参与者必须遵守 `CODE_OF_CONDUCT.md` 中规定的友善沟通与协作原则，违规行为将被限制参与权限。

2. 从 GitHub 派生本仓库并创建特性分支。请使用 `feature/` 或 `fix/` 前缀命名分支，例如 `feature/support-excel-import`，并确保分支基于最新的 `main` 分支。

3. 编写或修改代码时，请同步更新对应的单元测试。所有新增功能必须包含正向与异常测试用例，修复缺陷需提供回归测试。运行 `pytest tests/` 确保全部测试通过且覆盖率不低于 85%。

4. 如果涉及用户界面或命令行接口的变更，必须更新 `docs/` 下的相应文档，并在 `changelog/` 中记录变更条目。文档风格请参考 `docs/contributing/style-guide.md`。

5. 提交拉取请求时，请在描述中清晰说明变更目的、实现方式以及测试验证结果。至少需要一位项目维护者审核通过后方可合并。合并后 CI 流水线会自动构建并部署到预发布环境。

## 常见问题

**问：HyperLink Hub 是否支持 PostgreSQL 作为生产数据库？**

答：当前版本默认使用 SQLite 以降低入门门槛，但项目从设计之初就基于 SQLAlchemy ORM，理论上支持 PostgreSQL、MySQL 等主流关系型数据库。您只需在 `config/production.toml` 中修改 `database_url` 配置项，并安装对应的数据库驱动（如 `psycopg2-binary`）即可。我们计划在 v2.0 版本中将 PostgreSQL 作为首选生产数据库并提供完整的迁移脚本。

**问：健康检查任务是否会因为外部网站响应慢而阻塞主服务？**

答：不会。健康检查任务运行在独立的异步工作进程池中，通过 Redis 队列进行任务分发。默认超时时间为 10 秒，超时后会标记为“不可达”并记录日志，主服务的 API 请求不受影响。您也可以在配置文件中调整超时时间、重试次数和并发检查数。

**问：如何将现有项目中的大量外链迁移到 HyperLink Hub？**

答：项目提供了 `import` 命令，支持从 JSON、CSV 和纯文本文件导入。对于 Markdown 格式的现有文档，我们推荐使用 `scripts/parse_markdown_links.py` 辅助脚本，它可以扫描指定目录下的所有 `.md` 文件，提取出所有 `[text](url)` 格式的链接，生成符合导入规范的 CSV 中间文件。该脚本的使用说明位于 `docs/user-guide/migration-guide.md`。

## 许可证

本项目采用 MIT 许可证。您可以自由使用、修改、分发本软件，包括用于商业目的，但需保留原始版权声明和免责声明。完整许可证文本请参阅项目根目录下的 `LICENSE` 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
