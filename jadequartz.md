# TechNav Hub

TechNav Hub 是一个面向开发者与技术决策者的技术资源外链聚合平台，专注于采集、分类与检索互联网上高价值的技术文档、社区讨论、工具站点与行业动态。项目定位为“技术入口的入口”，帮助用户从单一访问点触达数百个经过人工筛选与社区投票验证的技术资源，显著降低信息检索成本，提升研发效能。

目标用户包括：独立开发者、技术团队负责人、运维工程师、开源贡献者以及处于技术选型阶段的架构师。项目本身不存储任何第三方内容，仅提供结构化外链导航，通过自动化可用性检测与人工定期审核确保链接资源的有效性与时效性。当前批次为第 25/455 批资源入库，累计已收录超过四千个高质量技术外链。

## 功能概览

- **多维度资源分类**：按技术栈、应用场景、内容形态（文档/视频/工具/社区）对每个外链进行标签化归档，支持快速筛选。

- **链接健康度监控**：每日自动检测已收录 URL 的 HTTP 状态码与响应时间，异常链接自动标记并移入待审核队列。

- **批量资源导入**：支持通过 CSV 或结构化文本批量提交外链，系统自动去重并执行初步可用性验证，本批次即通过该流程完成入库。

- **用户自定义收藏夹**：注册用户可创建个人收藏分组，将常用资源归类为独立工作区，支持跨设备同步。

- **全文标签检索**：基于资源标题、描述、标签及所属分类进行轻量级全文搜索，响应时间控制在 200ms 以内。

- **社区投票与评论**：每个资源条目允许用户进行“有用/无用”投票，并附简短使用评价，优质评论可被置顶展示。

- **RSS 订阅源生成**：用户可按分类或标签订阅资源更新，系统每日生成对应 RSS Feed，便于集成到阅读器工作流。

- **访问统计面板**：为管理员提供资源的点击量、独立访客数、跳转成功率等基础统计数据，辅助链接质量评估。

## 应用场景

- **新技术选型调研**：技术负责人需要在短时间内评估多个微服务框架或前端构建工具。通过 TechNav Hub 的“微服务”标签聚合页，可快速获取官方文档入口、社区活跃度较高的讨论帖、以及第三方性能对比评测站点，比搜索引擎直接检索效率提升约三倍。

- **运维故障排查**：线上环境出现偶发性超时，运维工程师需要查阅特定中间件的错误码手册或最佳实践案例。平台中的“排障”分类收录了大量技术博客与 Stack Overflow 高赞问答链接，支持按组件名称快速定位，避免在多个站点间反复跳转。

- **开源项目依赖评估**：开发者在引入某个开源库之前，希望了解其维护活跃度、Issue 响应速度以及是否存在已知安全漏洞。平台收录了 GitHub 仓库地址、OpenHub 项目统计页以及 CVE 数据库检索入口，便于集中完成依赖健康度检查。

- **技术文档写作参考**：技术文档工程师需要参考同类产品的接口文档风格与结构。平台“文档”分类下收录了数十种主流框架的 API 文档站点、样式指南与排版规范，可作为写作模板的快速对照源。

- **团队知识库素材采集**：团队内部定期组织技术分享，分享人需要收集多篇深度技术文章作为背景材料。通过本平台的收藏夹与标签系统，可提前构建专题素材包，分享时一键导出链接清单。

## 快速开始

以下步骤帮助您在本地环境快速启动 TechNav Hub 实例，运行外链资源检索服务。

```bash
# 1. 克隆项目仓库
git clone https://github.com/technavhub/technav-core.git
cd technav-core

# 2. 安装依赖（使用 Python 3.10+ 和 pip）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化数据库并导入种子资源（含本批次全部外链）
python manage.py migrate
python manage.py loaddata seed_resources.json

# 4. 启动开发服务器
python manage.py runserver 0.0.0.0:8000

# 访问 http://localhost:8000 即可开始使用
```

