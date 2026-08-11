# RQResource Aggregator

RQResource Aggregator 是一个面向中文网络资源检索与分类导航的开源工具集，定位为技术化外链汇总与结构化数据管理方案。该项目主要服务于需要高效组织、校验和展示大量外部链接的开发者、内容运营者及数据归档人员，帮助其解决多源异构链接在收集、去重、可用性检测及版本控制中的混乱问题。

项目以静态站点生成与自动化检测脚本为核心，提供标准化链接元数据模板，支持批量导入、规则过滤、状态监控与多格式导出。通过将分散的资源链接转化为可维护的结构化数据集，RQResource Aggregator 显著降低人工维护成本，提升资源库的长期可用性与可追溯性。

## 功能概览

- **批量链接导入与解析**：支持从 CSV、JSON 及纯文本列表批量导入 URL，自动解析协议、域名及路径参数，生成标准化资源记录。

- **自定义分类与标签系统**：允许用户为每个链接赋予多级分类、自定义标签及备注信息，便于按主题、来源或质量等级进行筛选与分组。

- **自动化可用性检测**：内置异步 HTTP 检测引擎，可定时检查链接响应状态码、页面标题及重定向链，标记失效或异常资源。

- **结构化数据导出**：支持将整理后的资源列表导出为 Markdown 表格、JSON 字典或静态 HTML 页面，适配文档生成、API 响应或站点展示等不同需求。

- **链接关系图谱**：基于域名聚合与引用关系分析，可视化展示资源之间的关联密度，辅助识别核心站点与孤立条目。

- **变更审计日志**：记录每次增删改操作的时间、内容及操作者，支持回滚与差异对比，满足团队协作下的资源管理审计要求。

- **多端适配的预览模板**：提供响应式 Web 预览界面，在桌面与移动设备上均能清晰浏览资源列表，并支持快速跳转与复制功能。

- **命令行交互工具**：提供完整的 CLI 命令集，支持脚本化批量处理，便于集成至 CI/CD 流水线或定时任务。

## 应用场景

- **技术文档外链维护**：技术团队在撰写项目文档或 Wiki 时，需引用大量外部参考链接。RQResource Aggregator 可作为文档外链的后台管理工具，自动检测链接有效性，并生成统一的引用列表，避免文档中出现死链。

- **内容聚合站点构建**：内容创作者或垂直领域媒体运营者，可利用本项目的分类与导出功能，快速搭建一个基于 Markdown 或 JSON 数据的资源导航页面，无需从零设计数据库结构。

- **数据归档与迁移校验**：在进行网站迁移或数据备份时，管理员可使用自动化检测功能，批量验证待迁移资源列表中的每个 URL 是否仍可访问，确保迁移后的资源完整性。

- **学术参考链接整理**：研究人员在收集文献、数据集或工具站点时，可利用标签与备注系统对链接进行精细标注，并通过关系图谱发现同领域内的核心资源分布。

## 快速开始

以下步骤帮助您在本地环境快速启动 RQResource Aggregator 的基础服务。

