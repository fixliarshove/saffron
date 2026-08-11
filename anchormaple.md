# ResourceLink Navigator

ResourceLink Navigator 是一个面向开发者、技术研究人员与内容聚合者的轻量级外链资源导航与元数据管理工具。该项目定位于解决多源、多类型外部链接在项目文档、研究笔记或技术归档场景下的结构化引用与可维护性问题，帮助用户从“裸链接堆砌”转向“可检索、可追溯、可协作”的资源管理方式。

目标用户包括开源文档维护者、技术博主、数据分析师以及需要定期整理大量外链资源的运维或研发团队。ResourceLink Navigator 不提供爬虫、代理或内容缓存功能，而是强调链接的元数据标注、批次管理、状态标记与导出能力，从而在不侵入目标站点的情况下，构建持久化的资源引用基线。

## 功能概览

- **链接批次管理**：支持按批次编号（如 328/455）组织链接集合，记录批次导入时间、来源描述与标签，便于后续追溯与版本对比。
- **域名与协议智能解析**：自动提取链接中的协议类型（http/https）、子域名层级、根域及路径深度，并生成标准化存储键值，减少人工整理误差。
- **元数据扩展字段**：每条链接可附加自定义键值对，包括但不限于用途分类、优先级、状态（有效/失效/待审核）、关联项目编号等，满足企业级文档规范。
- **标记过滤与检索**：提供基于标签、批次号、域名后缀（如 .org.cn）的多维度筛选接口，支持正则表达式匹配路径关键字，便于快速定位特定类型资源。
- **只读导出与快照生成**：支持将当前链接库导出为只读 Markdown 列表、JSON 结构或静态 HTML 目录页，便于嵌入现有文档站点或交付给第三方审计。
- **链接健康检查（手动触发）**：通过 HTTP HEAD 请求验证链接可达性，并记录响应状态码与响应时间，辅助判断资源是否依然有效（不自动重试或缓存内容）。
- **历史变更日志**：记录每条链接的增删改操作，包括操作时间、操作者（本地用户）及变更摘要，满足内部合规与协作审计需求。

## 应用场景

- **开源项目文档外链整理**：当项目 README 或 Wiki 中需要引用大量第三方资源（如规范文档、参考实现、数据源）时，使用 ResourceLink Navigator 统一管理这些链接，避免在多个文件中散落重复或过时的 URL，同时通过元数据标注区分推荐链接与备用链接。
- **技术调研与竞品分析归档**：技术团队在开展竞品分析或新技术选型时，通常需要收集数十至上百个相关站点。利用批次管理功能将同一调研周期的链接归为一个批次，并添加优先级、关注领域等标签，后续可快速生成调研报告附件或对比表格。
- **内容运营与 SEO 外链台账**：内容运营人员需要记录已发布文章中的外链来源，用于跟踪外链权重变化或合作方资源更新。ResourceLink Navigator 的元数据扩展字段可存储合作方联系人、合作日期、备注信息，便于运营维护长期合作关系。
- **数据管道依赖记录**：在数据采集或 ETL 任务中，常依赖若干公开数据源接口。使用本工具记录这些接口地址、频率限制说明及备用地址，当源站变更时可快速定位所有受影响任务，提高故障响应效率。

## 快速开始

以下操作以 Linux/macOS 环境为例，假设已安装 Git 及 Python 3.9+。

