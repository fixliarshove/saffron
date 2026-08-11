# TechLink Navigator

TechLink Navigator 是一个面向开发者与技术研究人员的开源技术资源外链聚合与导航系统。该项目定位于解决技术信息碎片化、优质资源分散、社区文档入口缺失等问题，通过人工筛选与社区贡献相结合的方式，构建一个高可用、可扩展的技术资源索引层。项目本身不存储任何第三方内容，仅提供结构化外链映射与状态监控能力，适用于个人技术收藏管理、团队文档入口标准化、以及开源社区外围资源整理等场景。

目标用户包括：需要系统化管理技术书签的开发者、希望降低团队新人上手成本的架构师、以及需要对外输出统一文档入口的开源项目维护者。通过 TechLink Navigator，用户可以在一处完成对多类技术资源（赛事信息、社区平台、数据查询、文档站点等）的集中查阅与状态追踪。

## 功能概览

- **多源外链统一收录**：支持将任意 HTTP/HTTPS 及裸域名资源录入系统，并按自定义分类标签进行组织，便于后续检索与维护。

- **资源可用性拨测**：内置简易 HTTP 状态检查模块，可定时检测已收录链接的可达性，并在状态变更时输出日志，辅助管理员发现失效资源。

- **标签与全文检索**：每个资源条目支持多个标签（如“体育数据”“社区论坛”“赛事直播”），并提供基于标题、描述、标签的轻量级全文搜索接口。

- **只读外链展示页**：生成纯静态的导航首页与分类页面，可直接部署至 Nginx、GitHub Pages 或任何静态托管服务，无需后端数据库即可访问。

- **导入与导出兼容性**：支持批量导入 CSV / JSON 格式的链接列表，同时支持将当前全部数据导出为标准书签 HTML 格式，便于迁移至浏览器或其他导航工具。

- **社区贡献工作流**：集成基于 Pull Request 的链接新增与更新流程，外部贡献者可通过修改数据目录下的 YAML 文件来提交新资源，经审核后合并。

- **访问量统计接口**：提供可选的匿名访问计数功能，帮助管理员了解高频资源入口，为链接排序与推荐提供数据参考。

## 应用场景

- **技术团队内部文档入口统一**：开发团队可将常用的 CI/CD 工具链、监控面板、日志系统、代码仓库等内部链接统一录入 TechLink Navigator，并部署在内网服务器上，替代浏览器混乱的书签栏。新人入职时仅需访问一个导航页即可找到所有必要系统入口。

- **开源项目周边资源整理**：开源项目维护者可以使用该项目整理与项目相关的论坛、赛事平台、数据提供方、镜像站等外部资源，放置于项目 README 或 Wiki 中，帮助社区成员快速定位生态内关键站点，减少重复提问。

- **技术资讯与活动追踪**：技术爱好者或社区运营人员可将多个赛事报名页面、活动日程表、成绩查询系统等时间敏感型资源集中收录，配合可用性拨测功能，在活动期间快速发现页面变更或宕机情况，及时通知参与者。

- **个人知识体系书签管理**：开发者可将长期积累的技术博客、在线课程、API 文档、规范标准等链接按主题分类整理，替代浏览器自带书签的扁平结构，并通过导出功能定期备份至本地或云端。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，需提前安装 Git 与 Node.js 18 以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/techlink-navigator/techlink-navigator.git
cd techlink-navigator

# 安装依赖（使用 npm）
npm install

# 复制示例配置文件并修改
cp .env.example .env

# 执行首次数据初始化与静态站点生成
npm run build

