# LinkHub Resource Aggregator

LinkHub is a curated technical resource aggregation system designed for developers, researchers, and content archivists who need to organize, categorize, and maintain large-scale external link collections. The project addresses the fundamental challenge of managing distributed web resources across multiple domains, providing a structured indexing framework that supports automated health checks, metadata extraction, and categorical navigation. Target users include open-source documentation maintainers, academic link librarians, and technical content curators who handle batch link collections exceeding fifty entries per release cycle.

The system operates as a static site generation pipeline that consumes plain-text link manifests and produces searchable HTML indices with faceted filtering. Unlike general-purpose bookmark managers, LinkHub implements version-controlled change tracking, link rot detection with Wayback Machine fallback, and batch annotation capabilities tailored for multi-language resource sets. The current release supports Chinese, Japanese, and English resource categorization with automatic language detection and tag suggestion based on domain pattern analysis. All operations are performed locally without external API dependencies, ensuring complete data ownership and offline accessibility.

## 功能概览

- **批量链接摄入与校验** - 支持通过纯文本列表或 CSV 一次性导入大量 URL，自动执行 DNS 解析验证、HTTP 状态码检查及 SSL 证书有效期检测，生成健康状态报告。

- **多维度分类与标签系统** - 允许为每个资源分配类别（文档、视频、社区、工具等）、语言标记（zh-CN, ja-JP, en-US）及自定义标签，支持层级化目录结构映射。

- **链接状态监控与自动报告** - 定时任务每日扫描所有已收录链接，检测 4xx/5xx 错误、重定向链变化及内容哈希变更，变更差异通过邮件或 Webhook 推送通知。

- **静态站点生成器集成** - 内置模板引擎可将链接数据渲染为响应式 HTML 目录页面，支持按分类、语言、状态筛选，并生成 RSS 订阅源供外部消费。

- **元数据缓存与归档** - 对每个链接缓存页面标题、描述摘要及 Open Graph 信息，当原始内容不可达时展示缓存副本，保留至少三个历史版本快照。

- **导入导出兼容性** - 支持标准书签 HTML 格式、JSON Lines 及 Markdown 列表的导入导出，便于与其他工具（浏览器书签管理器、Notion 数据库）进行数据交换。

- **权限与协作支持** - 提供基于角色的访问控制（管理员、编辑者、观察者），所有变更操作记录审计日志，支持通过 Pull Request 模式审核外部提交的链接。

## 应用场景

- **技术文档站点的外链管理** - 开源项目维护者可使用 LinkHub 统一管理文档中引用的第三方库地址、教程链接及 API 参考站点。当依赖的文档站点改版或迁移时，系统自动标记异常并建议替代镜像，避免用户访问失效链接。

- **学术研究参考资料汇编** - 研究机构可利用本系统整理领域相关数据集、论文预印本仓库及工具代码库的链接集合。通过分类标签快速筛选特定主题资源，生成的静态页面可直接作为实验室内部知识库的导航门户。

- **多语言内容本地化协调** - 全球化产品团队在管理多语言文档资源时，使用 LinkHub 追踪各语言版本对应的原始素材链接。系统根据域名特征自动提示语言一致性，帮助识别翻译版本与源文版本的同步状态。

- **媒体素材索引库构建** - 内容创作者可建立视频、音频、图像素材的来源链接索引，配合元数据缓存功能预览素材描述，避免因原始链接失效导致素材来源追溯困难。定期生成的健康报告辅助清理过期资源。

- **社区聚合页动态维护** - 技术社区运营者可收集成员博客、项目仓库及活动页面的链接清单，LinkHub 的自动更新机制确保聚合页始终展示有效资源，降低人工巡检成本。

## 快速开始

以下操作指南适用于 Linux 及 macOS 环境，Windows 用户建议通过 WSL2 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/linkhub-org/linkhub.git
cd linkhub

# 安装依赖（使用 Python 虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 准备链接清单文件（示例：links.txt）
echo "<code>zhongwenzimudibaye.org.cn</code>" >> data/manifest.txt
echo "<code>rihanoumeisetu.org.cn</code>" >> data/manifest.txt

# 执行导入与初始化构建
python linkhub.py import --source data/manifest.txt --category resources
python linkhub.py build --output dist/

