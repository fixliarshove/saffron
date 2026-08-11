# NexusIndex

NexusIndex 是一个面向技术社区与内容聚合场景的轻量化资源导航与外链管理工具。项目定位为技术团队、个人开发者与内容运营者提供可自托管的资源目录基础设施，用于系统化组织、展示与共享外部链接集合。NexusIndex 不依赖数据库，基于静态 Markdown 与元数据驱动，解决的是多源外链的归集、分类展示、版本追溯与快速检索问题，适用于内部知识库、开源项目推荐列表、行业信息门户等场景。

## 功能概览

- **多级分类索引**：支持无限层级的目录树结构，可自定义分类标题与排序权重，便于按主题、区域、语种或业务线组织链接。
- **原始链接完整保留**：所有收录的 URL 均以原始字符串形式存储与展示，自动识别裸域名、带协议或带 www 前缀的链接，不做任何主动改写或归一化处理。
- **元数据标注系统**：每条资源可附加标签、描述、维护状态与更新日期，支持按字段过滤与排序，方便快速筛选有效资源。
- **静态站点生成**：内置模板引擎，可将资源列表与目录树渲染为纯静态 HTML 页面，无需后端服务即可部署至任意 Web 服务器或对象存储。
- **版本化变更日志**：每次增删改操作均生成时间戳记录，配合 Git 可追溯完整变更历史，满足合规审计需求。
- **多格式导入导出**：支持 JSON、CSV 与 TOML 格式的批量导入导出，便于与其他系统（如 CMS、爬虫、数据中台）进行数据交换。
- **访问统计与死链检测**：提供轻量级定时任务，可配置周期检测链接可访问性，并生成可用性报告，辅助维护者及时清理失效资源。

## 应用场景

- **团队内部技术文档中心**：研发团队可将项目文档、监控面板、CI/CD 系统、代码仓库等内部链接统一收录于 NexusIndex，按团队或服务分类，替代浏览器书签的分散管理，提升协作效率。
- **开源项目推荐聚合站**：社区运营者可利用 NexusIndex 汇集某一领域（如机器学习、前端框架、区块链）的优质开源项目列表，为外部访问者提供一站式发现入口，同时通过元数据标注项目活跃度与许可证类型。
- **行业信息监控看板**：媒体编辑或行业分析师可将多个数据源、报告网站、新闻频道的外链归集为专题目录，配合定时死链检测功能，快速定位失效或变更的内容源，保障信息渠道的可靠性。
- **个人知识收藏夹**：开发者或研究人员可自建私有实例，按学习路径或研究课题组织长期积累的外链资源，避免依赖第三方书签服务的商业限制或数据丢失风险。

## 快速开始

以下操作基于 Linux/macOS 环境，Windows 用户可使用 WSL 或 Git Bash 执行。

```bash
# 1. 克隆代码仓库
git clone https://github.com/nexusindex/nexusindex.git
cd nexusindex

# 2. 安装依赖（使用 pip 虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 初始化配置并启动开发服务器
cp .env.example .env
python manage.py migrate
python manage.py runserver
```

