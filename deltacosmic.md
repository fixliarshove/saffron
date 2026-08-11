# HyperLink Navigator

HyperLink Navigator 是一个面向技术社区与内容创作者的轻量级外链资源聚合与导航系统。项目定位于为开发者、运维工程师、技术写作者以及信息分析人员提供一套结构清晰、可私有化部署的技术资源目录管理工具。其核心目标是解决信息分散、链接失效、检索效率低下等问题，通过分类索引与状态监控机制，帮助用户高效组织和复用网络上的公开技术资料与实时数据源。

本项目并非传统意义上的爬虫或采集器，而是一个强调人工策展与机器辅助验证的链接治理平台。用户可通过简洁的 Web 界面或 API 接口，录入、分类、标注和检测外部链接的可访问性，并生成多种格式的导航页面或数据快照。项目特别适用于需要定期追踪多个技术博客、开源项目镜像、数据统计面板或动态赛事信息流的团队或个人。

## 功能概览

- **多级分类目录管理**：支持无限层级的自定义分类树，允许用户为每个链接指定所属领域、标签、优先级及生效时间范围，便于按主题或项目周期组织资源。

- **链接健康状态检测**：内置异步任务队列，可定时发起 HTTP/HTTPS 请求检测链接的有效性与响应耗时，自动标记异常链接并生成告警日志，减少人工维护成本。

- **全文检索与快速筛选**：基于内存索引提供对链接标题、描述、标签及目标页面摘要内容的快速检索，支持按状态、分类、创建时间等多维度组合筛选。

- **数据导入导出标准格式**：支持 CSV、JSON 及 Markdown 表格格式的批量导入与导出，方便与其他工具链（如 Excel、Obsidian、Notion）进行数据交换。

- **只读快照发布模式**：允许将当前链接列表生成静态 HTML 或纯 Markdown 目录页面，便于嵌入技术文档站点或作为项目附属资源对外发布。

- **用户权限与操作审计**：提供基础的多用户角色划分（管理员、编辑者、访客），记录所有增删改操作日志，满足团队协作与合规追溯需求。

- **自定义元数据扩展**：允许用户为每个链接附加键值对形式的自定义字段，例如“数据更新频率”“关联工单编号”“备用镜像地址”等，提升资源描述的灵活性。

## 应用场景

- **技术文档站点的外链管理**：当技术博客或开源项目文档中包含大量外部参考链接时，可使用 HyperLink Navigator 集中维护这些链接，利用健康检测功能定期检查链接有效性，避免文档中出现死链影响读者体验。

- **实时数据仪表盘的源地址聚合**：运维或数据分析团队需要同时监控多个外部数据接口或统计面板（例如体育赛事比分、汇率变动、天气信息等），通过本系统统一登记这些源地址，并利用状态检测快速发现接口异常。

- **行业信息周报的素材库维护**：内容编辑人员每周需要从数十个固定来源摘录新闻或数据，利用本系统的分类与检索功能，可快速筛选出本周新增或更新的链接，配合导出功能生成周报附录中的参考列表。

- **开源社区的资源共建共享**：技术社区可部署本系统作为公共资源导航页，允许社区成员提交新链接，经审核后上线，形成持续更新的社区知识库，降低新人查找资料的入门门槛。

## 快速开始

以下步骤适用于在 Linux/macOS 或 Windows WSL 环境中从源码启动项目。

```bash
# 1. 克隆项目仓库
git clone https://github.com/hyperlink-navigator/hln-core.git
cd hln-core

# 2. 安装依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 初始化本地数据库并启动内置服务
python manage.py migrate
python manage.py init_categories
python manage.py runserver --host 0.0.0.0 --port 8080
```

访问 http://localhost:8080 即可进入导航面板首页。默认管理员账号为 `admin`，初始密码在首次启动时由控制台输出。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 或更高 | 核心运行环境，推荐使用 3.10 以上版本以获得更好的性能与类型提示支持 |
| SQLite | 系统内置 | 默认嵌入式数据库，适合单机或小规模部署；生产环境可切换至 PostgreSQL |
| Redis | 可选 (>=6.0) | 用于缓存链接状态检测结果和异步任务队列，若未安装则使用内存缓存替代 |
| Node.js | 可选 (>=16) | 仅当需要构建前端静态资源时必需，纯后端运行无需安装 |
| Git | 任意版本 | 用于版本控制及后续拉取更新，初次克隆必须 |
| 系统时区数据 | 任意 | 用于任务调度与日志时间戳，建议设置为 Asia/Shanghai 或 UTC |

## 文档导航

| 层面 | 目录/章节 | 回答的问题 |
|------|----------|----------|
| 基础使用 | `docs/quick-start.md` | 如何快速录入第一个链接、创建分类、生成导航页面？ |
| 配置说明 | `docs/configuration.md` | 环境变量、检测超时参数、邮件告警设置等如何修改？ |
| API 参考 | `docs/api/v1/endpoints.md` | 如何通过 API 批量导入链接、获取状态报告、触发检测任务？ |
| 运维指南 | `docs/operations/health-check.md` | 如何调整健康检测的频率、并发数及异常通知策略？ |