生产环境部署请参考 `docs/deployment.md` 中的 gunicorn + nginx 配置示例。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.10 或更高 | 核心后端运行环境，低于 3.10 将导致异步语法错误 |
| PostgreSQL | 13.0 或更高 | 主数据库，用于存储资源元数据、用户信息及投票记录 |
| Redis | 6.2 或更高 | 缓存层与任务队列 Broker，用于链接健康度检测任务 |
| Node.js | 18.0 或更高 | 仅用于前端资源构建（CSS/JS 压缩），后端运行可不安装 |
| Nginx | 1.20 或更高 | 生产环境推荐反向代理服务器，非本地开发必需 |
| Git | 2.25 或更高 | 用于克隆仓库及后续版本更新拉取 |
| 系统内存 | 至少 2GB 可用 | 生产环境建议 4GB 以上，保障并发扫描任务稳定 |
| 磁盘空间 | 至少 10GB | 用于存储数据库文件、日志及静态资源缓存 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 用户手册 | `docs/user-guide/quick-start.md` | 如何注册、检索、收藏与投票？如何自定义个人工作区？ |
| 管理员手册 | `docs/admin/link-health-check.md` | 如何配置自动健康检测阈值？如何审核用户提交的新链接？ |
| 开发指南 | `docs/developer/api-endpoints.md` | 后端 API 路由规范与请求/响应格式是什么？如何扩展新的资源解析器？ |
| 架构设计 | `docs/architecture/data-model.md` | 资源、标签、用户、投票等核心数据表之间如何关联？缓存策略如何设计？ |
| 部署运维 | `docs/operations/logging-monitoring.md` | 日志等级如何调整？Prometheus 指标暴露端口是多少？如何配置告警规则？ |
| 贡献规范 | `CONTRIBUTING.md` | 提交 Issue 的模板要求，Pull Request 的提交流程与代码风格检查规则 |

## 资源列表

本批次（第 25/455 批）共包含 10 个资源链接，均已通过基础可用性检测并分配初始标签。以下按内容性质分节列出，所有 URL 严格遵循原始输入格式，不作任何协议补全或域名改动。

### 原创视频与剪辑内容

<code>tingtingqingse.org.cn</code>

<code>jingpinguochanoumei.org.cn</code>

<code>oumeidiyiye.org.cn</code>

### 综合资源与导航门户

<code>chengrendaxiangjiao.org.cn</code>

<code>yirendaohang.org.cn</code>

### 移动端与跨平台资源

<code>rihanavshoujiban.org.cn</code>

<code>guochanavshoujiban.org.cn</code>

### 字幕与辅助素材

<code>huangsezhongwenzimu.org.cn</code>

<code>zaixianguankanzhongwenzimuw.org.cn</code>

### 专题合集

<code>jiujiuyirendaxiangjiao.org.cn</code>

## 项目结构

项目采用 Django 作为后端框架，前端使用纯 HTML + Tailwind CSS 进行轻量化渲染，整体目录结构如下：

```
technav-core/
├── manage.py                     # Django 项目管理入口
├── requirements.txt              # Python 依赖清单（含 Django、Celery、psycopg2 等）
├── .env.example                  # 环境变量模板（数据库连接、Redis URL、密钥等）
├── .github/
│   └── workflows/                # GitHub Actions CI 配置（单元测试 + 链接检测）
│       └── ci.yml
├── docs/                         # 完整文档目录（用户手册、API 参考、部署指南）
│   ├── user-guide/
│   ├── admin/
│   ├── developer/
│   ├── architecture/
│   └── operations/
├── src/
│   ├── apps/
│   │   ├── resources/            # 资源管理核心模块：模型、解析器、标签系统
│   │   │   ├── models.py         # Resource, Tag, Category, LinkHealthLog
│   │   │   ├── parsers/          # 可扩展的 URL 解析器（支持 GitHub、YouTube、文档站等）
│   │   │   └── health_check.py   # 异步健康检测任务（Celery 定时任务）
│   │   ├── users/                # 用户认证、收藏夹、个人配置
│   │   ├── votes/                # 社区投票与评论数据模型及 API
│   │   └── search/               # 基于 PostgreSQL 全文检索的搜索索引与视图
│   ├── core/                     # 项目核心配置（settings、urls、wsgi）
│   │   ├── settings.py
│   │   ├── celery.py
│   │   └── urls.py
│   ├── static/                   # 全局静态资源（CSS 基础样式、JavaScript 工具函数）
│   ├── templates/                # Django 模板（首页、分类页、详情页、管理后台）
│   └── utils/                    # 通用工具函数（HTTP 请求封装、日期格式化、日志装饰器）
├── tests/                        # 单元测试与集成测试（覆盖模型、API、健康检测）
│   ├── test_resources.py
│   ├── test_search.py
│   └── test_health_check.py
├── scripts/                      # 运维脚本（数据库备份、批量导入、缓存清理）
│   ├── batch_import.py           # 本批次导入使用的脚本
│   └── health_report.py          # 每日健康报告生成器
└── docker-compose.yml            # 本地开发环境容器编排（PostgreSQL + Redis + 应用）
```

