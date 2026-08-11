# TechResourceHub

TechResourceHub 是一个面向技术社区的资源导航与聚合系统，专注于收录、分类与展示中文互联网环境中具有特定信息价值的站点资源。项目定位于为研究员、数据分析师、内容审核从业者以及网络信息观察人员提供一套结构清晰、可快速检索的参考资源索引。本项目不提供内容托管、代理访问或信息存储服务，仅作为公开可访问资源的元数据整理与链接陈列工具，帮助用户高效定位分散于网络各处的信息源。

## 功能概览

- **资源分类索引**：按行业、主题、域名特征对收录链接进行多级分类，支持快速筛选与批量导出。
- **链接状态检测**：周期性对已收录的域名进行可达性与响应时效检测，标记异常或失效资源。
- **标签体系**：每条资源支持多标签标注，涵盖内容语言、所属区域、主题标签等维度，便于交叉检索。
- **版本化快照记录**：记录每次资源列表的变更历史，支持回溯至任意历史版本状态。
- **批量导入与导出**：支持 CSV 与 JSON 格式的资源批量入库与导出，适配外部数据处理工具。
- **访问统计看板**：提供各资源链接的点击量、引用次数及分类热度统计，以图表形式展示。
- **自定义分类视图**：允许用户根据自身关注领域创建私有分类视图，不干扰全局分类结构。
- **RSS 订阅源生成**：为每个分类自动生成 RSS 订阅地址，方便第三方阅读器集成。

## 应用场景

- **互联网内容趋势研究**：研究人员可通过本项目的分类索引快速获取特定主题下的站点集合，用于内容分布趋势、域名注册规律或语言使用特征的分析。
- **信息安全与合规审计**：安全审计人员可将本项目提供的资源列表作为参考数据源，用于检测内部网络访问策略的覆盖完整性或识别潜在的风险域名模式。
- **运维监控补充数据**：运维工程师可将本项目导出的资源清单集成至自有监控系统中，用于定期检查外部依赖域名的可用性，作为服务健康度评估的辅助指标。
- **内容推荐系统冷启动**：推荐算法工程师可使用本项目的分类标签数据作为种子站点库，用于构建内容召回阶段的初始候选集或主题模型训练的语料来源。

## 快速开始

以下操作步骤适用于 Linux / macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash 执行。