```bash
# 克隆项目仓库
git clone https://github.com/your-org/resource-link-navigator.git

# 进入项目目录
cd resource-link-navigator

# 安装依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# 初始化本地数据库（SQLite）
python scripts/init_db.py

# 导入示例批次链接（包含本批次 328/455）
python scripts/import_batch.py --batch 328/455 --file samples/links_328_455.txt

# 启动本地 Web 界面（可选，默认监听 127.0.0.1:5000）
python app.py
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 - 3.12 | 核心运行环境，低于 3.9 不支持类型注解语法 |
| SQLite | 3.31+ | 内嵌数据库，用于存储链接元数据及日志，无需额外安装 |
| Flask | 2.2.0 - 2.3.x | Web 界面框架（可选），若仅使用 CLI 模式可不安装 |
| requests | 2.28.0+ | 用于健康检查的 HTTP 客户端，支持连接超时与重试策略 |
| pytest | 7.2.0+ | 单元测试框架（仅开发模式需要） |
| black | 22.3.0+ | 代码格式化工具（仅开发模式需要） |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|----------|----------|
| 用户手册 | docs/user-guide.md | 如何导入新批次、添加自定义字段、过滤链接及导出报告？ |
| 管理指南 | docs/admin-guide.md | 如何配置健康检查超时参数、清理历史日志、备份数据库？ |
| 开发者文档 | docs/developer-guide.md | 核心数据模型设计、扩展元数据方案、API 路由说明及单元测试编写规范。 |
| 命令参考 | docs/cli-reference.md | 所有 CLI 命令的完整参数列表、使用示例及退出码含义。 |
| 常见工作流 | docs/workflows.md | 典型使用场景（如调研归档、文档发布前检查）的分步操作指引。 |

## 资源列表

本批次（第 328/455 批）共包含 10 个外部资源链接，按用途分类如下：

### 中文拼音与字母资源类

<code>zhongwenzimudibaye.org.cn</code>

<code>nvyouzhongwenzimu.org.cn</code>

<code>zhongwenzimurenqishunv.org.cn</code>

<code>siwarenqizhongwenzimu.org.cn</code>

### 日韩欧美综合内容类

<code>rihanoumeisetu.org.cn</code>

<code>oumeilingleishipin.org.cn</code>

<code>guochanoumeirihanyiqu.org.cn</code>

### 特定站点与品牌类

<code>ludashiguanfangwangzhan.org.cn</code>

<code>ribenshunvshipin.org.cn</code>

<code>mitaojiujiujiu.org.cn</code>

## 项目结构

```
resource-link-navigator/
├── app/                            # Web 界面模块（可选）
│   ├── __init__.py                # Flask 应用工厂
│   ├── routes/                    # 路由蓝本
│   │   ├── index.py               # 首页及总览统计
│   │   ├── batch.py               # 批次管理页面
│   │   └── health.py              # 健康检查结果展示
│   └── templates/                 # Jinja2 模板文件
├── core/                          # 核心业务逻辑
│   ├── models.py                  # SQLAlchemy 数据模型（Batch, Link, Log）
│   ├── parser.py                  # URL 解析、域名拆分与协议规范化
│   ├── health.py                  # 健康检查执行器（并发控制）
│   └── exporter.py                # Markdown / JSON / HTML 导出器
├── scripts/                       # 命令行工具与运维脚本
│   ├── init_db.py                 # 初始化数据库表结构
│   ├── import_batch.py            # 从文本文件导入批次链接
│   ├── export_snapshot.py         # 导出当前全量链接为快照文件
│   └── clean_logs.py              # 清理 90 天前的历史日志
├── tests/                         # 单元测试与集成测试
│   ├── test_parser.py             # URL 解析函数测试
│   ├── test_health.py             # 健康检查模拟测试
│   └── test_exporter.py           # 导出格式正确性测试
├── samples/                       # 示例数据文件
│   └── links_328_455.txt          # 第 328/455 批次链接样例
├── docs/                          # 完整文档（见文档导航）
├── requirements.txt               # 生产环境依赖清单
├── requirements-dev.txt           # 开发环境额外依赖
├── .flake8                        # 代码风格检查配置
├── pyproject.toml                 # 项目元数据与构建配置
└── README.md                      # 本文件
```

## 贡献指南

1. 在 GitHub Issues 中查找或创建与您改动相关的问题，并等待维护者确认。避免直接提交未讨论过的较大功能变更。
2. Fork 本仓库，在您的分支上基于 main 分支进行开发。建议分支命名格式为 `feature/<简述>` 或 `fix/<问题编号>`。
3. 编写代码时请遵循项目内 `.flake8` 和 `pyproject.toml` 中定义的代码风格（Python 使用 Black 格式化，行宽 100 字符）。所有新增功能必须包含对应的单元测试，测试覆盖率不低于 85%。
4. 提交前运行 `pytest tests/` 确保所有测试通过，并执行 `python scripts/clean_logs.py --dry-run` 验证日志清理逻辑不受影响。
5. 发起 Pull Request，并在描述中关联相关 Issue，说明改动点、测试结果及对现有功能的影响。PR 需要至少一位维护者审阅通过后方可合并。

## 常见问题

**问：导入链接时提示“协议缺失”，是否必须手动补全？**

答：是的。ResourceLink Navigator 要求每条链接必须包含协议前缀（http:// 或 https://），以保证解析和健康检查的准确性。您可以在导入前使用文本编辑器批量替换，或使用 `scripts/preprocess_urls.py` 辅助脚本尝试自动补全（但该脚本无法区分裸域名与路径，建议人工确认）。

**问：健康检查显示某链接为“失效”，但实际上浏览器可以访问，是什么原因？**

答：健康检查默认使用 HTTP HEAD 方法且超时时间为 5 秒，部分站点可能屏蔽 HEAD 请求或响应较慢。您可以通过 CLI 参数 `--method GET` 改为 GET 请求，并适当增加 `--timeout` 值。另外，某些站点依赖 Cookie 或 JavaScript 渲染，此类站点无法通过简单的 HTTP 请求验证有效性，请在元数据中标记为“需人工确认”。

**问：如何迁移数据库到另一台机器？**

答：SQLite 数据库文件默认为 `data/links.db`，直接复制该文件到新机器相同相对路径即可。如需迁移到 MySQL 或 PostgreSQL，请参考 `docs/admin-guide.md` 中的外部数据库配置说明，并使用 `scripts/migrate_db.py` 工具完成数据转移。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:31