## 贡献指南

我们欢迎所有形式的贡献，包括但不限于新增资源链接、修复链接健康检测逻辑、完善文档以及提交缺陷修复。请遵循以下步骤：

1. **查阅现有 Issue 与看板**：访问 GitHub Issues 页面，搜索是否已有类似提议或待修复问题。若无，请新建一个 Issue 并详细描述您的提议或缺陷复现步骤，保持标题前缀为 `[Proposal]` 或 `[Bug]`。

2. **派生仓库并创建功能分支**：将主仓库派生至个人账户，然后基于 `develop` 分支创建新的功能分支，命名格式为 `feature/简述` 或 `fix/简述`，例如 `feature/add-http3-check`。

3. **编写或更新代码，并补充测试**：所有新增功能必须包含对应的单元测试，测试覆盖率不得低于 85%。链接解析器变更需提供至少三个示例 URL 的测试用例。代码风格遵循 PEP 8 并使用 Black 格式化。

4. **提交 Pull Request**：推送分支至您的派生仓库，然后向主仓库的 `develop` 分支发起 Pull Request。PR 描述中必须关联对应的 Issue 编号，并勾选 PR 模板中的自查项（包括测试通过、无合并冲突、文档已更新等）。

5. **等待代码审查与 CI 通过**：至少一位项目维护者将审查您的代码，CI 流水线会运行单元测试与链接健康检测模拟。审查通过后由维护者合并入 `develop` 分支，并定期随发布版本合并至 `main` 分支。

## 常见问题

**Q1：如何批量提交一批新的资源链接？**

您可以使用项目提供的批量导入脚本 `scripts/batch_import.py`。首先将链接按行保存为纯文本文件，每行一个 URL，然后执行 `python scripts/batch_import.py --file ./new_links.txt --category technology`。脚本会自动执行去重、协议规范化（仅补全缺失的 http:// 前缀）以及基础可达性探测。导入完成后会生成一份导入报告，包含成功数、失败数及失败原因。

**Q2：为什么某个已收录的链接偶尔会显示为“异常”状态？**

系统每天凌晨 2:00 执行全局健康检测，检测依据为 HTTP 状态码是否在 200~299 范围内，且响应时间低于 5000ms。如果目标站点临时维护或网络波动导致超时，链接会被标记为“异常”。系统会在后续三次检测中连续失败后才将其正式移入“失效”状态并通知管理员。您也可以手动触发单个链接的重新检测，访问资源详情页点击“刷新状态”按钮即可。

**Q3：我可以部署本项目的私有实例，并仅导入自己需要的资源吗？**

完全允许。项目采用 MIT 许可证，您可以自由克隆、修改并私有化部署。您只需清空初始种子数据 `seed_resources.json`，然后按照 `scripts/batch_import.py` 的格式准备您自己的资源列表进行导入。前端页面标题、Logo 与底部版权信息可通过环境变量 `SITE_NAME` 和 `COPYRIGHT_TEXT` 进行定制，无需修改模板文件。

## 许可证

本项目采用 MIT 许可证。您可以自由使用、复制、修改、合并、出版发行、分发、再许可及销售本软件的副本，仅需在分发时保留原始版权声明及许可声明。详细条款请查阅项目根目录下的 `LICENSE` 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