## 资源列表

以下链接为本项目批次收录的外部资源索引，按类别分组展示。所有链接均保持用户原始格式原样输出。

技术数据与赛事信息类

- <code>qiutanjishibifenmobile.asia</code>
- <code>jinrizuqiubifenyucetuijian.asia</code>
- <code>aodaliyazuqiuchaojiliansaizhugongbang.top</code>
- <code>aodaliyazuqiuchaojiliansaizhibo.top</code>
- <code>aodaliyazuqiuchaojiliansaisheshoubang.top</code>
- <code>aodaliyazuqiuchaojiliansaiqianzhan.top</code>
- <code>aodaliyazuqiuchaojiliansaijishibifen.top</code>
- <code>aochaozhugongbang.asia</code>
- <code>500shoujibanbifen.asia</code>
- <code>dszuqiushengpingfu.cn</code>

## 项目结构

```
hln-core/
├── src/
│   ├── core/                       # 核心业务逻辑模块
│   │   ├── link_manager.py         # 链接增删改查与分类关联逻辑
│   │   ├── health_checker.py       # 异步健康检测调度器与结果处理器
│   │   └── index_builder.py        # 内存倒排索引构建与检索实现
│   ├── api/                        # RESTful API 路由与请求处理
│   │   ├── v1/
│   │   │   ├── links.py            # 链接资源端点 (CRUD)
│   │   │   └── categories.py       # 分类管理端点
│   ├── models/                     # 数据模型定义（SQLAlchemy/Peewee）
│   │   ├── link.py                 # 链接实体模型，包含 url、标题、状态字段
│   │   └── category.py             # 分类树模型，支持 parent_id 自关联
│   ├── utils/                      # 通用工具函数
│   │   ├── network.py              # HTTP 请求封装、超时与重试策略
│   │   └── export.py               # 导出为 CSV/JSON/Markdown 的转换器
├── tests/                          # 单元测试与集成测试用例
│   ├── test_link_manager.py
│   └── test_health_checker.py
├── scripts/                        # 运维辅助脚本
│   ├── init_db.py                  # 数据库初始化与种子数据填充
│   └── daily_check.py              # 可被 crontab 调用的每日检测任务入口
├── docs/                           # 完整项目文档（Markdown 格式）
│   ├── quick-start.md
│   ├── configuration.md
│   └── api/
├── requirements.txt                # Python 依赖清单
└── README.md                       # 本文件
```

## 贡献指南

1.  **问题反馈与讨论**：请先查阅现有 Issues 列表，确认无人报告相同问题后，提交新 Issue 并详细描述复现步骤、预期行为与实际结果，附带必要的日志片段或截图。

2.  **分支开发流程**：Fork 主仓库后，从 `main` 分支切出以 `feature/` 或 `fix/` 为前缀的命名分支进行开发。提交前请运行全量单元测试，确保无回归错误。

3.  **代码风格与文档**：Python 代码遵循 PEP 8 规范，提交前建议使用 `black` 与 `isort` 格式化。任何新增的公开函数或配置项必须在对应的 `.md` 文档中更新说明。

4.  **Pull Request 提交**：提交 PR 时请填写标准模板，清晰描述变更动机、实现方案及测试覆盖情况。至少需要一位项目维护者批准后合并。

5.  **安全漏洞报告**：如发现潜在安全风险（例如任意文件读取、注入漏洞），请直接发送邮件至项目维护者邮箱，勿公开披露，以便在补丁发布后再行公告。

## 常见问题

**Q1: 健康检测任务是否会影响页面浏览速度？**

检测任务默认在后台异步执行，使用独立的线程池或 Redis 队列。前端请求不阻塞等待检测结果。若需调整检测频率，可在 `config.yaml` 中修改 `check_interval_minutes` 参数。生产环境建议将检测任务单独剥离为定时脚本执行。

**Q2: 项目是否支持 Windows 系统原生运行？**

支持 Windows 10/11 下的 WSL2 环境。原生 CMD 或 PowerShell 下运行需手动安装 `waitress` 或 `gunicorn` 的替代适配，且部分路径处理逻辑可能不兼容。官方推荐使用 Docker 部署或在 Linux 环境运行。

**Q3: 如何迁移已有的书签或收藏夹数据？**

项目根目录下提供了 `scripts/import_browser_bookmarks.py` 脚本，可解析 Chrome/Firefox 导出的 HTML 书签文件，自动提取标题与 URL 并映射到默认分类。若需从 CSV 导入，可直接使用管理界面中的“批量导入”功能，或调用 `POST /api/v1/links/batch` 接口。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:35
