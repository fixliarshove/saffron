# Rihan Resource Hub

Rihan Resource Hub is a community-driven technical documentation and resource aggregation project designed for developers, researchers, and system administrators who require rapid access to high-quality external references, dataset indices, and specialized topic catalogues. The project does not host any proprietary content but instead serves as a curated navigation layer that organizes publicly available technical materials, historical archives, and category-specific link collections into a structured, machine-readable format.

The primary audience includes open-source maintainers building documentation pipelines, data engineers who need reproducible source lists for web scraping or validation workflows, and technical writers who manage large reference catalogs. By providing a unified entry point with version-controlled metadata, Rihan Resource Hub reduces the overhead of manual link discovery and offers a transparent audit trail for all included external resources. This approach ensures that users can trust the integrity and longevity of the reference base, while contributors can easily propose additions or updates through standard pull request workflows.

## 功能概览

- **结构化资源索引** – 按照项目批次、类别和域名后缀自动生成分类目录，支持快速过滤和排序。

- **外部链接健康检查** – 每日定时验证收录的 URL 可达性，自动标记失效链接并生成报告。

- **元数据注解系统** – 每个资源条目可附加标签、描述、更新日期和关联议题编号，便于上下文理解。

- **只读镜像缓存** – 对高频访问的静态文档页面提供本地只读缓存，提升内网部署环境下的加载速度。

- **版本化变更日志** – 所有增删改操作均记录在 CHANGELOG 中，支持按批次号回滚或对比差异。

- **批量导入导出** – 支持 CSV 和 JSON 格式的批量资源清单导入导出，兼容主流数据管理工具。

- **RESTful API 查询接口** – 提供基于 HTTP 的查询端点，允许第三方系统按标签、域名或批次号检索资源。

## 应用场景

- **离线文档站点的外部引用管理** – 当构建企业级离线文档中心时，需要统一管理所有外部超链接。Rihan Resource Hub 的定期可达性检查能提前预警失效链接，避免用户访问到错误页面，同时元数据注解帮助文档维护者快速定位每个链接的用途和验证状态。

- **学术研究中的数据集溯源** – 研究人员在整理实验数据或撰写综述时，需要引用大量网络来源。利用本项目的结构化索引和版本化日志，可以精确记录每个引用来源的添加时间和批次，确保研究可复现性，同时满足出版机构对引用材料的可追溯性要求。

- **自动化运维脚本的依赖资源列表** – 运维工程师编写的部署或监控脚本往往依赖外部下载地址或 API 端点。通过将这类 URL 纳入资源中心统一管理，脚本可以直接查询 API 获取最新可用地址，当外部资源变更时只需更新索引而不必修改每一份脚本代码。

- **技术社区的内容聚合与导航** – 社区版主或技术博主可以使用本项目维护推荐阅读列表、工具合集或案例库。分类功能和标签系统使得不同主题的资源能够清晰划分，新成员可以按图索骥快速找到入门材料，而无需在大量历史帖子中手动翻找。

## 快速开始

以下指令适用于 Linux 及 macOS 环境，Windows 用户建议通过 WSL2 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/rihan-resource/rihan-hub.git
cd rihan-hub

# 安装依赖（需要 Python 3.9+ 和 pip）
pip install -r requirements.txt

# 初始化本地数据库并导入第 145/455 批资源
python manage.py initdb
python manage.py import-batch --batch 145 --file ./data/batch_145.csv

# 启动开发服务器
python manage.py runserver --port 8080
```

访问 `http://localhost:8080` 即可浏览资源列表。若需要执行健康检查，请运行：

