# TechLink Navigator

TechLink Navigator 是一个面向技术调研、内容聚合与合规性扫描场景的轻量级外链资源汇总系统。该项目定位于技术团队、内容运营人员与合规审计师，用于快速构建可追溯、可分类、可版本化的外链资源目录，解决多源链接分散、手工整理易错、变更历史难回溯等问题。系统以纯静态 Markdown 为核心数据层，配合自动化校验脚本，可在 CI/CD 环境中运行，输出结构化资源清单。

## 功能概览

- **批量外链导入与去重**：支持从 CSV、JSON 或纯文本列表批量导入 URL，自动去除重复条目，并检测协议一致性。
- **合规性规则引擎**：内置可配置的正则过滤规则，支持黑名单域名、路径关键词、协议限定等策略，对外链进行自动化合规标注。
- **多维度分类标签**：每个外链资源可绑定多个分类标签（如“文档”、“社区”、“工具”、“合规”），支持层级标签体系。
- **变更审计日志**：记录每次外链增删改的操作人、时间戳与变更原因，生成可导出的审计报告。
- **健康状态探测**：周期性对已收录的外链发起 HEAD 请求，检测状态码、响应时间与 TLS 证书有效期，标记异常链接。
- **静态站点生成**：基于项目根目录下的 `resources/` 数据文件，一键生成可供内部浏览的静态 HTML 目录页，无需数据库。
- **命令行交互工具**：提供 `tln` CLI 工具，支持外链添加、删除、列表查询、合规校验等常用操作，适合脚本化调用。

## 应用场景

- **技术文档库的外链管理**：大型技术文档项目往往引用数十个外部参考链接。TechLink Navigator 可帮助文档团队统一维护这些链接，定期检测失效资源，并在版本发布前自动执行合规扫描。
- **内容聚合网站的源管理**：面向垂直领域的内容聚合平台，需要持续从多个源头采集信息。本系统可作为上游源地址的登记与校验层，确保采集任务指向的 URL 始终有效且符合内容安全策略。
- **企业内部合规审计辅助**：法务或合规部门需要定期审查对外公开页面中的外部链接。TechLink Navigator 提供标签化过滤与审计日志，支持按时间范围导出链接变更记录，减轻人工核对负担。
- **开源项目外部依赖溯源**：开源项目中常常包含对第三方服务、镜像源或参考资料的引用。使用本系统可以建立一份清晰的外部依赖清单，便于在供应链风险排查时快速定位。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境。

```bash
# 1. 克隆项目仓库
git clone https://github.com/techlink-navigator/tln-core.git
cd tln-core

# 2. 安装依赖（需要 Python 3.9+ 和 pip）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化本地资源数据库并运行示例导入
python scripts/init_db.py --sample
python scripts/import_urls.py --input samples/url_list_sample.csv --tag initial

# 4. 执行一次完整校验并生成静态目录
tln validate --all
tln build --output ./public

# 5. 启动本地预览服务器（可选）
python -m http.server 8000 --directory ./public
```

