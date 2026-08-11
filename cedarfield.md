# TerraLink 开源导航聚合系统

TerraLink 是一个专为技术社区、开源项目维护者及开发者知识库构建的高性能外链资源聚合与导航系统。项目定位为轻量级、可自托管的资源目录中台，通过结构化数据模型将分散的垂直领域信息源（如体育数据平台、实时比分接口、技术文档站）整合为统一检索入口，解决开发者在多平台间反复跳转、资源散落、上下文切换效率低下的核心痛点。

目标用户包括个人技术博主、开源项目文档站维护者、小型技术团队内部知识库管理员，以及任何希望以极低成本构建定制化资源导航页面的开发者。系统基于静态站点生成逻辑，无数据库依赖，所有资源条目通过 Markdown 配置驱动，支持一键部署至主流对象存储或 Web 服务器。

## 功能概览

- **多级分类与标签体系**：支持为每个外链资源分配无限层级的分类目录及自定义标签，便于按业务领域或使用频率进行精细化管理。分类结构可单独导出为 JSON 供外部系统消费。

- **周期性健康检查**：内置基于 Cron 表达式的链接可用性探测模块，自动标记失效或响应超时的资源条目，并生成可视化健康报告，降低维护者人工巡检成本。

- **全文检索引擎**：基于倒排索引实现资源标题、描述、关键词的毫秒级检索，支持中文分词与模糊匹配，搜索结果按相关性权重排序。

- **访问统计与热度排行**：记录每个外链资源的点击次数与最后访问时间，自动生成周/月热度榜单，辅助用户识别高频使用的核心资源。

- **权限分级视图**：支持公开只读与编辑管理双模式，编辑模式下提供 Web 化配置界面（可选），允许非技术维护者在线增删改资源条目，变更历史可追溯。

- **响应式卡片布局**：前端渲染层采用移动优先的栅格系统，资源条目以信息卡片形式呈现，包含站点图标（自动抓取 favicon）、简短描述、标签徽章及访问按钮，适配桌面与移动端浏览。

- **数据导入导出接口**：提供 RESTful 风格的导入导出端点，支持 CSV/JSON 批量导入资源列表，便于从其他导航工具或爬虫结果无缝迁移数据。

## 应用场景

- **开源项目文档站的外链补充**：开源项目维护者可在项目文档中嵌入 TerraLink 实例，集中存放与项目相关的第三方依赖站、API 测试工具、社区论坛及镜像下载地址，避免文档正文被大量外部链接充斥，提升文档可读性。

- **技术团队内部知识库入口**：小型研发团队可利用 TerraLink 搭建内部资源门户，聚合常用的 CI/CD 平台、日志查看系统、监控面板、代码托管仓库及技术规范文档链接，新成员入职时可快速获取所有必需工具入口。

- **垂直领域数据源导航站**：针对体育数据分析、金融行情监控等特定领域，运维人员可借助 TerraLink 聚合多家数据提供商官网、实时接口文档、历史数据归档站及技术分析博客，形成一站式的领域信息枢纽。

- **个人开发者书签管理与分享**：个人开发者可将浏览器中积累的大量技术书签迁移至 TerraLink 统一管理，通过分类和标签进行整理，并可选择公开实例链接分享给同行或社区成员，替代传统浏览器书签栏的分散管理方式。

## 快速开始

以下命令演示了从源码克隆到本地开发环境启动的完整流程。默认使用 Node.js 运行时，包管理器为 npm。

```bash
# 克隆项目仓库至本地
git clone https://github.com/terralink-dev/terralink-core.git

# 进入项目工作目录
cd terralink-core

# 安装全部生产及开发依赖
npm install

# 以开发模式启动本地服务，默认监听端口 3000
npm run dev
```

