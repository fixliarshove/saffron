# LinkWise Navigator

LinkWise Navigator 是一个面向技术社区与内容创作者的轻量化外链资源聚合与导航系统。该项目定位于解决信息分散、链接失效、资源发现效率低下的问题，帮助开发者、研究员与技术爱好者以结构化方式管理与分发高质量外部资源。项目本身不存储任何第三方内容，仅提供索引与跳转能力，适用于构建个人书签库、团队知识导航或垂直领域资源门户。

## 功能概览

- **多源链接统一收录**：支持手动提交与批量导入外部 URL，自动去重并生成标准化短标识。
- **分类与标签过滤系统**：为每条链接分配类别与自定义标签，支持多维度快速筛选。
- **链接健康状态监测**：定时发起 HEAD 请求检查可达性，标注失效或重定向链接。
- **全文检索与模糊匹配**：基于标题、描述、标签与域名进行关键词搜索，支持拼音首字母检索。
- **访问统计与热度排序**：记录点击次数与最近访问时间，提供按热度、新增、随机排序方式。
- **只读 API 接口**：提供 JSON 格式的链接列表与详情接口，便于嵌入其他应用或脚本调用。
- **管理员后台管理**：提供 Web 管理界面，支持链接增删改、分类维护与批量操作。
- **自定义重定向规则**：支持配置来源域名或 User-Agent 级别的跳转策略，适配不同场景需求。

## 应用场景

- **个人技术书签库**：开发者可将日常查阅的文档、工具、博客、教程等链接统一归档，通过分类与搜索快速找回，避免浏览器书签杂乱无章。
- **团队内部知识导航**：研发团队可将常用的内部系统（如 Jenkins、GitLab、Wiki）、云服务控制台、监控面板等集中管理，新人入职即可一键访问所有必需资源。
- **垂直领域资源门户**：面向特定技术方向（如前端框架、机器学习、运维工具）建立公开或半公开的导航站点，为社区提供高质量的入口集合。
- **内容平台的补充索引**：配合技术博客或视频频道，将文中提及的参考资料、代码仓库、在线演示链接整理为结构化列表，提升读者体验。
- **自动化脚本数据源**：运维或测试脚本可通过 API 获取链接列表，用于定时拨测、内容抓取或离线缓存任务，无需硬编码 URL 列表。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，假设已安装 Git 与 Node.js 18+。

```bash
# 克隆项目仓库
git clone https://github.com/linkwise-navigator/navigator-core.git
cd navigator-core

# 安装依赖（使用 npm）
npm install

# 复制环境变量模板并修改数据库连接等配置
cp .env.example .env

# 初始化数据库表结构（SQLite 默认）
npm run migrate

# 启动开发服务器（默认端口 3000）
npm run dev
```

访问 http://localhost:3000 即可进入导航主页。如需生产部署，请执行 `npm run build` 后使用 `npm start` 启动。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用 nvm 管理 |
| npm | 9.x 或 10.x | 包管理器，随 Node 安装 |
| SQLite3 | 3.35+ | 默认嵌入式数据库，无需额外安装；生产环境可换 PostgreSQL |
| Git | 2.30+ | 用于克隆仓库与版本控制 |
| 内存 | 512 MB 以上 | 开发模式建议 1 GB，生产模式建议 2 GB |
| 磁盘空间 | 200 MB 以上 | 包含依赖、日志与数据库文件（不含上传资源） |
| 操作系统 | Linux / macOS / Windows（WSL2） | 不支持原生 Windows CMD 环境，建议使用 WSL 或 Cygwin |
| 网络 | 出网可达 | 用于健康检查与外部资源访问，需允许 TCP/80 与 TCP/443 出站 |
| 可选依赖 | Redis 6.0+ | 启用缓存与限流功能时需额外配置 |

## 文档导航