```bash
# 1. 克隆项目仓库
git clone https://github.com/rqresource/rqresource-aggregator.git

# 2. 进入项目目录
cd rqresource-aggregator

# 3. 安装依赖（使用 Python 虚拟环境）
python3 -m venv venv
source venv/bin/activate   # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 4. 初始化示例资源数据库
python manage.py initdb --sample-data

# 5. 启动本地预览服务
python manage.py serve --port 8080

# 此时访问 http://127.0.0.1:8080 即可查看示例资源列表
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行时，用于执行管理脚本与检测引擎 |
| pip | 22.0 及以上 | Python 包管理工具，用于安装依赖库 |
| aiohttp | 3.9.0 | 异步 HTTP 客户端，用于并发链接检测 |
| jinja2 | 3.1.0 | 模板引擎，用于生成预览页面与导出 HTML |
| PyYAML | 6.0 | YAML 解析器，用于读取自定义配置文件 |
| click | 8.1.0 | CLI 命令框架，提供命令行交互接口 |
| pytest | 8.0.0（可选） | 单元测试框架，用于运行项目测试套件 |
| Git | 2.30 及以上（可选） | 版本控制工具，用于克隆仓库及提交变更 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|----------|-----------|
| 入门指南 | docs/quickstart.md | 如何在 10 分钟内完成安装、配置并导入第一批资源链接？ |
| 功能手册 | docs/commands.md | 每个 CLI 命令的具体参数、用法及典型示例是什么？ |
| 数据规范 | docs/schema.md | 资源记录的 JSON 结构、必填字段及扩展字段如何定义？ |
| 部署运维 | docs/deployment.md | 如何将资源聚合器部署为长期运行的后台服务或静态站点生成器？ |
| API 参考 | docs/api/internal.md | 内部核心模块（检测器、解析器、导出器）的类与方法接口说明？ |
| 故障排查 | docs/troubleshooting.md | 遇到链接检测超时、导出编码错误或预览空白时如何定位问题？ |

## 资源列表

本部分收录项目初始内置及示例数据中涉及的全部外部链接，按类别分组展示。所有链接均按原始输入原样呈现，未做任何协议补全或域名规范化处理。

### 核心分类索引

- <code>zhongwenrenqi.org.cn</code>
- <code>renqishaofu.org.cn</code>
- <code>rihanlunli.org.cn</code>

### 多媒体与视频专题

- <code>bajiaoshipinapp.org.cn</code>
- <code>zhongwenzimusiwa.org.cn</code>
- <code>renqiyouma.org.cn</code>

### 社区与交互平台

- <code>xiaodiaowang.org.cn</code>
- <code>chengrenjingpin18.org.cn</code>

### 综合归档与专项资源

- <code>guoyuav.org.cn</code>
- <code>jiujiurenqi.org.cn</code>

## 项目结构

```
rqresource-aggregator/
├── manage.py                  # CLI 入口，聚合所有子命令
├── requirements.txt           # 生产环境依赖列表
├── config/                    # 配置目录
│   ├── default.yaml           # 全局默认配置（检测超时、并发数、导出格式）
│   └── schema.json            # 资源记录 JSON Schema 定义
├── core/                      # 核心业务模块
│   ├── __init__.py
│   ├── detector.py            # 异步链接检测器，包含重试与超时策略
│   ├── parser.py              # URL 解析与规范化工具
│   ├── exporter.py            # 支持 Markdown/JSON/HTML 的导出器
│   └── graph.py               # 域名聚合与关系图谱计算
├── storage/                   # 数据持久化层
│   ├── memory.py              # 内存存储实现（用于测试）
│   └── file.py                # 基于 JSON 文件的存储实现
├── templates/                 # Jinja2 预览模板
│   ├── base.html              # 基础布局模板
│   └── resource_list.html     # 资源列表渲染模板
├── tests/                     # 单元测试与集成测试
│   ├── test_detector.py
│   ├── test_parser.py
│   └── test_exporter.py
├── docs/                      # 项目文档源文件
│   ├── quickstart.md
│   ├── commands.md
│   ├── schema.md
│   ├── deployment.md
│   ├── api/
│   └── troubleshooting.md
└── sample_data/               # 示例资源数据
    ├── sample_links.json      # 包含本 README 资源列表的示例数据
    └── sample_tags.yaml       # 预定义的分类标签体系
```

## 贡献指南

1. **问题报告与需求提议**：请在 GitHub Issues 中搜索是否已有相似话题，若无则新建 Issue，并按照模板填写复现步骤、预期行为与实际结果，或详细描述新功能的使用场景。

2. **分支开发流程**：从 `main` 分支切出 `feature/xxx` 或 `fix/xxx` 功能分支进行开发，确保分支命名简洁反映变更内容。开发完成后提交 Pull Request 至 `main` 分支。

3. **代码风格与测试**：所有 Python 代码需遵循 PEP 8 规范，并使用 `black` 格式化。新增或修改功能必须补充对应的单元测试，确保测试覆盖率达到 80% 以上。运行 `pytest tests/` 验证本地测试通过。

4. **文档同步更新**：若变更涉及 CLI 命令、配置项或数据模型，需同步更新 `docs/` 目录下的对应文档，并在 PR 描述中标注文档变更位置。

5. **提交信息规范**：提交信息使用 `<type>(<scope>): <subject>` 格式，其中 type 可选 `feat`、`fix`、`docs`、`refactor`、`test` 等，scope 为影响的模块名称，subject 简明描述变更内容。

## 常见问题

**Q1: 检测链接时出现大量超时或连接拒绝，如何处理？**

A: 首先检查网络环境是否可访问目标域名，部分站点可能对高频请求有限制。您可以在 `config/default.yaml` 中调整 `detection.timeout` 参数（单位秒）和 `detection.concurrent_limit` 参数（并发数）以降低检测压力。若仍失败，可使用 `--retry` 参数手动重试失败条目。

**Q2: 导出的 Markdown 表格中链接显示为纯文本，无法点击跳转？**

A: 默认导出的 Markdown 采用标准表格语法，链接以 `<code>` 包裹，旨在保持可读性并避免自动渲染干扰。若需要可点击链接，可在导出时指定 `--format html` 或使用 `--link-style full` 参数生成包含 `[text](url)` 语法的版本。具体参数请参考 `docs/commands.md` 中的 export 子命令说明。

**Q3: 项目是否支持 Windows 系统下的路径编码问题？**

A: 项目内部所有文件路径操作均使用 Python 的 `pathlib` 模块，该模块自动处理不同操作系统下的路径分隔符与编码差异。在 Windows 下运行 CLI 命令时，建议使用 PowerShell 或 Git Bash 终端，并确保系统区域设置为 UTF-8 编码，以避免控制台输出乱码。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:25
