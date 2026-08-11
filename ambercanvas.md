# ResourcePilot

ResourcePilot 是一个面向技术团队与内容运营人员的开源外链资源聚合与管理平台。该项目定位为轻量级资源导航中间件，用于将分散于多个域名的外部参考链接、政策说明页、数据源地址等进行统一收录、分类展示与快速检索，解决开发文档中外部引用链接杂乱、易失效、难以维护的问题。目标用户包括开源项目维护者、技术文档工程师、合规审查人员以及需要频繁引用特定外部站点的自动化脚本开发者。

ResourcePilot 本身不存储任何第三方内容，仅提供结构化的链接索引与状态探测功能，帮助用户高效管理外部资源依赖，降低因链接变更导致的文档或业务中断风险。

## 功能概览

- **批量链接导入与分类**：支持通过 YAML 或 JSON 配置文件一次性导入大量外链，并按自定义标签或类别分组，便于后续维护与展示。

- **链接可用性主动探测**：内置异步 HTTP 检查器，可定期对收录的 URL 进行可达性测试，自动标记异常链接并输出告警日志。

- **多格式文档生成**：支持将链接库导出为 Markdown 表格、HTML 目录页或纯文本列表，方便直接嵌入项目 README 或 Wiki。

- **模板变量替换**：允许为链接设置占位符变量（如 `{version}`、`{region}`），在生成文档时批量替换，适配多环境部署需求。

- **变更审计追踪**：记录每条链接的添加时间、修改历史与状态变化，便于团队协作时追溯责任与还原旧版本配置。

- **命令行交互界面**：提供完整的 CLI 工具，支持链接查询、新增、删除、状态刷新等操作，适合在 CI/CD 流水线中集成使用。

- **权限分级管理**：支持只读用户、编辑者、管理员三级角色，适用于多团队共用同一资源库的场景。

## 应用场景

1. **开源项目外部依赖索引**：当项目文档或代码中引用了大量第三方政策说明页、数据源或工具站时，使用 ResourcePilot 统一管理这些链接，并在 README 中自动生成引用清单，避免遗漏或错引。

2. **合规审查资料归档**：法务或合规团队需要定期核对业务所引用的外部声明页是否仍然有效。ResourcePilot 的定期探测功能可自动生成状态报告，显著降低人工巡检成本。

3. **多区域部署配置管理**：对于需要根据用户地域切换不同服务入口的应用，可通过 ResourcePilot 维护多个地域的对应链接表，并利用变量替换功能快速生成各环境的配置文件。

4. **文档自动化发布流水线**：在 CI 流程中集成 ResourcePilot 命令，每次构建时自动拉取最新链接库并生成文档片段，确保发布文档中的外部引用始终处于可用状态。

## 快速开始

以下命令演示如何获取 ResourcePilot 源码、安装依赖并启动基础服务。