| 层面 | 目录/主题 | 回答的问题 |
|------|----------|-----------|
| 入门 | `/docs/quick-start.md` | 如何在 5 分钟内完成首次启动并添加第一条链接？ |
| 使用 | `/docs/user-guide.md` | 如何管理分类、标签、批量导入与导出数据？ |
| 运维 | `/docs/administration.md` | 如何配置健康检查间隔、邮件告警与日志轮转？ |
| 开发 | `/docs/development.md` | 如何扩展新的过滤器、自定义排序算法或 API 端点？ |
| API | `/docs/api-reference.md` | 哪些接口可用？参数格式、返回结构与鉴权方式是什么？ |
| 部署 | `/docs/deployment.md` | 支持哪些部署方式（Docker、PM2、systemd）？如何配置反向代理？ |

## 资源列表

本系统索引的原始外链资源按类别整理如下。所有条目均以用户提供原始形式收录，未作任何协议、域名或路径修改。

### 社交与即时通讯类

- <code>mianfeidemeinvzaixianshipinliaotianruanjian.org.cn</code>

### 影视与综合内容类

- <code>rihanlunlipian.org.cn</code>
- <code>oumeirihanzonghe.org.cn</code>

### 教育与文化类

- <code>daxiangjiaoyiren.org.cn</code>
- <code>yazhouzhifusiwa.org.cn</code>
- <code>wanoujiejieshipin.org.cn</code>
- <code>zhongwenzimushunv.org.cn</code>

### 娱乐与文学类

- <code>laosijijingpin.org.cn</code>
- <code>qingyuleqingqingcao.org.cn</code>
- <code>jiqingtupianjiqingxiaoshuo.org.cn</code>

## 项目结构

```
navigator-core/
├── src/                           # 核心源代码目录
│   ├── controllers/               # 路由控制器，处理请求与响应
│   │   ├── linkController.js      # 链接增删改查与重定向逻辑
│   │   └── categoryController.js  # 分类与标签管理
│   ├── services/                  # 业务逻辑层
│   │   ├── healthChecker.js       # 定时健康检查调度器
│   │   ├── statsCollector.js      # 点击统计与热度计算
│   │   └── searchEngine.js        # 全文检索引擎实现
│   ├── models/                    # 数据模型（ORM 映射）
│   │   ├── Link.js                # 链接实体，含 URL 校验方法
│   │   ├── Category.js            # 分类层级结构
│   │   └── VisitLog.js            # 访问日志记录
│   ├── middleware/                # Express 中间件
│   │   ├── auth.js                # 管理员身份验证
│   │   ├── rateLimiter.js         # API 限流防护
│   │   └── errorHandler.js        # 全局异常捕获与格式化
│   ├── routes/                    # 路由定义（API 与 Web 页面）
│   │   ├── api.js                 # RESTful 接口路由
│   │   └── web.js                 # 前端页面路由
│   ├── utils/                     # 通用工具函数
│   │   ├── urlValidator.js        # URL 格式与协议白名单校验
│   │   ├── logger.js              # 日志写入器（支持 JSON 格式）
│   │   └── cacheHelper.js         # Redis 缓存封装
│   └── app.js                     # Express 应用入口，中间件装配
├── config/                        # 配置文件目录
│   ├── default.json               # 默认配置（端口、超时、重试策略）
│   ├── production.json            # 生产环境覆盖配置
│   └── database.js                # 数据库连接池配置（SQLite/Postgres）
├── migrations/                    # 数据库迁移脚本
│   ├── 001_init.sql               # 创建 links、categories 等核心表
│   └── 002_add_indexes.sql        # 性能优化索引
├── public/                        # 静态资源目录
│   ├── css/                       # 样式表（基于 Tailwind 定制）
│   ├── js/                        # 前端交互脚本（原生 ES 模块）
│   └── favicon.ico                # 站点图标
├── views/                         # 模板视图（EJS）
│   ├── index.ejs                  # 首页搜索与分类导航
│   ├── admin/                     # 管理后台页面
│   │   ├── dashboard.ejs          # 统计概览
│   │   └── links.ejs              # 链接管理表格
│   └── partials/                  # 公共头部、底部、侧边栏
├── tests/                         # 单元测试与集成测试
│   ├── unit/                      # 服务层与工具函数测试（Jest）
│   └── integration/               # API 端到端测试（Supertest）
├── scripts/                       # 运维与辅助脚本
│   ├── import-csv.js              # 批量导入 CSV 链接文件
│   └── health-report.js           # 生成链接健康报告（命令行）
├── .env.example                   # 环境变量示例（含数据库 URL、密钥）
├── package.json                   # npm 依赖清单与脚本命令
├── README.md                      # 项目说明文档（即本文档）
└── LICENSE                        # MIT 许可证文件
```