# 启动本地开发服务器，默认监听 3000 端口
npm start
```

访问 <code>http://localhost:3000</code> 即可浏览导航首页。若需要后台管理界面，请使用 <code>npm run admin</code> 启动管理面板（默认账户密码见 .env 文件说明）。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | 9.x 或 10.x | 包管理器，用于安装项目依赖 |
| Git | 2.30 及以上 | 版本控制工具，用于克隆仓库及贡献操作 |
| 内存 | 最低 512 MB，推荐 1 GB | 构建静态站点时内存占用随链接数量线性增长 |
| 磁盘空间 | 最低 200 MB | 包含依赖包与生成文件，建议预留 500 MB |
| 网络 | 可访问公网（可选） | 仅当需要使用拨测功能或远程数据源时需网络 |

## 文档导航

| 层面 | 目录 / 文档 | 回答的问题 |
|---|---|---|
| 用户入门 | <code>docs/quick-start.md</code> | 如何快速搭建并运行实例？如何添加第一批链接？ |
| 管理员指南 | <code>docs/admin-guide.md</code> | 如何配置自动拨测？如何管理标签体系？如何导入导出数据？ |
| 开发者文档 | <code>docs/development.md</code> | 项目目录结构说明，如何扩展新数据源？如何自定义主题？ |
| 贡献规范 | <code>CONTRIBUTING.md</code> | 提交链接的 YAML 格式要求，Pull Request 流程与审核标准 |

## 资源列表

### 体育赛事数据类

<code>lanqiubifeng.org.cn</code>

<code>lanqiubifenh.org.cn</code>

<code>zuqiubifenziboa.org.cn</code>

<code>zuqiubifenzibob.org.cn</code>

<code>zuqiubifenziboc.org.cn</code>

<code>zuqiubifenzibod.org.cn</code>

<code>zuqiubifenziboe.org.cn</code>

### 综合赛事与社区平台类

<code>ajiasaicheng.asia</code>

<code>bajiazhugongbang.asia</code>

<code>baxizuqiujiajiliansai.asia</code>

## 项目结构

```
techlink-navigator/
├── data/                           # 核心数据目录，所有链接以 YAML 形式存储
│   ├── sources/                    # 每个资源条目一个 .yaml 文件
│   │   ├── basketball/             # 篮球相关资源分类
│   │   │   ├── lanqiubifeng.yaml   # 对应 <code>lanqiubifeng.org.cn</code> 的元数据
│   │   │   └── lanqiubifenh.yaml   # 对应 <code>lanqiubifenh.org.cn</code> 的元数据
│   │   ├── football/               # 足球相关资源分类
│   │   │   ├── zuqiubifen_1.yaml   # 对应 zuqiubifenziboa ~ ziboc
│   │   │   ├── zuqiubifen_2.yaml   # 对应 zuqiubifenzibod ~ ziboe
│   │   │   └── baxizuqiu.yaml      # 对应 <code>baxizuqiujiajiliansai.asia</code>
│   │   └── asia_events/            # 亚洲地区赛事活动
│   │       ├── ajiasaicheng.yaml   # 对应 <code>ajiasaicheng.asia</code>
│   │       └── bajiazhugong.yaml   # 对应 <code>bajiazhugongbang.asia</code>
│   ├── tags.yaml                   # 全局标签定义与颜色映射
│   └── categories.yaml             # 分类层级结构配置
├── src/                            # 源代码目录
│   ├── core/                       # 核心逻辑模块：解析、校验、构建
│   │   ├── parser.js               # YAML 解析与校验器
│   │   ├── builder.js              # 静态页面生成引擎
│   │   └── health.js               # HTTP 状态拨测模块
│   ├── admin/                      # 管理后台 UI 组件（React）
│   │   ├── pages/                  # 后台页面视图
│   │   └── api/                    # 本地管理 API 路由
│   └── templates/                  # 前端展示模板（EJS）
│       ├── index.ejs               # 首页模板
│       ├── category.ejs            # 分类详情页模板
│       └── detail.ejs              # 单个链接详情页
├── public/                         # 静态资源输出目录（构建后）
│   ├── css/                        # 编译后的样式文件
│   ├── js/                         # 前端交互脚本
│   └── index.html                  # 生成的首页入口
├── tests/                          # 单元测试与集成测试
│   ├── parser.test.js
│   ├── builder.test.js
│   └── health.test.js
├── scripts/                        # 辅助运维脚本
│   ├── import-csv.js               # CSV 批量导入工具
│   └── export-html.js              # HTML 书签导出工具
├── .env.example                    # 环境变量模板（含管理员密钥配置）
├── .eslintrc.js                    # 代码规范配置
├── package.json                    # 项目依赖与脚本声明
├── README.md                       # 本文件
└── LICENSE                         # MIT 许可证文本
```

## 贡献指南

1.  **查阅现有议题与 Pull Request**：访问项目 GitHub Issues 页面，搜索是否已有关于您想新增的链接或功能的讨论。若无相关议题，请先新建一个 Issue 说明您要新增的资源类型与分类建议，避免重复劳动。

2.  **克隆代码并创建功能分支**：将主仓库 Fork 至个人账号，然后克隆到本地。请基于 <code>main</code> 分支创建新的功能分支，分支命名建议采用 <code>feat/add-resource-{name}</code> 或 <code>fix/health-check-{issue-id}</code> 格式。

3.  **按模板添加或修改数据文件**：在 <code>data/sources/</code> 下对应的分类子目录中，新建或编辑 YAML 文件。必须包含 <code>title</code>、<code>url</code>、<code>description</code>、<code>tags</code> 字段。请确保 URL 值与用户原始数据完全一致（不擅自添加协议或 www），并运行 <code>npm run validate</code> 校验数据格式。

4.  **本地构建与自测**：执行 <code>npm run build</code> 确认站点可正常生成，然后运行 <code>npm start</code> 访问本地预览。检查新增资源是否正确显示在分类页面，且链接跳转无误。

5.  **提交变更并发起 Pull Request**：提交代码并推送到您的远程 Fork 仓库，然后向主仓库的 <code>main</code> 分支发起 Pull Request。请清晰描述变更内容，并关联相关 Issue 编号。项目维护者将在 3 个工作日内审核，通过后即合并。

## 常见问题

**Q: 我添加的裸域名链接（如 <code>lanqiubifeng.org.cn</code>）在拨测中总是报告超时，该如何处理？**

A: 拨测模块默认使用 Node.js 的 <code>http</code> 和 <code>https</code> 模块尝试访问。对于裸域名，我们会依次尝试 http 和 https 协议。若超时，可能是目标服务器对非浏览器请求有限制或网络环境问题。您可以在 <code>.env</code> 中调整 <code>HEALTH_TIMEOUT</code> 参数（单位毫秒），或将该资源的 <code>health_check_enabled</code> 字段设为 <code>false</code> 以跳过拨测。同时，建议您在浏览器中手动验证该域名是否可正常访问。

**Q: 如何将我的现有浏览器书签批量导入 TechLink Navigator？**

A: 项目提供了导入脚本 <code>scripts/import-csv.js</code>。您需要先从浏览器导出书签为 HTML 文件，然后使用在线工具或脚本将 HTML 转换为 CSV 格式（列标题为：title, url, description, tags）。之后运行 <code>node scripts/import-csv.js ./path/to/bookmarks.csv</code>，脚本会自动根据 URL 域名归类到对应的分类子目录中。导入完成后请手动检查分类是否合理，并运行 <code>npm run build</code> 重新生成站点。

**Q: 静态站点生成后，是否可以增量更新而不用全量重建？**

A: 当前版本仅支持全量构建，因为链接数量通常在数百以内，全量构建耗时在 2 秒以内，性能开销可忽略。若您的实例包含数千条链接，建议使用 <code>--watch</code> 模式运行开发服务器，该模式会监听数据目录变更并自动执行增量式重新构建。生产环境部署仍推荐使用全量构建后上传静态文件，以确保一致性。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:37
