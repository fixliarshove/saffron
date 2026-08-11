# NexusLink 技术导航站

NexusLink 是一个面向开发人员、技术研究人员和互联网信息分析者的高密度外链资源汇总平台。该项目不生产内容，不存储任何媒体文件，仅提供结构化、分类清晰的互联网公开资源入口，帮助用户快速定位特定领域的信息节点。

本项目的目标用户包括自动化脚本编写者、网络拓扑研究人员、内容聚合系统开发者以及需要批量获取公开域名样本的数据分析人员。通过集中管理并定期校验这些资源入口的有效性，NexusLink 降低了人工检索和手工整理的时间成本，同时提供标准化的输出格式便于二次开发集成。

## 功能概览

- **按领域分类的资源索引**：将收集到的公开入口按内容主题划分为视频、文学、综合门户等类别，每一条记录均附带原始来源标注。

- **自动化可用性检测**：内置轻量级检测模块，可对收录的每条链接进行基础可达性测试，并在管理后台标注状态。

- **批量导出与结构化输出**：支持将整个资源列表导出为 JSON、CSV 或纯文本格式，方便下游系统批量处理。

- **变更历史追踪**：记录每次资源列表的增删改操作，支持回滚至任意历史版本，确保数据变更可追溯。

- **自定义标签系统**：允许用户为每条链接添加自定义标签（如“高延迟”、“备用节点”、“移动端适配”），实现个性化分类。

- **外部元数据富化**：对部分资源入口自动补充 WHOIS 信息、ICP 备案状态和 DNS 解析记录，提供更丰富的诊断参考。

- **只读镜像部署模式**：支持生成完全静态化的只读镜像站点，满足内网部署或离线查阅需求。

## 应用场景

1. **数据采集系统种子列表**：数据采集工程师可将本项目的资源列表作为初始种子集合，用于构建分布式爬虫的任务队列，省去手动收集起始 URL 的繁琐步骤。

2. **网络边界探测与可用性监控**：网络运维人员可利用本项目的导出接口，将链接列表导入外部监控系统，定期检测各地域节点的连通性与响应时间变化。

3. **内容分类模型训练样本标注**：自然语言处理研究人员可将这些资源入口按类别作为正负样本的候选源，用于训练网页分类器或主题识别模型。

4. **合规审计与域名备案核查**：法务或合规人员可依据本项目的备案信息补充功能，快速复核所涉域名是否具备合法运营资质，生成初步审计报告。

5. **个人技术研究实验环境搭建**：开发者在搭建私有搜索引擎或推荐系统原型时，可将本项目作为测试数据源，验证索引算法和排序策略的有效性。

## 快速开始

以下命令适用于 Linux/macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/nexuslink-io/nexuslink-station.git
cd nexuslink-station

# 2. 安装依赖（项目基于 Python 3.10+ 构建）
pip install -r requirements.txt

# 3. 初始化本地数据库并导入基础资源列表
python manage.py migrate
python manage.py import-seeds --source data/seeds_17th_batch.json

# 4. 启动本地开发服务器
python manage.py runserver --host 0.0.0.0 --port 8080

# 5. 执行一次全量可用性检测（可选）
python manage.py health-check --timeout 5 --retries 2
```

访问 http://localhost:8080 即可查看本地实例的资源导航界面。生产环境部署请参考 `docs/deployment.md`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 或更高 | 核心运行环境，低于此版本将导致异步 I/O 模块异常 |
| SQLite | 3.35.0+ | 默认内置数据库，用于存储资源条目和变更日志；生产环境可切换至 PostgreSQL |
| pip | 22.0+ | Python 包管理工具，用于安装 requirements.txt 中列出的所有依赖 |
| Git | 2.25+ | 用于克隆仓库和管理版本，非运行强制要求，但建议保留 |
| 网络连接 | 出方向 80/443 可达 | 用于执行可用性检测和 WHOIS 查询，内网部署可关闭此功能 |
| 系统时区 | UTC+8 或 UTC | 用于时间戳记录，建议与运维监控系统保持同一时区 |
| 磁盘空间 | 至少 200 MB | 用于存放数据库文件、日志和临时缓存，实际占用随条目数线性增长 |
| 内存 | 512 MB 以上 | 运行检测任务时若并发数过高需适当增加内存，建议生产环境不低于 1 GB |

## 文档导航

| 层面 | 目录文件 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user-guide.md` | 如何使用导航界面、如何搜索和筛选资源、如何导出列表 |
| 管理员手册 | `docs/admin-guide.md` | 如何添加/删除/编辑资源条目、如何查看变更历史、如何触发健康检测 |
| 开发指南 | `docs/development.md` | 如何扩展新的元数据富化插件、如何修改导出格式、如何编写单元测试 |
| API 参考 | `docs/api-reference.md` | 所有 RESTful 接口的请求参数、响应格式和错误码说明 |
| 部署运维 | `docs/deployment.md` | 生产环境下的 Nginx 反向代理配置、SSL 证书安装、PostgreSQL 迁移步骤 |
| 架构设计 | `docs/architecture.md` | 系统模块划分、数据流图、扩展性设计及性能优化建议 |
| 常见问题 | `docs/faq.md` | 补充性的问题排查指南，涵盖端口占用、权限错误和数据库锁等问题 |