# 启动本地预览服务器
python -m http.server 8000 --directory dist/
# 访问 http://localhost:8000 查看生成的索引页面
```

如需执行定时监控任务，可配置 cron 表达式：

```bash
# 每天凌晨 2:00 执行链接健康检查
crontab -e
# 添加以下行
0 2 * * * cd /path/to/linkhub && python linkhub.py check --report --notify
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 - 3.11 | 核心运行环境，类型注解依赖 3.9+ 特性 |
| pip | 21.0+ | 包管理工具，用于安装 requirements.txt 中声明的依赖项 |
| Git | 2.25+ | 版本控制，用于克隆仓库及管理配置文件的变更历史 |
| SQLite | 3.35+ | 嵌入式数据库，存储链接元数据、标签及监控日志，无需额外安装 |
| aiohttp | 3.8.4+ | 异步 HTTP 客户端库，用于并发链接状态检测，提升扫描效率 |
| jinja2 | 3.1.2+ | 模板渲染引擎，驱动静态页面生成器的 HTML 输出 |
| click | 8.1.3+ | 命令行接口框架，提供子命令解析及参数校验能力 |
| pytest | 7.2+ | 单元测试框架（开发依赖），仅在运行测试套件时使用 |
| black | 22.3+ | 代码格式化工具（开发依赖），保持代码风格一致性 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 入门指南 | docs/getting-started.md | 如何快速配置第一个链接集合？链接清单文件应遵循什么格式规范？生成静态页面的最小命令组合是什么？ |
| 配置参考 | docs/configuration.md | 有哪些可用的配置文件项？如何自定义分类映射表？定时监控间隔及通知渠道如何调整？缓存存储路径可否修改？ |
| API 参考 | docs/api/ | 导入模块暴露了哪些编程接口？Link 和 Category 数据类的字段定义及方法签名是什么？如何编写自定义校验钩子？ |
| 运维手册 | docs/operations.md | 如何迁移 SQLite 数据库到新机器？链接数量超过万条时的性能优化建议有哪些？日志轮转策略如何设置？ |
| 贡献指引 | CONTRIBUTING.md | 提交代码或文档修改的完整流程是什么？测试用例编写要求及代码审查通过标准是什么？ |
| 常见问题 | docs/faq.md | 遇到 SSL 证书错误如何排查？为何某些链接始终显示状态为未知？如何强制重新抓取元数据？ |

## 资源列表

### 中文拼音及字符资源

<code>zhongwenzimudibaye.org.cn</code>

<code>zhongwenzimurenqishunv.org.cn</code>

<code>siwarenqizhongwenzimu.org.cn</code>

### 日韩欧美影视及文化资源

<code>rihanoumeisetu.org.cn</code>

<code>ribenshunvshipin.org.cn</code>

<code>oumeilingleishipin.org.cn</code>

<code>guochanoumeirihanyiqu.org.cn</code>

### 综合信息及导航站点

<code>ludashiguanfangwangzhan.org.cn</code>

<code>nvyouzhongwenzimu.org.cn</code>

<code>mitaojiujiujiu.org.cn</code>

## 项目结构

```
linkhub/
├── data/                           # 数据存储目录（用户链接清单及缓存）
│   ├── manifest.txt               # 主链接清单，每行一个 URL
│   ├── archive/                   # 元数据缓存及历史快照（JSON 格式）
│   │   ├── 2026-08-01/            # 按日期组织的缓存目录
│   │   └── latest/                # 指向最新快照的符号链接
│   └── tags.yaml                  # 用户自定义标签与分类映射规则
├── src/                            # 核心源代码
│   ├── linkhub/                    # 主包目录
│   │   ├── __init__.py
│   │   ├── cli.py                 # 命令行入口（click 命令定义）
│   │   ├── importer.py            # 链接解析、去重及数据库写入逻辑
│   │   ├── checker.py             # 异步 HTTP 状态检测与内容哈希计算
│   │   ├── builder.py             # 静态页面渲染器（Jinja2 模板整合）
│   │   ├── models.py              # 数据类定义（Link, Category, CheckResult）
│   │   ├── database.py            # SQLite 连接管理及 ORM 映射辅助
│   │   └── utils.py               # 通用工具函数（域名解析、日期格式化等）
│   └── templates/                  # 页面生成用模板文件
│       ├── base.html              # 基础 HTML 骨架（含导航栏及页脚）
│       ├── index.html             # 首页总览（分类统计及最新变更）
│       ├── category.html          # 分类筛选视图（带标签过滤侧栏）
│       └── detail.html            # 单个链接详情页（含监控历史图表）
├── tests/                          # 单元测试与集成测试
│   ├── test_importer.py           # 导入模块测试（含边界用例）
│   ├── test_checker.py            # 检测器模拟网络响应的测试套件
│   └── fixtures/                  # 测试用静态数据（模拟链接清单）
├── scripts/                        # 运维辅助脚本
│   ├── migrate_db.py              # 数据库版本升级迁移工具
│   ├── export_bookmarks.py        # 导出为浏览器书签 HTML 格式
│   └── cleanup_cache.py           # 清理过期缓存及日志轮转
├── docs/                           # 项目文档（Markdown 格式）
│   ├── getting-started.md
│   ├── configuration.md
│   └── operations.md
├── requirements.txt               # 生产环境依赖列表（含版本锁定）
├── setup.py                       # 打包与分发配置（setuptools）
├── .github/                       # GitHub 工作流配置
│   └── workflows/
│       └── ci.yml                 # 持续集成（测试覆盖率及代码风格检查）
├── .gitignore
└── README.md                      # 本文件
```