访问 `http://localhost:8000` 即可查看生成的资源目录页面。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.11 | 核心运行环境，3.12 暂未完全适配 |
| pip | 21.0+ | Python 包管理工具 |
| Git | 2.25+ | 用于克隆仓库及版本管理 |
| Network | 公网可访问 | 用于外链健康状态探测（可配置代理） |
| 磁盘空间 | 至少 200 MB | 存放资源数据、日志及生成的静态文件 |
| 内存 | 建议 512 MB 以上 | 处理大规模链接列表（> 10 万条）时建议 1 GB |
| 操作系统 | Linux / macOS / Windows (WSL2) | 生产环境推荐 Linux |
| make | 3.81+ | 可选，用于执行自动化任务脚本 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user-guide/` | 如何使用 CLI 工具、如何配置合规规则、如何生成静态目录 |
| 管理员指南 | `docs/admin/` | 如何部署生产环境、如何配置 CI/CD 流水线、如何迁移数据 |
| 开发文档 | `docs/developer/` | 如何扩展新校验器、如何修改标签体系、如何运行单元测试 |
| 设计说明 | `docs/design/` | 系统的模块划分、数据流图、关键数据结构设计 |
| 故障排查 | `docs/troubleshooting/` | 常见报错及解决方法、日志分析方法、性能调优建议 |

## 资源列表

### 核心数据源（第 13/455 批次）

本批次收录的原始链接如下，将作为初始资源清单导入系统，并接受合规性校验与健康检测。

<code>zhongwenzimurenqisiwa.org.cn</code>
<code>baoruwuma.org.cn</code>
<code>wuyeguochan.org.cn</code>
<code>zhongwenzimuyiersan.org.cn</code>
<code>renqidaxiangjiao.org.cn</code>
<code>bukarenqi.org.cn</code>
<code>tiantianganyeyeqi.org.cn</code>
<code>yazhouhenhenai.org.cn</code>
<code>yazhouzhongwenzimuyiqu.org.cn</code>
<code>renrenqirenrenai.org.cn</code>

## 项目结构

```
tln-core/
├── src/                                # 核心源代码目录
│   ├── core/                           # 核心模块
│   │   ├── validator.py                # 合规性校验引擎
│   │   ├── health.py                   # 健康探测（HTTP / TLS）
│   │   ├── tagger.py                   # 标签分类管理
│   │   └── audit.py                    # 审计日志写入与查询
│   ├── cli/                            # 命令行工具实现
│   │   ├── main.py                     # tln 入口
│   │   ├── commands.py                 # 各子命令路由
│   │   └── formatter.py                # 终端输出格式
│   └── static/                         # 静态站点生成器
│       ├── generator.py                # HTML / JSON 生成
│       ├── templates/                  # Jinja2 模板
│       └── assets/                     # CSS / JS 静态资源
├── scripts/                            # 运维与开发辅助脚本
│   ├── init_db.py                      # 初始化本地数据存储
│   ├── import_urls.py                  # 批量导入外部列表
│   └── migrate_v1_to_v2.py             # 数据迁移工具
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # 单元测试（pytest）
│   ├── integration/                    # 集成测试（含网络请求）
│   └── fixtures/                       # 测试用固定数据集
├── docs/                               # 全部文档（见文档导航）
├── resources/                          # 资源数据存储（JSON / SQLite）
│   ├── raw/                            # 原始导入数据备份
│   ├── processed/                      # 清洗后数据
│   └── audit_logs/                     # 审计日志文件
├── public/                             # 静态站点输出目录（生成后）
├── config/                             # 配置文件目录
│   ├── default.yaml                    # 默认配置
│   ├── production.yaml                 # 生产环境覆盖
│   └── rules/                          # 合规规则集（正则表达式）
├── requirements.txt                    # Python 依赖列表
├── Makefile                            # 常用任务脚本
├── README.md                           # 项目主文档（本文件）
└── LICENSE                             # MIT 许可证
```

## 贡献指南

1. 查阅问题追踪器中的“待认领”标签，或提交新 Issue 描述你希望解决的问题或新增功能，等待维护者确认。
2. 从主仓库派生副本到你的个人账户下，并将派生仓库克隆至本地开发环境。
3. 创建新的功能分支，分支命名遵循 `feature/简述` 或 `fix/简述` 格式，例如 `feature/add-telegram-notifier`。
4. 完成代码修改后，确保所有原有单元测试通过，并为新增代码编写对应的测试用例。运行 `make test` 可执行全部测试。
5. 提交 Pull Request 到主仓库的 `main` 分支，在 PR 描述中关联对应的 Issue 编号，并简要说明改动内容与测试覆盖情况。

## 常见问题

**Q：系统是否支持 HTTPS 与 HTTP 混用？**

A：支持。校验引擎默认保留原始协议，但合规规则中可配置强制要求 HTTPS，此时会对 HTTP 链接发出警告。健康探测模块会自动跟随重定向，最终状态码与最终 URL 都会记录。

**Q：如何处理被屏蔽或需要代理的外链？**

A：健康探测模块支持通过环境变量 `HTTP_PROXY` 和 `HTTPS_PROXY` 配置代理服务器。对于需要认证的代理，可扩展 `src/core/health.py` 中的 Session 配置。建议在生产环境将代理地址写入 `config/production.yaml`。

**Q：静态站点的访问权限如何控制？**

A：本系统生成的静态站点不内置认证机制。如需限制访问，建议配合 Web 服务器的基本认证（如 Nginx 的 auth_basic），或将 `public/` 目录部署在已经存在身份验证体系的内部网段中。

## 许可证

MIT License

Copyright (c) 2026 TechLink Navigator Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
