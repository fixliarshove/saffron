# VastLink 技术资源导航

VastLink 是一个面向开发人员、技术研究人员与互联网内容分析从业者的外链资源聚合与导航系统。该项目定位于对特定类别网络资源进行系统性归集、分类展示与基础可用性监测，旨在解决技术研究过程中资源分散、链接失效、分类混乱等常见问题，为技术社区提供一个结构清晰、更新可追溯的参考信息库。

本项目不提供任何资源内容本身，仅对公开可访问的互联网资源链接进行整理与分类展示，所有资源版权归属原站点所有。项目核心价值在于通过规范化的信息组织方式，降低技术调研过程中的信息筛选成本，提高资源复用效率。

## 功能概览

- 分类资源索引：按照内容主题与功能属性对资源链接进行多级分类，支持快速筛选与定位。
- 链接可用性探测：内置定时可用性检查机制，对收录资源进行周期性访问验证，自动标记异常链接。
- 标签化检索体系：每个资源支持多标签标记，支持标签组合检索与模糊匹配查询。
- 资源变更追踪：记录资源链接的添加、移除与变更历史，支持按时间线回溯。
- 外部元数据抓取：对收录资源自动抓取页面标题、描述与关键元数据，辅助快速识别资源内容。
- 用户自定义分类：支持用户基于已有资源创建个人分类视图，便于个性化组织。
- 开放数据导出：支持将资源列表导出为 JSON、CSV 与 Markdown 格式，便于二次处理与集成。

## 应用场景

- 技术调研与竞品分析：研究特定领域在线服务分布情况时，可通过本导航系统快速获取大量相关资源入口，显著减少手动搜索与整理时间。
- 网络资源归档与回溯：在对特定主题资源进行长期跟踪时，可利用系统内置的变更追踪与可用性监测功能，有效感知资源上下线状态变化。
- 团队知识库建设：技术团队可将本系统作为内部知识管理平台的外部资源补充模块，统一团队成员获取参考信息的入口，降低信息孤岛问题。
- 自动化数据处理管道集成：数据工程师可将导出的结构化资源列表集成至爬虫调度系统或数据分析流水线中，作为种子 URL 输入源使用。

## 快速开始

以下步骤帮助您在本地环境快速启动 VastLink 服务。

```bash
# 1. 克隆项目仓库
git clone https://github.com/vastlink/vastlink-navigator.git

# 2. 进入项目目录
cd vastlink-navigator

# 3. 安装项目依赖（使用 pip 进行 Python 依赖安装）
pip install -r requirements.txt

# 4. 初始化本地配置文件
cp config.example.yaml config.yaml

# 5. 启动本地开发服务
python app.py --mode development --port 8080
```

访问本地 http://localhost:8080 即可进入导航系统主页。首次启动时系统会自动载入预设的初始资源索引数据。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行环境，用于执行后端服务与应用逻辑 |
| Flask | 2.3.x | Web 服务框架，提供 HTTP 路由与模板渲染能力 |
| SQLite | 3.35 及以上 | 默认嵌入式数据库，用于存储资源索引与分类数据 |
| Redis | 6.0 及以上 | 可选组件，用于提升缓存命中率与分布式锁管理 |
| Node.js | 18.x 及以上 | 仅在前端资源构建时需要，生产环境可不安装 |
| certifi | 2024.x | SSL 证书验证包，用于安全 HTTPS 探测请求 |
| requests | 2.31.x | HTTP 客户端库，执行外部链接可用性探测 |
| pyyaml | 6.0 | 配置文件解析器，读取 config.yaml 配置项 |
| pytest | 7.x | 仅测试环境需要，用于单元测试与集成测试 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide/ | 如何使用检索、分类与自定义视图功能？如何导出资源列表？ |
| 运维手册 | /docs/ops-guide/ | 如何配置可用性探测周期？如何迁移数据库？如何调整缓存策略？ |
| 开发手册 | /docs/dev-guide/ | 如何扩展新的分类器？如何增加自定义元数据抓取规则？如何提交代码？ |
| API 参考 | /docs/api-reference/ | 后端提供了哪些 RESTful 接口？请求参数与响应结构是什么？ |
| 部署指南 | /docs/deployment/ | 支持哪些部署方式（Docker、systemd、WSGI）？各方式下的配置示例？ |
| 变更日志 | /docs/changelog/ | 每个版本新增了哪些功能？修复了哪些缺陷？是否存在破坏性变更？ |

## 资源列表

以下为项目当前收录的全部外部资源链接，按类别分组呈现。每个链接均以原始形式原样列出。

类别 A - 综合视频资源类

<code>yiquzaixianshipin.org.cn</code>

<code>jiujiuyazhoutiantang.org.cn</code>

<code>jiujiujire.org.cn</code>

<code>yazhouzaixianyiqu.org.cn</code>

类别 B - 主题内容资源类