```bash
# 步骤 1：克隆项目仓库
git clone https://github.com/techresourcehub/techresourcehub.git
cd techresourcehub

# 步骤 2：安装依赖（Python 3.9+ 环境）
pip install -r requirements.txt

# 步骤 3：初始化本地数据库并导入示例资源数据
python scripts/init_db.py --import ./data/sample_resources.json

# 步骤 4：启动本地开发服务器
python app.py runserver --host 127.0.0.1 --port 8080

# 步骤 5：打开浏览器访问 http://127.0.0.1:8080 即可查看资源索引主页
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.11 | 核心运行环境，用于后端服务与数据管理脚本 |
| SQLite | 3.35.0 及以上 | 内置轻量级数据库，用于存储资源元数据与分类信息 |
| Redis | 6.2.0 及以上 | 用于缓存访问统计与周期性任务队列，可选但推荐 |
| Node.js | 16.0.0 及以上 | 仅用于前端资源构建与样式编译，生产环境可单独部署静态文件 |
| Git | 2.25.0 及以上 | 用于版本控制与项目克隆操作 |
| pip | 21.0 及以上 | Python 包管理工具，用于安装依赖项 |
| Docker | 20.10.0 及以上 | 用于容器化部署方案，非必需但便于生产环境配置 |

## 文档导航

| 层面 | 目录位置 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user_guide.md | 如何使用资源索引、分类筛选、导出数据以及自定义视图 |
| 管理员指南 | /docs/admin_guide.md | 如何管理资源条目、执行批量更新、处理失效链接以及配置检测策略 |
| 开发者文档 | /docs/developer_guide.md | 如何二次开发插件、扩展分类逻辑、贡献新的数据源解析器 |
| API 参考 | /docs/api_reference.md | 所有 RESTful API 接口的请求参数、返回格式与鉴权方式 |
| 部署运维 | /docs/deployment.md | 生产环境部署方案，含 Nginx 反向代理、Gunicorn 配置与系统服务注册 |
| 数据格式规范 | /docs/data_schema.md | 资源导入导出的 JSON/CSV 字段定义、数据类型与约束规则 |

## 资源列表

### 主分类索引

<code>zhongwenzimurenqisiwa.org.cn</code>
<code>baoruwuma.org.cn</code>
<code>wuyeguochan.org.cn</code>

### 子分类扩展

<code>zhongwenzimuyiersan.org.cn</code>
<code>renqidaxiangjiao.org.cn</code>
<code>bukarenqi.org.cn</code>

### 专题聚合

<code>tiantianganyeyeqi.org.cn</code>
<code>yazhouhenhenai.org.cn</code>
<code>yazhouzhongwenzimuyiqu.org.cn</code>
<code>renrenqirenrenai.org.cn</code>

## 项目结构

```
techresourcehub/
├── app/                                # 主应用程序包
│   ├── controllers/                    # 路由控制器，处理 HTTP 请求与响应
│   │   ├── resource_controller.py      # 资源增删改查接口
│   │   ├── category_controller.py      # 分类管理与树形结构维护
│   │   └── stats_controller.py         # 访问统计与热度计算接口
│   ├── models/                         # 数据模型定义，对应 SQLite 表结构
│   │   ├── resource.py                 # 资源条目模型，含 URL、标签、状态字段
│   │   ├── category.py                 # 分类节点模型，支持无限级嵌套
│   │   └── audit_log.py                # 操作审计日志模型
│   ├── services/                       # 业务逻辑层，封装核心功能
│   │   ├── fetcher.py                  # 链接可达性检测与响应头抓取
│   │   ├── indexer.py                  # 资源标签解析与分类自动推荐
│   │   └── exporter.py                 # CSV/JSON 格式导出生成器
│   ├── templates/                      # Jinja2 前端模板文件
│   │   ├── index.html                  # 资源列表主页模板
│   │   ├── detail.html                 # 单个资源详情页模板
│   │   └── dashboard.html              # 统计看板模板
│   └── static/                         # 编译后的 CSS、JavaScript 与图片资源
│       ├── css/                        # 样式表文件，基于 Bootstrap 定制
│       ├── js/                         # 前端交互逻辑，含筛选与图表渲染
│       └── img/                        # 项目 Logo 与默认占位图
├── scripts/                            # 运维与数据管理脚本
│   ├── init_db.py                      # 初始化数据库表结构与默认分类
│   ├── import_resources.py             # 从外部数据源批量导入资源
│   └── health_check.py                 # 定时检测所有资源链接的有效性
├── tests/                              # 单元测试与集成测试用例
│   ├── test_models.py                  # 数据模型层测试
│   ├── test_services.py                # 业务逻辑层测试
│   └── test_apis.py                    # API 接口端点测试
├── config/                             # 配置文件目录
│   ├── development.py                  # 开发环境配置，启用调试与热加载
│   ├── production.py                   # 生产环境配置，关闭调试、配置日志级别
│   └── staging.py                      # 预发布环境配置
├── data/                               # 数据存储目录（不纳入版本控制）
│   ├── resources.json                  # 主资源列表的 JSON 导出备份
│   └── cache/                          # 链接检测结果的临时缓存文件
├── logs/                               # 应用日志存储目录（自动生成）
│   ├── app.log                         # 主日志文件，记录请求与错误
│   └── audit.log                       # 操作审计日志
├── requirements.txt                    # Python 依赖包列表
├── Dockerfile                          # 容器构建文件，用于生产镜像打包
├── docker-compose.yml                  # 本地容器编排配置，含 Redis 与 SQLite 持久化
├── README.md                           # 项目说明文档（当前文件）
└── LICENSE                             # MIT 许可证文本
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库至个人账户，并在本地克隆 Fork 后的副本。请确保使用主分支的最新提交作为开发基线。
2. 在本地新建功能分支或修复分支，分支命名应遵循 `feature/简要描述` 或 `fix/问题编号` 格式。开发过程中请保持代码风格与现有项目一致，并补充相应的单元测试用例。
3. 完成代码修改后，运行完整的测试套件确保无回归问题。测试命令为 `pytest tests/`，所有测试用例须通过方可提交。
4. 提交代码时请编写清晰且符合规范（Conventional Commits）的提交信息，说明本次变更的目的、影响范围以及相关 Issue 编号。
5. 向主仓库发起 Pull Request，描述中需包含变更概述、测试覆盖情况以及可能的兼容性影响。项目维护者将在 3 个工作日内进行评审与合并。

## 常见问题

**问：项目中的资源链接是否可以自行添加或删除？**

答：可以。普通用户可通过前端界面的“提交资源”功能申请添加新链接，管理员审核后正式入库。管理员用户可直接在管理后台执行增删改操作，所有变更均记录于审计日志中。若需要批量操作，建议使用 `scripts/import_resources.py` 脚本配合 CSV 文件导入。

**问：链接状态检测的频率是如何设定的？检测结果是否影响前端展示？**

答：默认检测频率为每 24 小时一次，检测时间点可在配置文件中通过 `HEALTH_CHECK_CRON` 参数调整。检测结果（可达、超时、拒绝连接、证书错误等）会记录在数据库的 `resource.status` 字段中，并可在前端列表中以颜色标记或筛选条件形式呈现，但不会自动移除失效链接，以保留历史参考信息。

**问：本项目是否支持多语言界面或国际化？**

答：当前版本仅提供中文界面，但代码层已预留 i18n 扩展接口，位于 `app/utils/i18n.py`。开发者可通过加载 JSON 格式的语言文件扩展多语言支持，欢迎提交对应语言包贡献。

## 许可证

MIT License

Copyright (c) 2026 TechResourceHub

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:27