## 贡献指南

1.  **分支开发流程** - 从 `main` 分支创建功能分支（命名格式为 `feature/描述` 或 `fix/描述`），所有开发工作在该分支进行。提交信息遵循 Conventional Commits 规范，使用 `<type>: <subject>` 格式（例如 `feat: add batch import from CSV`）。

2.  **本地测试验证** - 在提交前必须运行完整测试套件，确保所有单元测试及集成测试通过。执行 `pytest tests/ --cov=src/linkhub --cov-report=term` 检查代码覆盖率不低于 85%。新增功能需同步编写对应测试用例。

3.  **文档同步更新** - 任何影响用户使用方式或配置接口的变更，必须同时更新 `docs/` 目录下对应的文档文件。命令行参数变更需同步更新 `cli.py` 中的帮助文本。

4.  **Pull Request 提交规范** - 向 `main` 分支发起 Pull Request 时，描述中需清晰说明变更动机、实现方案及测试结果。至少需要一位项目维护者 Approve 后方可合并。CI 流水线全部通过为合并的前置条件。

5.  **问题报告与建议** - 使用 GitHub Issues 提交 bug 报告或功能请求。Bug 报告需包含复现步骤、预期行为与实际行为对比，以及运行环境信息（Python 版本、操作系统）。功能请求需阐述应用场景及收益分析。

## 常见问题

**问：导入链接清单时提示 DNS 解析失败，但这些网站在浏览器中可以正常访问，是什么原因？**

答：该现象通常由网络环境差异导致。LinkHub 默认使用系统 DNS 解析器，而浏览器可能使用了 DoH（DNS over HTTPS）或代理设置。解决方案有两种：一是在配置文件 `config.yaml` 中指定备用 DNS 服务器（如 `8.8.8.8` 或 `1.1.1.1`）；二是通过 `--skip-dns` 参数跳过 DNS 预检，仅依赖 HTTP 请求结果判断链接可用性。同时检查系统代理环境变量 `HTTP_PROXY` 和 `HTTPS_PROXY` 是否正确设置，若企业网络需使用代理访问外网，请将代理地址添加至 `config.yaml` 的 `proxy` 字段。

**问：静态页面生成后，分类筛选和标签过滤在浏览器中无效，页面显示空白或没有筛选结果？**

答：此问题多为浏览器的安全策略限制导致，当使用 `file://` 协议直接打开生成的 HTML 文件时，同源策略会阻止 JavaScript 加载本地数据文件。解决方法为通过 HTTP 服务器提供文件服务（如使用 `python -m http.server` 或 `npx serve`），确保数据通过 `fetch` API 正常获取。若仍存在问题，请检查 `dist/` 目录下的 `data.js` 文件是否成功生成，以及 `index.html` 中引用的静态资源路径是否使用相对路径。可尝试执行 `python linkhub.py build --force` 强制重新生成全部文件。

**问：监控任务发现链接状态变化（如 200 变为 404），如何回溯查看该链接的历史状态记录？**

答：所有监控结果均持久化存储在 SQLite 数据库的 `check_history` 表中。可使用内置命令 `python linkhub.py history --url <域名>` 输出该链接的全部检查时间轴，包含状态码、响应时间及内容哈希值。如需恢复之前缓存的页面元数据，可执行 `python linkhub.py restore --url <域名> --timestamp <YYYY-MM-DD>`，系统将从 `data/archive/` 目录提取对应日期的缓存快照，并重新生成详情页面。历史记录默认保留 90 天，超过期限的数据可通过 `scripts/cleanup_cache.py --keep-days 90` 进行清理。

## 许可证

MIT License

Copyright (c) 2026 LinkHub Contributors

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
