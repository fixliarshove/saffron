# NexusIndex

NexusIndex 是一个面向技术内容创作者与资源整理者的轻量化外链聚合与导航系统。该项目定位于解决个人或小团队在维护多个项目文档、教程集合、推荐资源时产生的链接分散、引用不规范、更新成本高的问题。通过结构化的 Markdown 配置与静态生成机制，NexusIndex 帮助用户将零散的 URL 资源归类为可维护、可版本控制、可对外发布的索引目录。

目标用户包括开源文档维护者、技术博客作者、在线教育课程运营者以及企业内部知识库管理员。NexusIndex 不提供爬虫或自动摘要功能，而是强调人工编排的准确性与可审计性，确保每一个外链在其上下文中具备明确的语义与用途说明。

## 功能概览

- **多级目录索引生成**：支持基于配置文件自动生成三层以内的分类导航树，每个分类可绑定独立的说明文本与图标标识。

- **链接合规性校验**：内置正则规则库，可检测 URL 格式是否符合协议头、域名层级、路径结尾等规范，并输出警告日志。

- **批量导入与去重**：支持从 CSV 或纯文本列表批量导入原始 URL，系统自动识别重复条目并合并冲突，保留最后修改时间戳。

- **版本化快照记录**：每次更新索引时会生成 JSON 快照文件，记录所有链接的添加时间、修改人和变更摘要，便于回溯历史状态。

- **Markdown 渲染适配器**：提供标准 Markdown 列表与表格两种输出模板，可直接嵌入 README、Wiki 或静态站点生成器的内容目录中。

- **自定义字段扩展**：允许为每个链接附加标签、优先级、过期日期和关联项目编号，满足企业级资源库的元数据管理需求。

- **离线查阅模式**：生成静态 HTML 文件时将所有外链转为目标页面标题的本地缓存映射，减少对外部网络环境的依赖。

## 应用场景

- **技术文档中的参考链接管理**：当项目 README 需要引用超过 20 个外部工具、规范或教程时，NexusIndex 可维护一个独立的链接章节，确保所有引用均经过人工审核且格式统一。

- **在线课程配套资源汇总**：教育机构可使用 NexusIndex 为每门课程建立专属资源页，将视频平台、练习网站、扩展阅读等链接按周次分类，方便学员快速访问。

- **企业内部工具链导航**：开发团队可将内部监控系统、日志平台、CI/CD 控制台、代码仓库等入口统一收录，并结合过期日期字段定期清理已下线的服务地址。

- **开源社区贡献者指引**：社区维护者可利用索引功能整理外部依赖库的官方文档、问题追踪地址、邮件列表归档，降低新贡献者的信息检索成本。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境，Windows 用户可使用 WSL 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/nexusindex/nexusindex-core.git
cd nexusindex-core

