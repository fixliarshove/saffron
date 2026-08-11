# ResourceHub

ResourceHub 是一个面向技术内容创作者与网站运营者的外链资源导航与信息汇总平台。本项目定位于系统化收集、分类与展示特定垂直领域内的可访问网络资源，帮助开发者、研究人员与内容编辑快速定位具备参考价值的站点集合。项目本身不产生或存储任何第三方数据，仅提供结构化的外链索引服务，通过自动化的可用性检测与元信息提取辅助用户进行资源筛选与评估。

## 功能概览

- **资源分类索引** 根据主题、域名后缀与内容特征对收录资源进行多级分类，支持按类别快速筛选。
- **外链可用性监测** 每日定时检测所有收录站点的 HTTP 状态码与响应时间，标记异常链接。
- **元信息自动提取** 获取目标站点的页面标题、关键词描述与服务器类型，丰富索引内容。
- **自定义标签系统** 允许用户为资源添加自定义标签，构建个性化分类维度。
- **全文搜索支持** 基于标题、描述、标签和域名关键词提供轻量级全文检索引擎。
- **资源变更历史记录** 记录每个站点标题、描述或可用性状态的变动轨迹，便于追溯。
- **RSS 订阅源生成** 为每个分类或标签生成独立的 RSS 订阅地址，方便外部订阅。
- **数据导入导出** 支持 JSON 与 CSV 格式的资源列表批量导入与导出，便于迁移与备份。

## 应用场景

- **技术文档站点外部链接管理** 技术博客或文档站点维护者可使用 ResourceHub 管理文末参考链接或推荐资源板块，确保引用资源的长期可用性。
- **垂直领域研究数据采集** 社会文化、语言学或区域研究方向的学者可通过本平台快速获取一批主题相关的可访问站点，作为研究样本池。
- **内容聚合站点的源列表维护** 内容聚合平台或导航站运营者可以利用 ResourceHub 的分类与标签功能构建自身的对外推荐资源库。
- **运维监控的补充探测节点** 系统运维人员可配置 ResourceHub 的可用性检测结果作为现有监控体系的补充数据源，用于判断特定网络区域的访问质量。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境，需预先安装 Git 与 Node.js（版本 >= 18.0）。

```bash
# 克隆项目仓库
git clone https://github.com/resourcehub/resourcehub.git

# 进入项目目录
cd resourcehub

# 安装依赖（使用 npm）
npm install

# 复制环境配置文件模板
cp .env.example .env

# 执行数据库初始化与资源索引构建
npm run setup

# 启动开发服务器（默认监听 3000 端口）
npm run dev
```

启动成功后，在浏览器中访问 http://localhost:3000 即可查看本地运行的 ResourceHub 实例。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | >= 18.0.0 | 运行时环境，需包含 npm 或 yarn 包管理器 |
| PostgreSQL | >= 14.0 | 主数据库，用于存储资源元信息、标签与历史记录 |
| Redis | >= 6.2 | 缓存层，用于加速搜索与可用性检测结果读取 |
| Git | >= 2.30 | 用于克隆仓库及后续版本更新 |
| Nginx | >= 1.20（生产环境推荐） | 反向代理与静态资源缓存加速 |
| PM2 | 最新稳定版（生产环境推荐） | Node.js 进程守护与自动重启管理 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | /docs/getting-started.md | 如何快速部署开发环境及首次启动流程 |
| 配置说明 | /docs/configuration.md | 环境变量含义、数据库连接参数与自定义分类规则 |
| API 参考 | /docs/api-reference.md | 所有 RESTful API 端点说明，包括请求参数与响应结构 |
| 运维部署 | /docs/deployment.md | 生产环境 Nginx 配置、SSL 证书绑定与 PM2 启动脚本 |

## 资源列表

### 综合类别

<code>zhongwenrenqi.org.cn</code>

<code>renqishaofu.org.cn</code>

<code>rihanlunli.org.cn</code>

### 媒体与视频相关

<code>bajiaoshipinapp.org.cn</code>

### 文字与内容类

<code>zhongwenzimusiwa.org.cn</code>

### 特色主题

<code>renqiyouma.org.cn</code>

<code>xiaodiaowang.org.cn</code>

<code>chengrenjingpin18.org.cn</code>

<code>guoyuav.org.cn</code>

<code>jiujiurenqi.org.cn</code>