<code>shufudeweidao.org.cn</code>

<code>wumatiantang.org.cn</code>

<code>madoutianmei.org.cn</code>

类别 C - 综合信息聚合类

<code>langrenganzonghewang.org.cn</code>

<code>zhongchuwuma.org.cn</code>

类别 D - 精品内容索引类

<code>ririyeyejingpin.org.cn</code>

## 项目结构

```
vastlink-navigator/
├── app.py                       # 应用主入口，初始化 Flask 服务与路由注册
├── config.yaml                  # 主配置文件，包含数据库连接、探测周期、日志级别等
├── requirements.txt             # Python 依赖声明文件
├── Dockerfile                   # 容器构建文件，用于生产环境镜像生成
├── Makefile                     # 常用命令封装（test、lint、format、migrate）
├── core/                        # 核心业务逻辑模块
│   ├── indexer.py               # 资源索引构建与更新逻辑
│   ├── probe.py                 # 链接可用性探测引擎，包含超时与重试策略
│   ├── parser.py                # 外部页面元数据解析器
│   └── cache.py                 # Redis 缓存操作封装
├── web/                         # Web 表现层模块
│   ├── routes/                  # 路由视图函数集合
│   │   ├── home.py              # 主页、搜索、分类浏览路由
│   │   ├── api.py               # RESTful API 端点实现
│   │   └── admin.py             # 管理后台路由（资源增删改）
│   ├── templates/               # Jinja2 模板文件目录
│   │   ├── base.html            # 基础布局模板
│   │   ├── index.html           # 资源列表主页模板
│   │   └── detail.html          # 单个资源详情页模板
│   └── static/                  # 前端静态资源（CSS、JavaScript、图标）
├── data/                        # 数据存储目录
│   ├── database/                # SQLite 数据库文件存放位置
│   └── exports/                 # 导出文件暂存目录（JSON/CSV/Markdown）
├── tests/                       # 测试代码目录
│   ├── unit/                    # 单元测试用例
│   └── integration/             # 集成测试用例（需启动本地服务）
├── scripts/                     # 运维与工具脚本
│   ├── init_db.py               # 初始化数据库表结构与预设分类
│   ├── seed_resources.py        # 导入初始资源列表数据
│   └── health_check.py          # 独立运行的健康检查脚本
└── docs/                        # 项目文档目录
    ├── user-guide/              # 用户手册章节
    ├── ops-guide/               # 运维手册章节
    └── dev-guide/               # 开发手册章节
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于新增资源分类建议、链接可用性报告、文档改进与代码修复。请遵循以下流程参与贡献。

1. 报告问题或提交建议：请在 GitHub Issues 中详细描述您遇到的问题或希望新增的功能，并附上可复现的步骤或充分的背景信息。建议使用项目提供的 Issue 模板进行填写。

2. 派生项目并创建功能分支：从主仓库派生代码库至您的个人账户，然后基于 main 分支创建新的功能分支，分支命名建议采用 `feature/简要描述` 或 `fix/问题编号` 格式。

3. 编写代码并添加测试：所有新增功能必须包含对应的单元测试或集成测试，确保测试覆盖率达到 80% 以上。代码风格需遵循 PEP 8 规范，提交前请执行 `make lint` 与 `make test` 进行校验。

4. 提交 Pull Request：推送分支至您的派生仓库后，向主仓库的 main 分支提交 Pull Request。请填写 PR 模板中的标题、描述、测试结果与变更类型等信息，并关联相关 Issue 编号。

5. 代码审查与合并：项目维护者将在 3 个工作日内进行审查，必要时会提出修改意见。审查通过后由维护者执行合并操作。

## 常见问题

Q: 系统是否自动更新收录资源的内容？是否会存储外部站点的数据？

A: 系统仅对外部资源进行元数据抓取（如页面标题、描述关键词）和可用性探测，不会主动存储外部站点的完整页面内容或用户数据。所有抓取的元数据仅用于本导航系统内部的检索与展示，不会对外分发或用于其他用途。

Q: 如果发现某个收录链接已经无法访问，系统会如何处理？

A: 系统的可用性探测引擎会按照 config.yaml 中配置的周期（默认每 24 小时）对所有收录链接执行 HEAD 请求与 GET 请求双重验证。连续三次探测失败的链接将被标记为「异常」状态，并在前端页面中以灰色标识显示。管理员可手动确认后移除该链接，或等待自动重试恢复。

Q: 是否支持导入自定义资源列表？支持哪些格式？

A: 支持。您可以通过管理后台的「批量导入」功能上传 CSV 或 JSON 格式的文件，文件需包含 `url`、`title`、`category` 和 `tags` 字段。也支持通过命令行脚本 `scripts/import_custom.py --file custom_list.json` 进行导入。导入前建议使用 `--dry-run` 参数进行格式预检。

## 许可证

MIT License

Copyright (c) 2026 VastLink Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