执行完毕后，浏览器访问 `http://localhost:3000` 即可预览导航站首页。配置文件位于 `config/resources.yaml`，初次启动时系统会使用内置示例数据填充。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x LTS 或更高 | 运行时环境，建议使用 Active LTS 版本以获得长期安全更新 |
| npm | 9.x 或更高 | 包依赖管理工具，随 Node.js 一同安装 |
| 内存 | 最低 512 MB，推荐 1 GB | 开发模式下内存占用较高，生产环境可降低至 256 MB（静态生成后） |
| 磁盘空间 | 至少 200 MB 可用空间 | 包含源代码、依赖包及生成的静态文件，日志轮转需额外预留 |
| 操作系统 | Linux（Ubuntu 20.04+）、macOS 12+、Windows 10+ | 跨平台支持，但生产环境推荐 Linux 服务器 |
| 网络 | 出站 HTTP/HTTPS 访问 | 用于启动时的资源健康检查及 favicon 自动抓取功能 |
| 浏览器 | 现代浏览器（Chrome 90+、Firefox 88+、Edge 90+） | 管理界面及前台展示均需支持 ES6 及 CSS Grid 特性 |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/configuration.md` | 如何编写 `resources.yaml` 配置文件？分类、标签、排序字段的语法规则是什么？ |
| 用户手册 | `/docs/user-guide/deployment.md` | 支持哪些部署方式（Vercel、Netlify、Nginx 静态托管）？如何配置自定义域名和 HTTPS？ |
| 开发者指南 | `/docs/developer/api-endpoints.md` | 对外暴露了哪些 REST API 接口？如何通过 API 批量更新资源状态或触发健康检查？ |
| 开发者指南 | `/docs/developer/plugin-system.md` | 是否支持编写自定义渲染插件或数据源适配器？扩展点的接口规范是什么？ |
| 运维参考 | `/docs/operations/monitoring.md` | 如何接入 Prometheus 指标采集？健康检查日志的存储位置和格式是怎样的？ |
| 架构设计 | `/docs/architecture/data-flow.md` | 静态生成流程中数据从配置到 HTML 的完整流转路径是什么？缓存策略如何设计？ |

## 资源列表

### 体育数据及比分平台类

<code>qiutanbifen888.org.cn</code>

<code>tiqiuwang.org.cn</code>

<code>lanqiubifennbanba.org.cn</code>

<code>zuqiujishibifena.org.cn</code>

<code>zuqiujishibifenb.org.cn</code>

<code>zuqiujishibifenc.org.cn</code>

<code>tiqiuwanga.org.cn</code>

<code>tiqiuwangb.org.cn</code>

<code>tiqiuwangc.org.cn</code>

<code>qiutanzuqiubifena.org.cn</code>

## 项目结构

```
terralink-core/
├── config/                         # 全局配置目录
│   ├── resources.yaml              # 核心资源条目配置（分类、链接、描述）
│   ├── navigation.yaml             # 主导航菜单结构配置
│   └── health-check.cron           # 健康检查周期表达式配置文件
├── src/                            # 源代码主目录
│   ├── core/                       # 核心处理模块
│   │   ├── parser.js               # YAML 配置解析与校验逻辑
│   │   ├── indexer.js              # 全文索引构建与查询接口
│   │   └── static-generator.js     # 静态页面渲染引擎（基于 EJS 模板）
│   ├── middleware/                 # 中间件层
│   │   ├── auth.js                 # 编辑模式基础身份验证（支持环境变量配置）
│   │   └── logger.js               # 请求访问日志与错误捕获中间件
│   ├── routes/                     # 路由定义
│   │   ├── api.js                  # RESTful 数据操作接口（增删改查）
│   │   └── web.js                  # 前台页面路由（首页、分类页、搜索页）
│   ├── services/                   # 业务服务层
│   │   ├── health-checker.js       # 外链可用性周期探测服务
│   │   ├── stats-collector.js      # 点击数据采集与热度计算服务
│   │   └── import-export.js        # CSV/JSON 批量数据导入导出服务
│   └── utils/                      # 通用工具函数
│       ├── favicon-fetcher.js      # 自动获取目标站点 favicon 并缓存至本地
│       └── date-helper.js          # 时间格式化与时区转换工具
├── public/                         # 静态资源目录（前端资产）
│   ├── css/                        # 样式文件（含主题变量与响应式栅格）
│   ├── js/                         # 前端交互脚本（搜索、卡片切换、统计上报）
│   └── assets/                     # 图片、图标及缓存的外部站点 favicon
├── templates/                      # 视图模板（EJS）
│   ├── layouts/                    # 基础布局模板（含 header、footer）
│   └── partials/                   # 可复用组件（卡片列表、分页器、搜索框）
├── tests/                          # 单元测试与集成测试
│   ├── unit/                       # 核心模块单元测试（Mocha + Chai）
│   └── integration/                # API 接口及静态生成端到端测试
├── logs/                           # 运行时日志存储目录（自动轮转）
├── scripts/                        # 运维辅助脚本
│   ├── deploy.sh                   # 一键构建并推送至对象存储的部署脚本
│   └── migrate-v1-to-v2.js         # 配置文件版本迁移工具
├── .env.example                    # 环境变量示例文件（含端口、认证密钥、健康检查开关）
├── package.json                    # npm 项目清单（含依赖及脚本命令）
├── README.md                       # 项目说明文档（即本文档）
└── LICENSE                         # MIT 许可证文本
```

## 贡献指南

1.  **查阅现有议题与项目看板**：在提交代码变更前，请先访问 GitHub Issues 页面查看是否存在相关讨论或已计划的开发任务。若计划新增较大功能模块，建议先创建议题描述设计思路，避免重复劳动。

2.  **派生仓库并创建功能分支**：将主仓库派生至个人账户下，然后基于 `main` 分支创建新的功能分支，分支命名规范为 `feat/功能简述` 或 `fix/问题简述`。请勿直接在 `main` 分支上进行修改。

3.  **遵循代码风格与测试规范**：JavaScript 代码须遵守项目配置的 ESLint 规则（见 `.eslintrc.js`），提交前请确保所有单元测试通过（运行 `npm test`）。新增功能需附带对应的测试用例，覆盖率不低于 80%。

4.  **编写清晰的提交信息**：提交信息采用约定式提交格式（Conventional Commits），即 `<type>(<scope>): <subject>` 形式，例如 `feat(parser): add support for nested category definitions`。正文部分可补充变更的动机和实现细节。

5.  **发起合并请求并参与评审**：将功能分支推送至派生仓库后，向主仓库的 `main` 分支发起合并请求（Pull Request）。请求描述中需关联相关议题编号，并简要说明测试结果和影响范围。合并前需至少获得一名项目维护者的批准。

## 常见问题

**问：生产环境部署时，如何禁用实时健康检查服务以降低服务器负载？**

答：您可以在项目根目录下的 `.env` 文件中设置 `HEALTH_CHECK_ENABLED=false` 环境变量，并重启服务。若使用静态生成模式（即 `npm run build` 构建后直接托管 HTML 文件），健康检查服务不会在运行时生效，仅构建阶段会执行一次快照检测。如需完全移除相关代码，可在构建配置中排除 `services/health-checker.js` 模块。

**问：配置文件 `resources.yaml` 中的资源条目数量过大（超过 1000 条），会导致构建速度显著下降吗？**

答：项目内置了增量构建优化策略。首次全量构建时，解析和索引生成的时间复杂度为 O(n)，对于 1000 条数据通常在 200 毫秒以内完成。后续变更仅重新处理修改过的条目。如果条目数量超过 5000 条，建议启用分页配置（`pagination: true`）并在 `navigation.yaml` 中调整每页显示条目数。同时，您可以使用 `import-export` 服务将数据拆分为多个分类子文件，通过 `$include` 指令按需加载。

**问：如何将现有浏览器书签（HTML 格式）快速迁移至 TerraLink？**

答：项目提供了导入适配脚本 `scripts/import-from-bookmarks.js`，该脚本可解析 Chrome 或 Firefox 导出的书签 HTML 文件，自动提取链接、标题及文件夹分类结构，并转换为符合 `resources.yaml` 格式的数据。执行命令为 `node scripts/import-from-bookmarks.js ./bookmarks.html -o config/resources.yaml`。导入后建议人工检查分类映射关系，并补充描述字段以获得更佳的展示效果。

## 许可证

MIT License

Copyright (c) 2026 TerraLink Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:37