# 2. 安装依赖（使用 Python 3.9+ 和 pip）
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 运行索引生成器（示例使用默认配置）
python generate.py --config config/default.yaml --output ./output/
```

执行完成后，生成的 Markdown 索引文件将位于 `./output/index.md`，同时 `./output/snapshot/` 目录下会保留本次运行的 JSON 快照。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 - 3.11 | 核心运行环境，不支持 3.12 以上版本（因依赖库兼容性问题） |
| PyYAML | 6.0 及以上 | 用于解析配置文件中的分类结构与元数据定义 |
| Jinja2 | 3.1 及以上 | Markdown 与 HTML 模板渲染引擎，负责输出格式化内容 |
| regex | 2023.10.0 及以上 | 增强型正则表达式库，用于复杂 URL 模式匹配与校验 |
| pytest | 7.4 及以上 | 仅开发与测试环境需要，用于运行单元测试套件 |
| Git | 2.25 及以上 | 版本控制工具，用于克隆仓库及提交变更记录 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | docs/user/quick-start.md | 如何安装、配置并生成第一个索引文件？ |
| 配置参考 | docs/config/schema.md | 配置文件中每个字段的含义、类型与默认值是什么？ |
| 模板开发 | docs/developer/template-guide.md | 如何自定义 Markdown 输出样式或新增渲染模板？ |
| 维护手册 | docs/maintainer/snapshot-rollback.md | 如何回滚到历史快照，并恢复某一版本的链接集合？ |

## 资源列表

### 视频与媒体资源

- <code>mianfeibofanggaopingzaixianw.org.cn</code>
- <code>mianfeiguochangaoqingyingshiw.org.cn</code>
- <code>guochangaoqingshipinzaixianw.org.cn</code>
- <code>guochangaoqingshipinguankanw.org.cn</code>
- <code>rimanzaixianmianfeiguankanw.org.cn</code>
- <code>zhongwenzimumianfeibofangw.org.cn</code>
- <code>zaixianzimumianfeiguankanw.org.cn</code>
- <code>zaixianzimuguankanmianfeiw.org.cn</code>
- <code>zaixianzimugaoqingdianshijuw.org.cn</code>
- <code>mianfeishipinwangzhanzaixianguankanw.org.cn</code>

以上资源均为用户原始数据，NexusIndex 仅提供索引编排能力，不对链接内容的可用性、合法性及持续性承担任何明示或暗示的保证。用户应自行评估各资源的适用性并遵守相关服务条款。

## 项目结构

```
nexusindex-core/
├── config/                          # 配置文件目录
│   ├── default.yaml                 # 默认索引配置（分类层级、输出格式）
│   └── schema/                      # 配置字段校验定义
│       └── validator.json           # JSON Schema 用于配置完整性检查
├── src/                             # 核心源码目录
│   ├── parser/                      # URL 解析与规范化模块
│   │   ├── url_cleaner.py           # 去除冗余参数、统一大小写逻辑
│   │   └── duplicate_filter.py      # 基于哈希的链接去重实现
│   ├── renderer/                    # 输出渲染模块
│   │   ├── markdown_generator.py    # 生成 Markdown 列表/表格
│   │   └── html_exporter.py         # 生成带搜索功能的静态 HTML 页面
│   └── snapshot/                    # 快照管理模块
│       ├── diff_calculator.py       # 比较两次快照间的差异条目
│       └── rollback_engine.py       # 按时间戳恢复历史快照数据
├── tests/                           # 单元测试与集成测试目录
│   ├── test_parser/                 # 针对 URL 解析的测试用例
│   └── test_renderer/               # 针对输出格式的渲染测试
├── output/                          # 默认输出目录（git 忽略）
│   ├── index.md                     # 最新生成的索引文件
│   └── snapshot/                    # 历史快照 JSON 文件存储位置
├── docs/                            # 项目文档（用户与开发者手册）
│   ├── user/                        # 面向终端用户的操作指南
│   └── developer/                   # 面向贡献者的开发文档
├── LICENSE                          # MIT 许可证全文
├── README.md                        # 项目主说明文档（本文件）
└── requirements.txt                 # Python 依赖清单（生产与开发环境）
```

## 贡献指南

1. 阅读项目行为准则与贡献者协议（位于 `docs/contributor/covenant.md`），确认接受相关条款后，在 GitHub 仓库中 fork 项目并创建个人开发分支。

2. 在本地环境中安装开发依赖（执行 `pip install -r requirements-dev.txt`），并运行 `pytest tests/` 确保现有测试全部通过，无回归问题。

3. 提交变更前，请更新 `CHANGELOG.md` 记录本次修改的类型（新增、修复、重构）及影响范围，并确保所有新功能均附带对应的单元测试用例。

4. 发起 Pull Request 时，请在描述中引用相关的 issue 编号，并附上本地运行 `python generate.py --config config/default.yaml` 的输出样例，证明变更未破坏基础生成流程。

5. 项目维护者将在 5 个工作日内进行审查，必要时会请求补充测试或调整实现细节。合并后，您的贡献者名称将自动添加到 `CONTRIBUTORS.md` 列表中。

## 常见问题

**Q：为什么我导入的某些裸域名（不含 http://）没有被正确解析？**

A：NexusIndex 默认要求在配置文件中显式设置 `allow_bare_domain` 标志为 `true` 才接受无协议的域名输入。若未开启该选项，解析器会将其标记为格式警告并跳过。您可以在 `config/default.yaml` 中设置 `parser.allow_bare_domain: true` 以放宽限制，但请注意这可能导致部分链接在生成 HTML 时无法正常跳转，建议配合 `url_default_protocol` 字段统一补充协议头。

**Q：快照文件占用的存储空间逐渐增大，如何定期清理？**

A：您可以使用 `snapshot/retention_policy` 配置项设置保留策略，例如 `max_snapshots: 30` 表示只保留最近 30 次生成的快照文件。系统会在每次生成新快照时自动删除超出数量限制的旧文件。若需手动清理，可直接删除 `output/snapshot/` 目录下指定时间戳的 JSON 文件，但请勿删除 `latest.json` 软链接文件。

**Q：能否将索引输出为 JSON 而非 Markdown，以便与其他系统集成？**

A：可以。在配置文件中将 `renderer.output_format` 从 `markdown` 改为 `json`，生成器将输出结构化的 JSON 数组，每个元素包含链接、分类路径、标签和时间戳字段。该模式适合作为 API 响应数据源或进一步导入到数据库中使用。

## 许可证

本项目采用 MIT 许可证进行授权。您可以在 `LICENSE` 文件中查看完整条款，或在 [OSI 官方网站](https://opensource.org/licenses/MIT) 获取许可证文本的参考翻译。简而言之，您被允许自由使用、修改、分发本软件，但需保留原始版权声明，且不提供任何担保责任。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