访问 `http://127.0.0.1:8000` 即可进入管理面板，首次使用需创建管理员账号。生产环境部署请参考 `deploy/` 目录下的 Docker 与 Nginx 配置模板。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 ~ 3.11 | 核心运行环境，低于 3.9 不支持类型注解新语法，高于 3.11 可能存在第三方库兼容性风险 |
| pip | 22.0+ | 包管理工具，用于安装 requirements 中列出的全部依赖 |
| Git | 2.25+ | 版本控制，用于克隆仓库、管理变更日志以及后续更新合并 |
| SQLite | 3.35+ | 内置轻量数据库，用于存储元数据、标签与访问记录；生产环境可切换至 PostgreSQL |
| Redis | 6.2+ | 可选组件，用于缓存分类树与访问统计结果，若未配置则降级为内存缓存 |
| Node.js | 16.0+ | 仅前端构建时需要，用于编译静态资源，若使用预编译包则非必需 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/` | 如何添加链接、创建分类、导入导出数据、配置访问权限 |
| 运维指南 | `/docs/ops-guide/` | 如何部署至生产环境、配置 HTTPS、执行死链检测、备份与恢复数据 |
| 开发者文档 | `/docs/dev-guide/` | 如何扩展自定义元数据字段、编写插件、参与核心模块重构 |
| API 参考 | `/docs/api-reference/` | 所有 RESTful 接口的请求参数、响应格式与错误码说明，供外部系统集成 |

## 资源列表

### 主题类资源

<code>rihanrenqixilie.org.cn</code>

<code>renqixiliezhongwenzimu.org.cn</code>

### 视频类资源

<code>shibajinzaixianmianfeiguankan.org.cn</code>

<code>shunvtiantang.org.cn</code>

### 综合类资源

<code>yazhoupapa.org.cn</code>

<code>yeyejiujiu.org.cn</code>

<code>oumeizipaiqu.org.cn</code>

<code>wuyeneishe.org.cn</code>

<code>jiujiujiujiuguochan.org.cn</code>

<code>neishemama.org.cn</code>

## 项目结构

```
nexusindex/
├── manage.py                  # Django 管理入口，用于开发调试与命令行操作
├── requirements.txt           # Python 依赖列表，包含 Django、django-rest-framework、celery 等
├── .env.example               # 环境变量模板，包含 SECRET_KEY、DEBUG、数据库连接串等配置
├── deploy/                    # 生产部署脚本与配置
│   ├── docker-compose.yml     # 全栈编排（应用 + Redis + PostgreSQL + Nginx）
│   ├── nginx.conf             # 反向代理与静态文件缓存规则
│   └── gunicorn.conf.py       # Gunicorn 工作进程与超时参数
├── src/                       # 核心源代码目录
│   ├── core/                  # 基础抽象层：元数据模型、链接校验器、分类树算法
│   ├── api/                   # RESTful API 视图集，序列化器与路由注册
│   ├── web/                   # 面向最终用户的页面视图，含首页、分类列表、详情页
│   ├── tasks/                 # 异步任务：死链检测、统计聚合、邮件报告（基于 Celery）
│   └── utils/                 # 通用工具函数：URL 规范化（仅保留原始输入）、日期处理、日志封装
├── static/                    # 前端静态资源（CSS、JavaScript、图片），经 Webpack 打包
│   ├── css/                   # 基于 Bootstrap 5 定制的主样式表
│   ├── js/                    # 交互逻辑：搜索过滤、分类折叠、批量操作
│   └── fonts/                 # 图标字体与备选字体文件
├── templates/                 # Django 模板文件，用于服务端渲染 HTML
│   ├── base.html              # 全局布局模板，含导航栏与页脚
│   ├── index.html             # 首页目录树渲染模板
│   └── detail.html            # 单个资源详情与关联标签展示模板
├── docs/                      # 完整文档源文件（Markdown + MkDocs 配置）
│   ├── user-guide/            # 用户操作手册，配截图与常见流程
│   ├── ops-guide/             # 运维部署与监控指南
│   ├── dev-guide/             # 开发环境搭建与贡献规范
│   └── api-reference/         # API 端点详细说明，附带 curl 示例
├── tests/                     # 单元测试与集成测试（pytest + coverage）
│   ├── unit/                  # 模型、序列化器、工具函数的独立测试
│   └── integration/           # API 端到端测试与任务执行测试
└── scripts/                   # 运维辅助脚本
    ├── backup_db.sh           # 数据库定时备份脚本（配合 crontab）
    ├── import_csv.sh          # 从 CSV 文件批量导入外链
    └── health_check.py        # 系统健康状态探测，用于监控告警
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。建议使用 Python 3.10 虚拟环境隔离依赖，确保所有测试用例在本地通过后再提交。
2. 选择 `src/` 目录下的任一模块进行修改，或新增功能。若涉及数据模型变更，需同时编写迁移脚本并更新 `docs/dev-guide/` 中的相关说明。
3. 代码风格遵循 PEP 8，并使用 `black` 与 `isort` 进行自动格式化。所有公共函数与类必须包含 docstring，且参数与返回值需注明类型。
4. 提交前运行 `pytest tests/` 确保无回归错误，并补充新用例覆盖新增代码。若修复了已有问题，请在 Commit Message 中引用 Issue 编号。
5. 发起 Pull Request 至 `develop` 分支，描述变更目的、影响范围与测试结果。核心维护者将在 3 个工作日内进行 Review，必要时会要求补充修改或添加示例。

## 常见问题

**Q：项目是否支持同时管理上千个外链，并保证页面加载速度？**
A：支持。NexusIndex 默认采用分类懒加载与前端分页策略，分类树仅在展开时请求子节点数据，而非一次性全量渲染。同时，静态模式可预生成完整 HTML，配合 CDN 可承载数万级链接的访问，单页加载时间控制在 300ms 以内。

**Q：如何迁移已有的书签文件（如 Chrome 导出的 HTML 或 Firefox JSON）？**
A：目前未内置浏览器书签解析器，但可通过导入导出功能实现转换：将书签文件手动整理为 CSV 格式（列：标题、URL、分类、标签），然后使用 `scripts/import_csv.sh` 脚本批量导入。后续版本计划增加直接解析 Chrome/Firefox 导出格式的适配器。

**Q：死链检测任务会不会影响主站访问性能？**
A：不会。死链检测任务被设计为 Celery 异步队列，由独立的工作进程执行，并可配置执行时间窗口（例如凌晨低峰期）。检测结果会写入单独的状态表，前端展示时仅读取缓存，不会因检测超时阻塞页面响应。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:36