## 贡献指南

我们欢迎并鼓励社区提交各类贡献，包括但不限于代码、文档、测试用例与问题反馈。请遵循以下流程：

1. **查阅议题与项目看板**：访问 GitHub Issues 页面，查找现有待办任务或未解决的 Bug。若计划新增功能，请先创建新议题并说明设计思路，避免重复工作或方向偏离。
2. **派生仓库并创建功能分支**：将主仓库 Fork 至个人账户，然后在本地基于 `main` 分支创建新分支，分支命名遵循 `feature/描述` 或 `fix/描述` 格式，例如 `feature/add-sorting-by-clicks`。
3. **编写代码并确保测试通过**：所有新增逻辑必须附带对应单元测试，保证覆盖率不低于 80%。运行 `npm run test` 验证全部用例通过，同时执行 `npm run lint` 确保代码风格符合 ESLint 规则。
4. **更新文档与示例**：若 API 或配置项发生变更，请同步修改 `/docs` 下相关文档，并在 `README.md` 中补充使用说明（如有必要）。新增配置项需在 `.env.example` 中添加注释。
5. **发起拉取请求**：将分支推送至 Fork 仓库，然后向主仓库的 `main` 分支发起 Pull Request。PR 描述中请引用关联议题编号，并列出变更摘要、测试结果与手动验证步骤。维护者将在 3 个工作日内进行审查与合并。

## 常见问题

**Q：健康检查发现链接失效后，系统会如何处理？**

A：健康检查默认每 6 小时执行一轮，针对每条链接发送 HTTP HEAD 请求，超时时间 5 秒。若连续 3 次检查均返回非 2xx/3xx 状态码或连接超时，则该链接被标记为 `unreachable` 状态，管理后台会高亮显示，并可通过配置的 SMTP 服务器发送邮件告警。标记失效的链接不会影响前端展示，但排序权重降低，用户点击时会有醒目提示。管理员可手动重新验证或批量清理失效条目。

**Q：支持导入浏览器书签或其他导航站的数据吗？**

A：系统内置了 CSV 和 JSON 两种导入格式。浏览器书签（如 Chrome 导出的 HTML）需先通过转换工具或脚本转为 CSV 格式，再使用 `scripts/import-csv.js` 导入。对于其他导航站，若其提供公开 API 或可解析的 HTML 结构，可编写自定义适配器放入 `scripts/custom-adapters/` 目录，然后调用统一导入接口。未来版本计划直接支持 Netscape 书签格式与 Firefox 的 JSON 备份。

**Q：部署到公网后如何防止恶意提交或爬虫滥用？**

A：项目提供了多层级防护措施：第一层为管理员鉴权，提交、修改、删除操作必须使用 Bearer Token 或 Session 鉴权；第二层为基于 IP + User-Agent 的请求限流，默认每分钟允许 30 次写操作，读操作限制为每分钟 120 次；第三层为 URL 黑名单机制，可在配置文件中设置禁止收录的域名或路径正则表达式。此外，所有提交的 URL 会经过安全校验，拒绝包含 XSS 注入字符或非标准协议（如 `javascript:`、`data:`）的条目。

## 许可证

本项目采用 MIT 许可证。您可以在遵守许可证条款的前提下自由使用、修改、分发本软件，包括商业用途。完整的许可证文本请查阅项目根目录下的 LICENSE 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