```bash
python manage.py health-check --batch 145 --timeout 5
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 至 3.11 | 核心运行时，用于 API 服务、迁移脚本和健康检查任务 |
| SQLite | 3.31 及以上 | 默认本地数据库，存储资源元数据和变更日志，无需额外配置 |
| pip | 21.0 及以上 | Python 包管理工具，用于安装 requirements.txt 中列出的依赖库 |
| Git | 2.25 及以上 | 版本控制工具，用于克隆仓库、提交贡献以及同步上游更新 |
| curl | 7.68 及以上 | 健康检查模块依赖的命令行 HTTP 客户端，用于发送验证请求 |
| make | 3.81 及以上 | 可选，但推荐用于自动化执行常见命令（如迁移、测试、格式化） |
| 网络连接 | 出站 80/443 端口开放 | 仅在执行健康检查或缓存刷新时需要访问外部 URL，本地浏览无需网络 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 用户手册 | `docs/user-guide/` | 如何浏览资源列表、如何查看资源详情、如何使用搜索和过滤功能、如何导出特定批次的数据 |
| 贡献者指南 | `docs/contributing/` | 如何新增资源链接、如何更新元数据、提交 PR 的格式要求、批处理脚本的使用方法 |
| 运维手册 | `docs/operations/` | 如何部署到生产环境、如何配置定时健康检查、如何迁移数据库、如何调整缓存策略 |
| API 参考 | `docs/api/` | RESTful 端点列表、请求参数说明、返回数据结构、错误码含义、速率限制规则 |
| 设计文档 | `docs/design/` | 项目整体架构设计、数据模型 ER 图、批次管理逻辑、健康检查调度原理 |

## 资源列表

本批次（第 145/455 批）收录的原始资源链接如下，按域名类别分组展示。所有链接均保留用户提供的原始格式，未做任何协议补全或域名规范化处理。

### 系列主题资源

<code>rihanrenqixilie.org.cn</code>

<code>renqixiliezhongwenzimu.org.cn</code>

### 影视及娱乐相关

<code>shibajinzaixianmianfeiguankan.org.cn</code>

<code>shunvtiantang.org.cn</code>

<code>yazhoupapa.org.cn</code>

### 内容分类资源

<code>yeyejiujiu.org.cn</code>

<code>oumeizipaiqu.org.cn</code>

<code>wuyeneishe.org.cn</code>

### 综合及衍生资源

<code>jiujiujiujiuguochan.org.cn</code>

<code>neishemama.org.cn</code>

## 项目结构

```
rihan-hub/
├── .github/                         # GitHub 工作流配置
│   └── workflows/
│       ├── health-check.yml         # 每日 02:00 执行健康检查
│       └── pr-validator.yml         # PR 自动校验资源格式
├── data/                            # 数据目录（只读）
│   ├── batches/                     # 批次原始数据（CSV/JSON）
│   │   └── 145/                     # 第 145 批资源文件
│   └── schemas/                     # 数据校验 schema 定义
├── docs/                            # 完整文档体系
│   ├── user-guide/                  # 用户手册章节
│   ├── contributing/                # 贡献指南详细版
│   ├── operations/                  # 部署与运维文档
│   ├── api/                         # API 参考文档
│   └── design/                      # 设计决策记录
├── src/                             # 源代码主目录
│   ├── core/                        # 核心业务逻辑（资源索引、批次管理）
│   ├── api/                         # Flask 路由与请求处理
│   ├── models/                      # ORM 数据模型（Resource, Batch, Tag）
│   ├── services/                    # 外部服务集成（健康检查、缓存）
│   └── utils/                       # 通用工具函数（日志、配置、验证）
├── tests/                           # 单元测试与集成测试
│   ├── unit/                        # 针对 models 和 utils 的测试
│   └── integration/                 # API 端点和健康检查流程测试
├── scripts/                         # 运维及辅助脚本
│   ├── import_batch.py              # 批次导入命令行工具
│   ├── export_catalog.py            # 目录导出为 JSON/CSV
│   └── migrate_db.py                # 数据库版本迁移脚本
├── config/                          # 环境配置文件
│   ├── development.py               # 开发环境配置
│   ├── production.py                # 生产环境配置（敏感信息使用环境变量）
│   └── testing.py                   # CI 测试环境配置
├── requirements.txt                 # Python 生产依赖列表
├── requirements-dev.txt             # 开发及测试额外依赖
├── Makefile                         # 常用命令封装（init, test, run, check）
├── LICENSE                          # MIT 许可证全文
├── CHANGELOG.md                     # 版本变更历史（按批次记录）
├── README.md                        # 本项目文件（即当前文档）
└── .env.example                     # 环境变量模板文件
```

## 贡献指南

1. **阅读行为准则** – 在提交任何内容之前，请仔细阅读项目根目录下的 `CODE_OF_CONDUCT.md` 文件，确保您的行为符合社区友善、尊重和建设性的基本要求。

2. **选择贡献类型** – 明确您要提交的是新增资源链接、更新现有元数据、修复文档错误，还是改进代码实现。不同贡献类型对应不同的模板和审核流程，请参考 `docs/contributing/` 下的详细说明。

3. **本地验证** – 运行 `make test` 执行全部单元测试，确保您的修改未引入回归问题。若涉及新增或修改 URL，请执行 `python manage.py health-check --batch 145` 验证链接可达性，并确认元数据格式符合 `data/schemas/resource_schema.json` 的校验规则。

4. **提交拉取请求** – 从 `main` 分支创建新的特性分支，使用清晰描述性的分支名称（如 `feat/add-batch-146` 或 `fix/update-batch-145-metadata`）。提交信息应遵循约定式提交规范（Conventional Commits），并在 PR 描述中引用相关议题编号（如有）。

5. **响应审核意见** – 项目维护者会在 48 小时内对 PR 进行初审，可能要求补充测试用例、调整元数据描述或澄清变更理由。请保持沟通渠道畅通，及时推送修改内容。合并后，您的贡献将出现在下一版的更新日志中。

## 常见问题

**Q：外部资源链接失效了怎么办？**

A：健康检查模块会在每日定时扫描中自动标记失效链接，并将结果更新到数据库的 `status` 字段。您可以通过 API 端点 `/api/resources?status=dead` 查询所有失效资源。如果您是项目维护者，建议定期查看健康检查报告并联系上游管理员，或寻找替代链接后提交 PR 更新。普通用户可以在 GitHub Issues 中使用 `broken-link` 标签报告失效链接，贡献者会尽快处理。

**Q：如何导入自定义的批量资源列表？**

A：项目支持通过 CSV 或 JSON 格式导入外部列表。您需要准备符合 `data/schemas/import_schema.json` 校验规则的文件，然后使用 `python manage.py import-batch --file <your-file>` 命令执行导入。若需为新批次分配独立的批次号，请使用 `--batch <number>` 参数。导入前建议使用 `--dry-run` 选项进行预检查，避免格式错误导致数据污染。

**Q：生产环境部署时需要注意哪些安全事项？**

A：首先，务必修改默认的 Flask 密钥和环境变量，不要将 `.env` 文件提交到版本控制系统。其次，健康检查模块对外部 URL 发起的请求应设置合理的超时（建议 5 秒）和重试次数（最多 2 次），防止恶意慢响应耗尽资源。最后，如果您的部署环境需要对外暴露 API，建议在反向代理层（如 Nginx）配置速率限制，并启用 HTTPS 以保障传输安全。详细的部署清单请参考 `docs/operations/deployment-checklist.md`。

## 许可证

MIT License

Copyright (c) 2026 Rihan Resource Hub Contributors

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