## 项目结构

```
resourcehub/
├── src/
│   ├── core/                     # 核心应用逻辑与初始化
│   │   ├── app.js                # Express 应用实例创建与中间件注册
│   │   └── bootstrap.js          # 数据库连接、缓存初始化与定时任务启动
│   ├── routes/                   # 路由层，按功能模块划分
│   │   ├── index.js              # 基础首页与健康检查路由
│   │   ├── resources.js          # 资源增删改查及搜索路由
│   │   ├── categories.js         # 分类与标签管理路由
│   │   └── monitor.js            # 可用性检测状态查询路由
│   ├── services/                 # 业务服务层
│   │   ├── fetcher.js            # 外链元信息抓取与解析服务
│   │   ├── checker.js            # 可用性检测与响应时间记录服务
│   │   └── search.js             # 全文索引构建与查询服务
│   ├── models/                   # 数据模型层（ORM 映射）
│   │   ├── Resource.js           # 资源主表模型
│   │   ├── Tag.js                # 标签模型与多对多关联
│   │   └── History.js            # 变更历史记录模型
│   ├── workers/                  # 后台任务队列
│   │   ├── daily-check.js        # 每日定时可用性检测任务
│   │   └── meta-update.js        # 元信息增量更新任务
│   └── utils/                    # 通用工具函数
│       ├── logger.js             # 统一日志输出配置
│       └── validator.js          # URL 校验与规范化工具
├── config/                       # 配置文件目录
│   ├── default.json              # 默认配置（端口、超时、并发数）
│   └── production.json           # 生产环境覆盖配置
├── migrations/                   # 数据库迁移脚本
│   ├── 001_init.sql              # 初始化建表语句
│   └── 002_add_index.sql         # 索引优化与外键约束
├── tests/                        # 单元测试与集成测试
│   ├── unit/                     # 单测用例
│   └── integration/              # API 集成测试
├── .env.example                  # 环境变量模板文件
├── package.json                  # 项目依赖清单与脚本定义
└── README.md                     # 本文件
```

## 贡献指南

1. 在 GitHub 上 fork 本仓库至个人账号，并 clone 到本地开发环境。请确保在新建分支上开展工作，分支命名建议采用 `feature/功能简述` 或 `fix/问题简述` 格式。
2. 完成代码修改后，请确保所有现有单元测试通过，并为新增功能补充对应的测试用例。测试命令为 `npm test`，覆盖率检查命令为 `npm run test:coverage`。
3. 提交前运行 `npm run lint` 与 `npm run format` 对代码风格进行自动检查与修复，项目使用 ESLint + Prettier 统一规范。
4. 发起 Pull Request 至主仓库的 `main` 分支，PR 描述中请清晰说明改动目的、实现方式与测试结果。至少需要一名项目维护者进行 Code Review。
5. 若涉及资源列表的增删或分类调整，请同时更新 `data/` 目录下的示例数据集，并运行 `npm run validate-data` 验证数据格式合法性。

## 常见问题

**Q: 可用性检测出现大量超时或失败，可能是什么原因？**

A: 首先检查本机网络环境，确认能够正常访问外网。其次，目标站点可能设置了反爬策略或防火墙，建议调整 `config/default.json` 中的 `checker.timeout` 和 `checker.userAgent` 参数。如果失败率持续高于 20%，可能是目标域名集体不可达，请关注项目公告或更新检测代理配置。

**Q: 如何导入我自己的资源列表？**

A: 项目支持通过管理后台的导入功能上传 JSON 或 CSV 文件。JSON 格式需包含 `url`、`title`、`category` 字段，CSV 文件需包含表头行。导入前请运行 `npm run validate-import` 进行格式预检验。批量导入超过 1000 条记录时，建议使用命令行工具 `node scripts/import.js --file /path/to/data.json` 以规避 HTTP 超时限制。

**Q: 搜索功能无法匹配我预期的结果，如何调整？**

A: 搜索服务默认基于标题与描述字段进行分词匹配，权重偏向标题。如需调整搜索权重或添加自定义停用词，请编辑 `config/default.json` 中的 `search.weights` 与 `search.stopwords` 数组。修改后需重启服务并执行 `npm run rebuild-index` 重新构建索引。

## 许可证

MIT License. See the [LICENSE](./LICENSE) file for details.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:31
