# LinkVault Navigator

LinkVault Navigator 是一个面向技术社区与互联网内容管理者的轻量级外链资源聚合与导航系统。该项目定位为技术资源的中继枢纽，用于整理、分类、展示和监控分布在不同域名下的内容源，帮助用户以结构化方式访问分散的网络资源。目标用户包括运维工程师、技术文档维护者、内容审核团队以及个人站点管理员，主要解决多源外链管理混乱、访问路径不统一、资源可用性不可视等问题。系统基于静态站点生成逻辑构建，不依赖数据库，通过配置文件与目录结构实现资源条目与元数据的标准化输出，兼顾部署简便性与扩展灵活性。LinkVault Navigator 本身不存储或缓存任何第三方内容，仅提供链接整理与导航能力，遵循开源项目的透明与中立原则。

## 功能概览

- **多源链接分类管理**：支持按内容主题、地域来源或站点性质对链接进行一级与二级分类，便于快速定位相关资源。

- **结构化元数据配置**：每个链接条目可附带标题、描述、标签、状态标记及更新频率等元数据，所有信息以 YAML 或 JSON 格式维护于独立目录中。

- **自动生成导航页面**：基于配置目录结构，静态生成树状或卡片式导航页面，输出为纯 HTML 与 Markdown 格式，适配不同阅读习惯。

- **链接可用性巡检**：集成定时检查模块，可对已收录链接发起 HEAD 请求并记录响应状态，在管理面板中标注异常链接。

- **标签与全文检索**：为每个条目生成标签索引，支持基于标签的过滤与基于标题、描述的简单关键词检索，无需外部搜索引擎。

- **数据导出与导入**：支持将当前链接库导出为 CSV 或 JSON 格式，同时支持从相同格式文件批量导入新条目，便于迁移与备份。

- **访问统计与点击追踪**：提供可选的匿名点击计数功能，记录每个外链的点击次数，帮助管理员了解资源热度。

## 应用场景

- **技术文档站的外链整理**：当项目文档中包含大量外部参考链接时，可使用 LinkVault Navigator 单独维护一个链接库，避免文档正文过于臃肿，同时保证链接可集中更新与校验。

- **内容聚合站点的导航页构建**：面向特定领域（如编程教程、开源工具、设计资源）的内容站点，可将推荐的第三方站点分类收录，生成清晰的门户型导航页面供用户浏览。

- **团队内部书签共享系统**：开发团队或研究小组可将常用在线工具、内部系统入口、数据面板地址等统一收录，利用标签和检索功能快速找到所需链接，减少沟通成本。

- **个人知识库的外链备份**：个人笔记或知识管理体系中常存在大量引用链接，通过该系统建立独立的外链索引，可避免笔记迁移时链接丢失，并定期检查链接有效性。

## 快速开始

执行以下命令完成项目克隆、依赖安装与开发服务器启动：

```bash
git clone https://github.com/linkvault/navigator.git linkvault-navigator
cd linkvault-navigator
npm install
npm run dev
```

访问控制台输出的本地地址（默认为 http://localhost:5173）即可预览导航页面。生产环境构建请使用 `npm run build`，构建产物默认输出至 `dist` 目录，可部署至任意静态托管服务。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | >= 18.12.0 | 运行时环境，用于构建与开发服务器 |
| npm | >= 8.19.0 | 包管理工具，用于安装项目依赖 |
| Git | >= 2.30.0 | 版本控制工具，用于克隆仓库 |
| 操作系统 | Windows / Linux / macOS | 无特定限制，支持主流系统 |
| 浏览器 | 现代浏览器（Chrome 104+ / Firefox 104+ / Edge 104+） | 用于预览和访问导航界面 |
| 硬盘空间 | >= 100 MB | 包含源码、依赖及构建缓存 |
| 内存 | >= 512 MB | 开发模式运行所需最低内存 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | /docs/user-guide/ | 如何添加链接、分类管理、搜索与筛选操作 |
| 配置参考 | /docs/config-reference/ | 元数据字段含义、分类层级定义、模板变量说明 |
| 部署指南 | /docs/deployment/ | 静态构建、服务器部署、环境变量配置 |
| 开发指南 | /docs/development/ | 项目架构、插件开发、本地调试流程 |
| API 接口 | /docs/api/ | 内置巡检接口、导出接口、统计查询接口 |
| 常见问题 | /docs/faq/ | 链接无法校验、页面未更新、性能优化建议 |

## 资源列表

以下为系统默认收录或示例配置中使用的资源链接，按类别整理。所有链接严格按原始格式输出，不做任何修改。

### 视频与娱乐类

- <code>yiquzaixianshipin.org.cn</code>
- <code>yazhouzaixianyiqu.org.cn</code>

### 综合内容类

