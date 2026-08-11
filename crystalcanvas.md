# NexusFixture

NexusFixture 是一个面向数据集成工程师与自动化测试人员的技术资源聚合与外部数据源编排系统。该项目不提供任何原始数据或分析结论，而是作为结构化外链资源的中转枢纽，专注于收集、分类、校验和维护来自公开网络的高频变更数据源入口。其核心目标用户为需要快速定位实时赛事统计、比分变动历史、联赛排期等动态信息的技术自动化项目维护者，以及需要构建数据抓取管道、对比多源数据一致性的质量保障团队。NexusFixture 通过统一的外链资源清单与可插拔的访问器接口，解决数据源分散、域名频繁变动、访问协议不一致等实际问题，降低自动化数据采集链路的维护成本。

## 功能概览

- 外链资源清单管理：以机器可读的 YAML 格式维护全部数据源 URL，支持批量导入、去重校验与版本差异对比。
- 资源可用性探测：对清单内每个 URL 执行定时 HEAD/GET 请求，记录状态码、响应时间和内容长度，生成可用性历史趋势。
- 协议适配转换层：自动识别并标准化 URL 协议头，统一处理 http 与 https 混用场景，支持裸域名自动补全策略配置。
- 变更通知机制：当资源清单发生增删改或某个 URL 持续不可用时，通过 Webhook 或邮件输出结构化变更报告。
- 访问器代码生成：根据资源 URL 模板和返回内容特征，生成 Python 或 TypeScript 的简易数据访问函数骨架。
- 标签与全文检索：为每个外链资源标记业务领域、数据频率、地域属性，支持基于标签组合和 URL 片段的快速过滤。
- 快照对比工具：支持对同一 URL 在不同时间点的响应内容做差异对比，辅助检测数据格式或字段结构的变动。

## 应用场景

- 自动化数据管道维护：团队在维护每日定时拉取的赛事数据管道时，可将 NexusFixture 作为上游配置中心，当某一数据源域名变更或协议升级时，只需在清单中更新对应条目，下游解析任务自动读取最新入口，无需修改各微服务代码。
- 多源数据一致性校验：质量保障人员在进行跨平台比分数据对比时，通过 NexusFixture 同时获取多个不同域名的实时页面，利用内置的快照对比工具快速识别不同源之间的数值偏差或更新延迟，定位异常数据源。
- 爬虫规则快速验证：开发者在编写新的数据抓取脚本时，使用 NexusFixture 生成的访问器骨架和可用性探测结果，快速筛选当前响应最快的资源入口进行调试，避免因目标站点过载或屏蔽导致开发中断。
- 历史数据回溯分析：数据分析师需要追溯某场比赛在不同时间点公布的比分变化时，利用快照对比功能调取同一资源在不同批次的响应记录，构建时间序列变化轨迹，用于赛事规律研究或模型训练数据清洗。

## 快速开始

以下步骤演示如何从 GitHub 克隆仓库、安装依赖并启动本地管理控制台。

