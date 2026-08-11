# HyperLink Navigator

HyperLink Navigator 是一个面向技术开发者与开源项目维护者的轻量级外链资源聚合与导航系统。该项目定位于解决技术文档、项目 README、博客教程中外部链接分散、失效、难以统一管理的问题，通过结构化的资源收录与呈现机制，帮助用户快速建立可维护、可审计、可追溯的外链资源目录。

目标用户包括开源项目作者、技术文档撰写者、社区运营人员以及企业内部知识管理团队。HyperLink Navigator 不依赖数据库，纯静态生成，兼容 GitHub Pages、Vercel、Netlify 等主流托管平台，支持 Markdown 驱动的资源清单自动渲染为可视化导航页面，并提供链接可用性检测与失效提醒机制。

## 功能概览

- **结构化资源收录**：支持按类别、标签、批次对 URL 进行分组管理，内置分类模板，便于维护大规模外链清单。

- **链接可用性探测**：集成异步 HTTP 健康检查，自动标记响应异常或超时的链接，生成状态报告。

- **静态页面渲染引擎**：基于 Markdown 配置文件，自动生成响应式导航页面，支持明暗主题与移动端适配。

- **链接变更追踪**：记录每次资源列表的修改历史，支持 diff 对比，便于审计和回滚。

- **自定义元数据扩展**：每条链接可附加描述、维护人、添加日期、过期策略等自定义字段，满足企业级管理需求。

- **批量导入与导出**：支持从 CSV、JSON、OPML 格式导入链接，导出为标准 Markdown 或 HTML 报告。

- **链接关系图谱**：可视化展示资源之间的引用关系与依赖层级，辅助理解信息架构。

## 应用场景

**技术文档外链附录管理**  
开源项目维护者可使用 HyperLink Navigator 管理 README 中引用的所有第三方文档、工具站、API 参考链接，当上游链接失效时系统自动告警，避免文档中出现死链。

**社区资源聚合导航页**  
技术社区或博客作者可构建专属的资源导航站，将常用开发工具、学习资料、官方文档按主题分类展示，提供比浏览器书签更清晰、可分享的公开入口。

**企业内部知识库链接治理**  
企业知识管理团队可利用本系统对内部 Wiki、Confluence、Notion 中的外部引用进行集中登记与周期性可用性验证，降低因链接漂移导致的信息丢失风险。

**开源项目目录索引**  
开源组织可使用本系统维护多项目依赖的外部服务清单，例如 CI/CD 工具、代码质量平台、容器镜像仓库地址，确保团队统一认知。

## 快速开始

以下步骤将在本地环境克隆项目、安装依赖并启动开发服务器。

```bash
# 克隆仓库
git clone https://github.com/hyperlink-navigator/hyperlink-navigator.git
cd hyperlink-navigator

# 安装依赖（使用 npm）
npm install

# 启动开发服务
npm run dev
```

启动成功后，访问 `http://localhost:3000` 即可查看导航界面。默认加载 `./resources/sample.json` 中的示例链接数据。替换为自定义资源文件后，页面将自动刷新。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | >= 18.0.0 | 运行时环境，用于执行构建与开发脚本 |
| npm | >= 9.0.0 | 包管理器，用于安装项目依赖 |
| Git | >= 2.30.0 | 版本控制，用于克隆仓库和管理配置变更 |
| 现代浏览器 | 最新两版 Chrome / Firefox / Edge | 用于访问渲染后的导航页面，支持 ES6 与 CSS Grid |
| 网络连通性 | 外网可访问 | 用于链接可用性检测时发起 HTTP 请求 |
| 磁盘空间 | >= 50 MB | 存放源码、依赖包及生成的静态页面 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | `/docs/user-guide/` | 如何添加、编辑、删除链接？如何查看可用性报告？如何自定义分类？ |
| 配置参考 | `/docs/configuration/` | 支持哪些配置文件格式？元数据字段如何定义？主题选项有哪些？ |
| 开发者指南 | `/docs/developer/` | 如何扩展检测器？如何替换渲染模板？如何编写自定义插件？ |
| 运维手册 | `/docs/operations/` | 如何部署到生产环境？如何设置定时检测任务？日志在哪里查看？ |
| API 文档 | `/docs/api/` | 提供了哪些 RESTful 接口？请求参数与响应格式是什么？ |

## 资源列表

### 足球赛事比分类

<code>zuqiubisaijieguo.net.cn</code>

<code>wangyitiyujishibifen.net.cn</code>

<code>jingcaizuqiubifen1.net.cn</code>

