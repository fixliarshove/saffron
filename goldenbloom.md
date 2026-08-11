# HyperLink Hub

HyperLink Hub 是一个面向开发者、技术研究人员与内容策展人的轻量级外链资源汇总平台。该项目定位于解决信息碎片化时代下高质量技术资源分散、检索成本高、更新不及时等问题，通过对特定领域外链进行结构化组织与版本化归档，帮助用户以可复现、可追踪的方式获取和共享精选网络资源。目标用户包括开源项目维护者、数据采集工程师、SEO 研究人员以及关注特定内容领域的普通用户。

HyperLink Hub 本身不生产内容，也不对目标链接的内容负责，而是提供一套标准化的资源索引框架与自动化更新机制，使外链管理如同代码版本管理一般清晰可控。项目内核采用纯静态生成方式，可托管于任何支持 HTTP 服务的环境，既适合个人本地使用，也支持团队协同维护。

## 功能概览

- **多维度资源索引**：支持按内容地域、语言、主题类别等维度对链接进行标记与筛选，内置标签系统便于快速定位。
- **自动化状态检查**：集成链接存活检测脚本，可定时验证资源可访问性，并输出状态报告。
- **版本化归档**：基于 Git 提交历史记录每次资源变更，支持回退至任意历史状态。
- **静态站点生成**：内置模板引擎可将资源数据渲染为 HTML 页面，无需后端服务即可访问。
- **批量导入导出**：支持 CSV 与 JSON 格式的链接批量导入导出，便于与其他工具链集成。
- **外链关系图**：生成资源间引用关系的可视化图谱，辅助分析资源网络结构。
- **自定义元数据扩展**：允许为每个链接附加自定义键值对元数据，满足个性化分类需求。
- **访问统计摘要**：记录各链接被引用或访问的频次，提供简单的热度排序功能。

## 应用场景

- **技术文献综述**：研究人员在开展文献调研时，可通过 HyperLink Hub 将分散于不同网站的技术博客、论文预印本、代码仓库链接统一收藏，并添加阅读笔记与重要性标签，构建个人知识库。
- **数据采集管道配置**：数据工程师在构建网络爬虫时，可将目标数据源链接通过本项目进行集中管理，结合状态检查功能及时发现失效源，避免采集任务异常中断。
- **内容合规审查辅助**：内容审核人员可利用项目的标签与注释功能对特定类别的外链进行分类标注，生成审查清单，配合自动状态检测提高审核效率。
- **开源项目推荐列表维护**：开源社区维护者可使用本项目管理社区推荐的工具、库或学习资源，通过版本化功能记录每次增删改的决策背景，增强社区透明度。

## 快速开始

以下步骤适用于 Linux 及 macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 1. 克隆代码仓库
git clone https://github.com/hyperlink-hub/hyperlink-hub.git
cd hyperlink-hub

# 2. 安装依赖（使用 pip 和 npm）
pip install -r requirements.txt
npm install --global gatsby-cli

# 3. 初始化资源数据库
python scripts/init_db.py --seed data/seed_links.json

# 4. 执行本地预览
gatsby develop