## 资源列表

### 视频服务类

- <code>yiquzaixianshipin.org.cn</code>
- <code>yazhouzaixianyiqu.org.cn</code>
- <code>ririyeyejingpin.org.cn</code>

### 综合门户与文学类

- <code>jiujiuyazhoutiantang.org.cn</code>
- <code>shufudeweidao.org.cn</code>
- <code>wumatiantang.org.cn</code>
- <code>jiujiujire.org.cn</code>
- <code>madoutianmei.org.cn</code>

### 专业垂直类

- <code>langrenganzonghewang.org.cn</code>
- <code>zhongchuwuma.org.cn</code>

## 项目结构

```
nexuslink-station/
├── manage.py                 # 项目统一管理入口（启动、迁移、检测）
├── requirements.txt          # Python 依赖列表（Flask、requests、whois 等）
├── config/
│   ├── settings.py           # 全局配置（端口、数据库路径、超时阈值）
│   ├── logging.conf          # 日志格式与输出级别配置
│   └── seeds.json            # 静态种子资源备份文件
├── core/
│   ├── __init__.py
│   ├── database.py           # SQLite/PostgreSQL 连接池与 ORM 基类
│   ├── models.py             # 资源条目、标签、变更日志的数据模型定义
│   └── validators.py         # 域名格式校验、协议校验、黑名单过滤
├── modules/
│   ├── health_check/         # 可用性检测子模块（异步并发 + 超时重试）
│   ├── enricher/             # 元数据富化子模块（WHOIS、DNS、备案）
│   ├── exporter/             # 导出子模块（JSON、CSV、纯文本格式器）
│   └── watcher/              # 变更追踪子模块（diff 计算与历史回滚）
├── web/
│   ├── routes/               # Flask 路由定义（首页、详情、管理、API）
│   ├── templates/            # Jinja2 模板文件（导航页、详情页、管理面板）
│   └── static/               # CSS、JavaScript、字体等静态资源
├── tests/
│   ├── unit/                 # 单元测试（模型、验证器、富化函数）
│   └── integration/          # 集成测试（API 端点、数据库迁移）
├── scripts/
│   ├── bootstrap.sh          # 新环境一键初始化脚本
│   └── cron_daily.sh         # 每日定时任务（自动检测 + 报表生成）
└── docs/                     # 全部文档（用户手册、API 参考、部署指南）
```

## 贡献指南

1. **提交资源新增或变更请求**：通过 GitHub Issues 提交新链接建议时，请附上该链接的简要描述、所属类别以及可访问性证据（如 curl 响应截图）。核心维护者将在 48 小时内审核并合并。

2. **完善文档或修复已知错误**：Fork 本仓库后，在本地分支进行修改，确保所有单元测试通过，然后提交 Pull Request。PR 描述中请明确引用相关 Issue 编号，并说明测试覆盖情况。

3. **参与健康检测模块优化**：若您对异步并发、超时控制或代理轮转有丰富经验，欢迎改进 `modules/health_check` 下的检测调度逻辑。提交前请确保新增代码符合 PEP 8 规范，并补充对应的单元测试用例。

4. **增加新的元数据富化源**：如需接入新的外部 API（如 IP 归属地查询、SSL 证书信息提取），请在 `modules/enricher` 下新建独立的插件文件，并实现统一的 `enrich(domain)` 接口。提交时需附带模拟 API 响应的测试桩。

5. **反馈部署或运行问题**：若在 Windows 或 ARM 架构下遇到兼容性问题，请详细描述操作系统版本、Python 发行版及完整的错误堆栈，以便维护团队进行针对性适配。

## 常见问题

**Q: 为什么某些链接在健康检测中显示为不可达，但仍然保留在列表中？**

A: 本项目保持“收录即保留”原则，不会因单次检测失败而自动删除任何条目。检测结果仅作为辅助参考标记在后台，最终是否保留由管理员或数据使用者自行判断。部分节点可能存在地域性访问限制或临时维护，建议从多个网络出口进行交叉验证。

**Q: 项目是否提供 API 接口供外部程序调用？**

A: 是的。项目在启动后默认提供 RESTful API 接口，基础路径为 `/api/v1/`。您可以通过 `/api/v1/resources` 获取全量资源列表（支持分页和分类过滤），通过 `/api/v1/health/{domain}` 查询单条链接的最新检测状态。详细参数请参阅 `docs/api-reference.md`。

**Q: 如何将当前数据迁移至 PostgreSQL 生产环境？**

A: 首先在 `config/settings.py` 中将 `DATABASE_URL` 修改为 PostgreSQL 的连接字符串（格式为 `postgresql://user:pass@host:port/dbname`），然后执行 `python manage.py migrate --prod`。系统会自动读取现有 SQLite 数据并完成全量同步，同步过程中会生成校验日志，建议迁移完成后人工抽检若干条目。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