```bash
# 克隆项目仓库
git clone https://github.com/nexusfixture/core.git
cd nexusfixture-core

# 创建并激活 Python 虚拟环境
python3 -m venv venv
source venv/bin/activate  # Windows 系统请使用 venv\Scripts\activate

# 安装核心依赖与开发依赖
pip install -r requirements.txt
pip install -r requirements-dev.txt

# 初始化本地配置文件和资源清单
cp config/example.yaml config/local.yaml
cp resources/example-manifest.yaml resources/manifest.yaml

# 运行基础可用性探测任务
python cli.py probe --manifest resources/manifest.yaml --output reports/probe-result.json

# 启动本地 Web 管理界面（默认监听 8000 端口）
python cli.py serve --port 8000
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 及以上 | 核心运行时环境，用于执行探测、生成、调度等所有逻辑 |
| PyYAML | 6.0.1 | 解析资源清单和配置文件，支持 YAML 1.2 规范 |
| httpx | 0.27.0 | 异步 HTTP 客户端，用于并发探测和快照抓取 |
| pydantic | 2.5.0 | 数据模型校验，确保资源条目字段类型和格式正确 |
| uvicorn | 0.27.1 | ASGI 服务器，用于承载 Web 管理界面和 API 端点 |
| jinja2 | 3.1.2 | 模板引擎，渲染 Web 界面的资源列表和报告页面 |
| rich | 13.7.0 | 终端美化输出，用于命令行探测进度和结果展示 |
| pytest | 8.0.0 | 单元测试框架，用于验证访问器生成和协议适配逻辑 |
| pre-commit | 3.6.0 | Git 钩子管理，用于提交前自动执行代码格式化和静态检查 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/manifest-format.md | 资源清单的字段定义、标签规范、版本管理策略是什么？ |
| 用户手册 | docs/user-guide/probe-config.md | 如何调整探测超时、重试策略、并发数及告警阈值？ |
| 开发指南 | docs/developer/accessor-generator.md | 访问器代码生成的模板规则、自定义过滤器及扩展接口如何实现？ |
| 开发指南 | docs/developer/api-endpoints.md | 管理控制台提供的 RESTful API 列表、请求参数及返回结构是什么？ |
| 运维手册 | docs/ops/deployment-checklist.md | 生产环境部署所需的环境变量、反向代理配置及健康检查策略有哪些？ |
| 运维手册 | docs/ops/migration-steps.md | 从旧版本资源清单迁移至新版本时，需要执行哪些数据库或文件操作？ |
| 设计文档 | docs/design/architecture-overview.md | 系统整体模块划分、数据流向、扩展点及设计取舍决策是什么？ |
| 设计文档 | docs/design/url-normalization.md | URL 规范化策略的具体规则，包括协议补全、路径标准化与去重逻辑。 |

## 资源列表

### 足球赛事比分类

<code>zuqiubisaijieguo.net.cn</code>

<code>jingcaizuqiubifen1.net.cn</code>

<code>jingcaizuqiubifenwang.org.cn</code>

<code>jingcaizuqijishibifen.org.cn</code>

<code>zuqiubifenjingcai.org.cn</code>

<code>jingcaizuqibisaijieguo.org.cn</code>

<code>jingcaizuqibifensaicheng.org.cn</code>

### 综合比分与竞猜类

<code>wangyitiyujishibifen.net.cn</code>

<code>jingcaibifenwang.org.cn</code>

<code>jingcaibifen.net.cn</code>

## 项目结构

```
nexusfixture-core/
├── cli.py                         # 命令行入口，注册 probe/serve/generate 等子命令
├── requirements.txt               # 生产环境核心依赖锁定列表
├── requirements-dev.txt           # 开发与测试额外依赖
├── pyproject.toml                 # 项目元数据与构建配置（setuptools 后端）
├── .pre-commit-config.yaml        # pre-commit 钩子配置（black/isort/flake8）
├── config/
│   ├── example.yaml               # 示例配置文件，含探测超时、通知渠道等参数
│   └── schema.json                # 配置文件 JSON Schema，用于 IDE 校验
├── resources/
│   ├── example-manifest.yaml      # 示例资源清单，含 10 个初始外链条目
│   └── manifest.yaml              # 实际使用的资源清单（用户需自行创建）
├── src/
│   ├── core/                      # 核心业务逻辑模块
│   │   ├── __init__.py
│   │   ├── loader.py              # 加载与解析 YAML 清单，返回 Pydantic 模型列表
│   │   ├── normalizer.py          # URL 协议补全、去 www、路径标准化实现
│   │   ├── probe.py               # 异步并发探测，记录状态码、耗时、内容摘要
│   │   └── diff.py                # 两次快照的文本/结构化差异比对引擎
│   ├── generate/                  # 访问器代码生成模块
│   │   ├── __init__.py
│   │   ├── python_gen.py          # 生成 Python requests/httpx 访问函数
│   │   └── typescript_gen.py      # 生成 TypeScript fetch/axios 访问函数
│   └── web/                       # Web 管理界面模块
│       ├── app.py                 # FastAPI 应用实例，注册路由与异常处理器
│       ├── templates/             # Jinja2 模板目录
│       │   ├── index.html         # 资源总览页，含搜索与过滤表单
│       │   └── detail.html        # 单条资源详情，含历史探测曲线
│       └── static/                # CSS/JS 静态资源
├── tests/                         # 单元测试与集成测试目录
│   ├── test_loader.py             # 测试清单加载与格式校验
│   ├── test_normalizer.py         # 测试各种 URL 输入下的规范化输出
│   └── test_probe.py              # 模拟 httpx 响应，测试探测状态更新逻辑
├── docs/                          # 完整文档（见上文导航）
│   ├── user-guide/
│   ├── developer/
│   ├── ops/
│   └── design/
├── reports/                       # 探测报告与快照存储目录（运行时生成）
│   ├── probe-result.json          # 最近一次全量探测的汇总 JSON
│   └── snapshots/                 # 按 URL 哈希分组的响应快照存储目录
└── logs/                          # 应用日志存储目录
    ├── cli.log                    # 命令行操作日志
    └── web.log                    # Web 服务访问与错误日志