```bash
# 克隆项目仓库
git clone https://github.com/resourcepilot/resourcepilot.git
cd resourcepilot

# 安装 Python 依赖（推荐使用虚拟环境）
python -m venv venv
source venv/bin/activate   # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化配置文件并运行本地服务
cp config.example.yaml config.yaml
python cli.py serve --port 8080
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 及以上 | 核心运行环境，低于此版本将无法解析类型注解 |
| pip | 21.0 及以上 | 用于安装依赖包，旧版本可能无法正确解析依赖树 |
| aiohttp | 3.8.0 及以上 | 异步 HTTP 客户端，用于并发探测链接状态 |
| pyyaml | 6.0 及以上 | 解析 YAML 格式的配置文件与导入数据 |
| jinja2 | 3.1.0 及以上 | 模板引擎，用于生成自定义格式的文档输出 |
| click | 8.1.0 及以上 | 提供命令行交互框架，支持子命令与参数解析 |
| pytest | 7.0.0 及以上 | 仅开发测试时需要，用于运行单元测试套件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门 | `docs/quickstart.md` | 如何快速上手、首个配置文件怎么写、如何启动服务？ |
| 配置 | `docs/configuration.md` | 完整的配置项说明、变量定义格式、探测间隔如何调整？ |
| 命令行 | `docs/cli.md` | 所有 CLI 子命令详情、参数示例、退出码含义？ |
| API | `docs/api.md` | 内部模块接口说明、自定义探测器的开发规范？ |
| 部署 | `docs/deployment.md` | 生产环境推荐部署方式、反向代理配置、数据库选型？ |
| 故障排查 | `docs/troubleshooting.md` | 常见启动错误、探测超时处理、日志级别调试方法？ |

## 资源列表

本项目的参考资源库涵盖多个外部信息站点，按类别整理如下。所有链接均保留用户提供的原始格式，未做任何改动。

**政策与备案类**

- <code>sihuchengrenwangzhi.org.cn</code>
- <code>zhongwenzimusiwazhifu.org.cn</code>
- <code>mianfeishipinyiquerqu.org.cn</code>

**行业资讯类**

- <code>oumeijiqingzipai.org.cn</code>
- <code>oumeiheirencuda.org.cn</code>
- <code>rennicaoshipin.org.cn</code>

**娱乐与综合类**

- <code>qingqingcaoqingyule.org.cn</code>
- <code>wuyenannvshuangshuangshuang.org.cn</code>
- <code>renqidiyiye.org.cn</code>
- <code>daxiangjiaoyazhou.org.cn</code>

## 项目结构

```
resourcepilot/
├── cli.py                      # CLI 入口，注册所有子命令
├── config.example.yaml         # 示例配置文件，含完整注释
├── requirements.txt            # 生产环境依赖列表
├── requirements-dev.txt        # 开发测试额外依赖
├── src/                        # 核心源代码目录
│   ├── core/                   # 核心模块：配置加载、日志、异常定义
│   │   ├── config.py           # 配置解析与合并逻辑
│   │   └── exceptions.py       # 自定义异常类
│   ├── checker/                # 链接探测模块
│   │   ├── http_checker.py     # HTTP/HTTPS 异步探测实现
│   │   └── scheduler.py        # 定时任务调度器
│   ├── loader/                 # 数据导入导出模块
│   │   ├── yaml_loader.py      # YAML 格式解析器
│   │   └── json_loader.py      # JSON 格式解析器
│   ├── render/                 # 文档渲染模块
│   │   ├── markdown_render.py  # Markdown 表格生成器
│   │   └── html_render.py      # HTML 目录页生成器
│   └── model/                  # 数据模型定义
│       ├── link.py             # Link 实体类（字段、状态枚举）
│       └── category.py         # 分类实体类
├── tests/                      # 单元测试目录
│   ├── test_checker.py         # 探测模块测试
│   └── test_loader.py          # 导入导出测试
├── docs/                       # 项目文档目录（见文档导航）
│   ├── quickstart.md
│   ├── configuration.md
│   └── cli.md
└── scripts/                    # 运维辅助脚本
    ├── health_check.sh         # 健康状态检查脚本
    └── backup_db.sh            # 数据库备份脚本（示例）
```

## 贡献指南

1. **问题反馈与需求讨论**：请在 GitHub Issues 中搜索是否已有相似话题，若无则新建 Issue 并填写提供的模板，详细描述使用场景、当前行为与期望行为。

2. **分支开发流程**：所有功能开发与缺陷修复均应在 `develop` 分支的基础上新建特性分支（如 `feature/xxx` 或 `fix/xxx`），完成后提交 Pull Request 并关联相关 Issue。

3. **代码规范与测试**：提交前必须执行 `pytest` 确保所有测试用例通过，同时使用 `black` 与 `isort` 进行代码格式化，保持风格统一。新增功能需补充对应单元测试。

4. **文档同步更新**：涉及配置项变更或 CLI 参数调整时，必须同步更新 `docs/` 目录下的对应文档，并确保 `config.example.yaml` 包含新增字段的注释示例。

5. **提交信息格式**：遵循 Conventional Commits 规范，使用 `feat:`、`fix:`、`docs:`、`chore:` 等前缀，提交正文简明扼要说明改动原因与影响范围。

## 常见问题

**Q：探测功能是否会对目标站点造成过大负载？**

A：探测模块默认采用单并发，且可配置请求间隔（默认 5 秒）与超时时间（默认 10 秒）。对于大型链接库，建议在非业务高峰期执行全量探测，或通过配置只检查上次状态变更超过 24 小时的链接，避免频繁请求。

**Q：如何迁移已有的链接列表到 ResourcePilot？**

A：项目支持从 CSV 和 JSON Lines 格式导入。您可以使用 `cli.py import --format csv --file old_links.csv` 命令进行批量导入，导入前建议先执行 `--dry-run` 参数进行预检查，确认字段映射正确后再执行实际导入。

**Q：服务重启后历史探测记录会丢失吗？**

A：ResourcePilot 默认将历史状态变更记录保存在本地 SQLite 数据库中（路径由 `db.path` 配置项指定）。只要该文件未被删除，重启服务后会自动加载最近 30 天的记录。如需持久化到外部数据库，可配置 `db.dsn` 连接串切换至 PostgreSQL 或 MySQL。

## 许可证

MIT License

Copyright (c) 2026 ResourcePilot Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