<code>jingcaizuqiubifenwang.org.cn</code>

<code>jingcaizuqiujishibifen.org.cn</code>

<code>jingcaibifenwang.org.cn</code>

<code>jingcaibifen.net.cn</code>

<code>zuqiubifenjingcai.org.cn</code>

<code>jingcaizuqiubisaijieguo.org.cn</code>

<code>jingcaizuqibifensaicheng.org.cn</code>

## 项目结构

```
hyperlink-navigator/
├── src/                           # 源码主目录
│   ├── core/                      # 核心逻辑模块
│   │   ├── linkParser.js          # 链接解析与标准化
│   │   ├── healthChecker.js       # HTTP 可用性检测
│   │   └── metadataValidator.js   # 元数据校验
│   ├── render/                    # 渲染引擎
│   │   ├── markdownRenderer.js    # Markdown -> HTML 转换
│   │   ├── themeManager.js        # 主题切换管理
│   │   └── templateEngine.js      # 模板编译
│   ├── cli/                       # 命令行工具
│   │   ├── import.js              # 批量导入命令
│   │   ├── export.js              # 导出报告命令
│   │   └── watch.js               # 监听模式
│   ├── adapters/                  # 数据格式适配器
│   │   ├── jsonAdapter.js         # JSON 读写
│   │   ├── csvAdapter.js          # CSV 解析
│   │   └── opmlAdapter.js         # OPML 订阅列表解析
│   └── server/                    # 开发服务器
│       ├── app.js                 # Express 应用入口
│       └── routes.js              # 路由定义
├── config/                        # 配置文件目录
│   ├── default.json               # 默认配置
│   ├── custom.json                # 用户自定义配置（不提交）
│   └── schema.json                # 配置 JSON Schema
├── resources/                     # 资源数据存储
│   ├── links/                     # 链接数据文件按批次存放
│   │   └── batch_122.json         # 第 122 批次资源
│   ├── reports/                   # 可用性报告输出目录
│   └── snapshots/                 # 历史快照
├── docs/                          # 文档目录
│   ├── user-guide/                # 用户手册
│   ├── developer/                 # 开发者指南
│   └── api/                       # API 参考
├── tests/                         # 单元测试与集成测试
│   ├── unit/                      # 单元测试
│   └── integration/               # 集成测试
├── public/                        # 静态资源输出目录
│   ├── css/                       # 样式文件
│   ├── js/                        # 前端脚本
│   └── images/                    # 图片资源
├── .github/                       # GitHub 工作流
│   └── workflows/                 # CI/CD 流水线
├── package.json                   # npm 依赖与脚本
├── README.md                      # 项目说明文档
└── LICENSE                        # MIT 许可证
```

## 贡献指南

1. 复刻仓库至个人账户，在本地创建功能分支（命名格式为 `feature/描述` 或 `fix/描述`），确保分支从最新的 main 分支切出。

2. 完成代码修改后，运行测试套件（`npm test`）确保所有用例通过，并补充新增功能的单元测试。若涉及资源数据变更，请使用 `npm run validate` 校验 JSON 格式是否正确。

3. 提交信息遵循 Conventional Commits 规范（如 `feat: 添加 OPML 导入支持`），提交前执行 `npm run lint` 检查代码风格。

4. 推送分支至远程仓库，发起 Pull Request 至主仓库的 main 分支，描述中说明改动原因、影响范围及测试情况。

5. 项目维护者将在 48 小时内进行 Code Review，必要时会提出修改意见。合并后您的贡献将出现在下一版本发布说明中。

## 常见问题

**Q: 链接可用性检测是否会误判临时性故障？**  
A: 系统默认对每个链接进行三次重试，每次重试间隔 2 秒，超时时间设置为 10 秒。若三次均失败才标记为不可用。同时支持配置 `retryCount` 和 `timeout` 参数以适配不同网络环境。

**Q: 如何管理成百上千条链接而不影响页面加载速度？**  
A: 系统采用按需渲染策略，默认仅渲染当前可视区域内的链接条目。同时支持分页加载和搜索过滤。对于超过 500 条的数据集，建议使用 `batchSize` 配置项分批加载，并启用静态缓存预生成 HTML。

**Q: 是否支持私有化部署且不依赖外部 CDN？**  
A: 完全支持。您可以将所有静态资源（包括 CSS、JavaScript 库）下载至 `public/vendor` 目录，并在配置中设置 `assets.cdn` 为 `local` 模式。系统将自动从本地路径加载所有依赖，无需访问公网。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