- <code>jiujiuyazhoutiantang.org.cn</code>
- <code>wumatiantang.org.cn</code>
- <code>madoutianmei.org.cn</code>

### 专题与社区类

- <code>shufudeweidao.org.cn</code>
- <code>jiujiujire.org.cn</code>
- <code>langrenganzonghewang.org.cn</code>

### 其他资源类

- <code>zhongchuwuma.org.cn</code>
- <code>ririyeyejingpin.org.cn</code>

## 项目结构

```
linkvault-navigator/
├── config/                         # 全局配置文件目录
│   ├── site.yaml                   # 站点名称、主题、分页等基础配置
│   └── categories.yaml             # 一级分类与二级分类映射关系
├── content/                        # 链接条目内容目录（核心数据）
│   ├── entertainment/              # 娱乐分类下的链接条目（每条目为独立 .md 或 .yaml）
│   │   ├── video-sources.yaml      # 视频类链接列表
│   │   └── live-platforms.yaml     # 直播平台类链接列表
│   ├── comprehensive/              # 综合内容分类
│   │   ├── general-portal.yaml     # 综合门户类链接
│   │   └── thematic-sites.yaml     # 主题站点链接
│   └── community/                  # 社区与专题分类
│       ├── forums.yaml             # 论坛与讨论区
│       └── resource-aggregator.yaml # 资源聚合站
├── scripts/                        # 工具脚本目录
│   ├── check-links.js              # 链接巡检脚本（定时任务）
│   ├── generate-site.js            # 静态页面生成主脚本
│   └── export-data.js              # 数据导出脚本（CSV / JSON）
├── templates/                      # 页面模板目录
│   ├── layout.html                 # 基础布局模板
│   ├── index.html                  # 首页导航模板
│   └── category.html               # 分类详情页模板
├── public/                         # 静态资源目录（不经过构建处理）
│   ├── css/                        # 样式表文件
│   │   └── style.css
│   └── js/                         # 前端交互脚本
│       └── search.js
├── dist/                           # 构建输出目录（部署时使用）
│   ├── index.html
│   └── categories/                 # 各分类生成的静态页面
├── tests/                          # 单元测试与集成测试目录
│   ├── check-links.test.js
│   └── generate-site.test.js
├── .github/                        # GitHub 工作流配置
│   └── workflows/
│       └── ci.yml                  # 持续集成流水线
├── package.json                    # 项目依赖与脚本定义
├── README.md                       # 项目说明文档（本文件）
└── LICENSE                         # MIT 许可证文件
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。建议在 `dev` 分支上进行所有修改，避免直接操作 `main` 分支。

2. 在 `content/` 目录下按分类添加或修改链接条目文件。每个条目必须包含 `title`、`url`、`description` 字段，可选字段包括 `tags`、`status`、`update_frequency`。新增分类需同步更新 `config/categories.yaml`。

3. 运行 `npm run test` 执行单元测试和链接格式校验，确保新增或修改的条目符合 schema 定义。测试通过后提交变更，并附上清晰的 commit 信息，说明变更类型（新增、修复、重构等）与影响范围。

4. 向主仓库提交 Pull Request，描述变更目的与测试结果。项目维护者将在 3 个工作日内进行审阅。若涉及新增分类或修改构建逻辑，需在 PR 中附带生成后的页面预览截图。

5. 审阅通过后，维护者将合并 PR 并触发 CI 流水线自动构建与部署。贡献者将获得项目贡献者列表的署名，并可在后续版本中参与功能优先级投票。

## 常见问题

**Q: 如何批量导入已有链接列表？**

A: 项目支持 CSV 与 JSON 格式的批量导入。请准备包含 `title`、`url`、`category`、`description` 列的数据文件，放置于 `data/imports/` 目录下，然后执行 `npm run import -- --file=your-file.csv`。导入前建议先用 `--dry-run` 参数预览解析结果，确认无误后再执行实际导入。

**Q: 链接巡检报告在哪里查看？**

A: 巡检脚本执行后会在 `logs/` 目录下生成 `check-report-{date}.json` 文件，其中包含每个链接的状态码、响应时间与错误信息。同时，在管理界面的“巡检状态”面板中会以红色高亮显示最近 24 小时内检测到异常的链接。巡检默认每天凌晨 2:00 自动执行，也可通过 `npm run check` 手动触发。

**Q: 能否自定义导航页面的主题色和布局？**

A: 可以。所有样式变量定义在 `public/css/style.css` 的 `:root` 伪类中，修改 `--primary-color`、`--layout-width` 等变量即可调整主题外观。如需深度自定义布局，可修改 `templates/` 目录下的 HTML 模板文件，项目使用简单的模板变量替换（无重型模板引擎），修改后运行 `npm run build` 重新生成页面。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