# 5. 构建静态站点
gatsby build
```

完成上述步骤后，访问本地 8000 端口即可浏览资源面板。如需自定义资源列表，可直接编辑 `data/links.json` 文件或使用 `scripts/import_csv.py` 导入外部数据。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 用于运行链接状态检查脚本及数据处理工具 |
| Node.js | 18.x LTS 或 20.x | Gatsby 框架运行环境，用于静态站点生成 |
| Git | 2.30 及以上 | 版本控制，用于记录资源变更历史 |
| SQLite | 3.35 及以上 | 本地轻量级数据库，存储链接元数据及状态记录 |
| Gatsby CLI | 5.0 及以上 | 通过 npm 全局安装，用于构建与开发服务器 |
| pip | 22.0 及以上 | Python 包管理工具，用于安装 requests、pandas 等依赖库 |
| curl | 7.68 及以上 | 部分自动化脚本依赖 curl 进行网络探测 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户入门 | docs/getting-started.md | 如何安装、配置并运行首个资源索引实例？ |
| 数据管理 | docs/data-format.md | 链接的 JSON 结构定义、字段含义及扩展方式是什么？ |
| 运维部署 | docs/deployment.md | 如何将生成的站点部署到生产环境（Nginx、S3、Vercel）？ |
| 开发贡献 | docs/contributing.md | 代码规范、测试流程及 PR 提交要求有哪些？ |
| 接口说明 | docs/api-reference.md | 内部脚本与数据接口的函数签名及调用示例是什么？ |

## 资源列表

以下为当前版本收录的外部资源链接，按域名类别分组。所有链接均保持用户提供时的原始格式，未做任何协议或主机名改写。

内容类别一：国内精选相关

<code>guochanjingpinyiren.org.cn</code>

<code>hongguochengrenban.org.cn</code>

<code>guochanyirenjiujiu.org.cn</code>

内容类别二：综合文化相关

<code>wuyeshuangshuang.org.cn</code>

<code>wuyuetianyiquerqu.org.cn</code>

内容类别三：动态影像与图谱相关

<code>xieedongtaitu.org.cn</code>

内容类别四：海外及区域内容

<code>oumeirihanchengren.org.cn</code>

<code>rihanrenqizhongwenzimu.org.cn</code>

内容类别五：其他独立站点

<code>jiujiutiantang.org.cn</code>

<code>jingpinneishe.org.cn</code>

## 项目结构

```
hyperlink-hub/
├── data/                                 # 数据存储目录
│   ├── links.json                        # 主链接资源索引文件
│   ├── tags.json                         # 标签体系定义
│   └── seed_links.json                   # 初始种子数据用于首次初始化
├── scripts/                              # 工具脚本集合
│   ├── check_health.py                   # 批量检测链接存活状态
│   ├── init_db.py                        # 初始化 SQLite 数据库表结构
│   ├── import_csv.py                     # 从 CSV 导入链接数据
│   └── export_json.py                    # 导出当前数据为 JSON 格式
├── src/                                  # Gatsby 前端源码
│   ├── pages/                            # 路由页面组件
│   │   ├── index.js                      # 首页资源列表展示
│   │   └── detail.js                     # 单条链接详情页
│   ├── components/                       # 可复用 UI 组件
│   │   ├── LinkTable.jsx                 # 链接表格渲染组件
│   │   └── StatusBadge.jsx               # 状态标识徽章组件
│   └── templates/                        # 页面模板
│       └── category.js                   # 按类别筛选的模板页
├── tests/                                # 单元测试与集成测试
│   ├── test_check_health.py              # 健康检查脚本测试
│   └── test_data_loader.py               # 数据加载函数测试
├── docs/                                 # 用户与开发者文档
│   ├── getting-started.md                # 快速入门指南
│   ├── data-format.md                    # 数据格式规范
│   └── contributing.md                   # 贡献者操作手册
├── .github/                              # GitHub 工作流配置
│   └── workflows/
│       └── ci.yml                        # 持续集成流水线配置
├── requirements.txt                      # Python 依赖清单
├── package.json                          # Node.js 依赖及脚本定义
├── gatsby-config.js                      # Gatsby 站点配置文件
└── README.md                             # 项目说明文档（即本文档）
```

## 贡献指南

1. 将本仓库复刻至个人账户，在复刻版本中创建以 `feature/` 或 `fix/` 为前缀的功能分支进行开发。所有分支需从最新的 `main` 分支切出。
2. 新增或修改资源链接时，请严格遵循 `data/links.json` 中定义的 JSON Schema 格式，确保包含 `id`、`url`、`title`、`category`、`tags`、`status` 等必需字段，并编写至少一条注释说明添加理由。
3. 提交代码前执行 `scripts/check_health.py` 确保所有新增链接可正常访问，并运行 `pytest tests/` 通过全部单元测试。若链接为临时性资源，需在 `expiry_date` 字段中标注预计失效时间。
4. 发起 Pull Request 时，在描述中清晰列明本次变更涉及的新增链接、修改链接或删除链接，并关联相关 Issue 编号（如有）。PR 需要至少一位项目维护者审核通过后方可合并。
5. 文档类修改（包括 README、docs 目录下的 Markdown 文件）无需通过测试流水线，但需确保语法正确且无错别字。非英语文档需在文件名中标注语言后缀。

## 常见问题

**问：项目中的链接状态检测机制是否会对目标服务器造成负载压力？**

答：状态检测脚本默认采用单线程顺序请求，且每次请求间设置至少 500 毫秒的延迟间隔。检测频率由用户通过 crontab 或定时任务自行控制，项目推荐的最小检测间隔为 12 小时。对于批量检测场景，建议在非高峰时段执行。脚本内部使用 HTTP HEAD 方法优先，仅当 HEAD 不被支持时降级为 GET 并限定响应体大小为 256KB，从而最大程度减少带宽消耗。

**问：如何迁移已存在的浏览器书签或其它格式的链接收藏到本项目？**

答：项目提供 `scripts/import_csv.py` 脚本，支持从 CSV 文件导入。用户只需将书签导出为 CSV 格式（包含标题和 URL 列），然后运行导入命令即可自动转换为内部 JSON 格式。对于浏览器 HTML 书签文件，建议先使用在线转换工具或 Python 的 `beautifulsoup4` 库解析为 CSV 后再行导入。若存在大量重复链接，导入脚本会自动去重并输出警告日志。

**问：静态站点生成后，资源列表更新是否需要重新构建整个站点？**

答：是的，由于本项目采用静态生成策略，任何资源数据的变更（包括新增、修改、删除链接）都需要执行 `gatsby build` 重新生成 HTML 文件。为简化更新流程，项目在 `package.json` 中预置了 `npm run update-and-build` 命令，该命令会先拉取最新数据、运行状态检测、再触发构建，实现一步到位。对于频繁更新的场景，建议配合 CI/CD 服务（如 GitHub Actions）实现定时自动构建与部署。

## 许可证

本项目采用 MIT 许可证授权。任何个人或组织均可自由使用、复制、修改、合并、发布、分发、再许可及销售本软件的副本，但需在软件及所有相关副本中保留原始版权声明和许可声明。本软件按“现状”提供，不提供任何明示或暗示的担保，包括但不限于适销性、特定用途适用性和非侵权性担保。有关完整条款，请参阅项目根目录下的 LICENSE 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