```

## 贡献指南

1. 阅读设计文档与开发指南：在提交任何代码或修改资源清单之前，请先浏览 docs/design/architecture-overview.md 了解整体架构，并查阅 docs/developer/ 目录下的相关模块说明，确保修改方向与项目设计理念一致。
2. 创建议题并获取反馈：对于新功能、性能优化或重大重构，请先在 GitHub Issues 中创建议题，简要描述问题背景、提议方案及预期影响，等待维护者或社区成员反馈后再开始具体实现。
3. 本地环境准备与测试：Fork 本仓库至个人账户，克隆后执行 pre-commit 安装（pre-commit install），确保所有提交通过 black、isort 和 flake8 检查。新增或修改功能需在 tests/ 目录下补充对应的单元测试用例，并保证 pytest 全部通过。
4. 提交 Pull Request：将本地分支推送至个人远程仓库，向主仓库的 main 分支发起 Pull Request，在描述中关联相关议题编号，列出变更摘要、测试覆盖情况及手动验证步骤。PR 需要至少一位维护者进行 Code Review，通过后由维护者合并。
5. 资源清单更新流程：若仅需增删或修改 resources/manifest.yaml 中的外链条目，无需编写代码，但需在 PR 描述中说明每项变动的理由（例如源站迁移、协议升级、域名过期等），并附上本次变更后的探测验证结果片段。

## 常见问题

Q: 资源清单中的 URL 可以包含查询参数或路径吗？例如 <code>example.com/v1/live?league=premier</code>。
A: 完全支持。NexusFixture 的 normalizer 模块仅对协议头和主域名部分做标准化处理，不会移除或修改查询参数与路径段。但需要注意，探测模块在发送请求时会原样使用完整 URL，因此如果参数中包含时间戳或 token 等动态值，可能会导致快照对比时产生预期内的差异，建议在配置中标记该条目为「动态参数」类型。

Q: 探测模块如何处理目标站点的反爬机制，例如 User-Agent 校验或 Cookie 会话？
A: 默认探测使用合理的 User-Agent（如 Mozilla/5.0 兼容字符串）并开启 follow_redirects。对于需要特定 Cookie 或 Header 的资源，可以在 resources/manifest.yaml 中为每个条目单独配置 headers 和 cookies 字段，探测模块会自动合并这些附加信息。若目标站点要求 JavaScript 渲染，则当前版本暂不支持，建议配合外部浏览器自动化工具使用，NexusFixture 仅负责入口管理。

Q: 如何迁移已有的手工维护 URL 列表至 NexusFixture 的资源清单格式？
A: 项目提供了辅助转换脚本 tools/import-legacy.py，支持从纯文本列表（每行一个 URL）或 CSV 文件（列：url, tags, description）批量导入。运行 python tools/import-legacy.py --input old-list.txt --output resources/manifest.yaml 即可完成初次转换，之后可手动编辑 YAML 文件补充更多字段（如频率、区域等）。如果导入格式有特殊需求，欢迎提交议题说明具体场景。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
