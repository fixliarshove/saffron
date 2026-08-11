# Terminus Catalog

Terminus Catalog 是一个面向开发人员与技术研究者的高质量技术资源导航与外部链接聚合系统。本项目定位于解决技术信息过载背景下的资源筛选与索引问题，通过人工整理与社区驱动的机制，为后端工程、系统架构、网络协议及多媒体处理等方向提供稳定、可追溯的参考链接库。目标用户包括基础架构工程师、DevOps 实践者、技术选型负责人以及计算机科学相关领域的研究人员。

本项目并非简单的书签集合，而是一个具备版本控制、分类标签、变更追踪与社区贡献流程的开放资源仓库。我们通过对每个收录的 URL 进行主题标注、可用性检测与内容摘要生成，帮助用户在复杂的技术生态中快速定位高价值信息。所有资源链接均经过初始质量审核，并鼓励用户通过 Issue 与 Pull Request 参与维护，从而构建一个长期活跃的技术外链生态。

## 功能概览

- **主题分类索引**：所有资源按技术领域（如网络协议、多媒体编码、系统内核、编程语言运行时）进行一级分类，并支持多级标签筛选，便于按上下文快速检索。

- **可用性健康检查**：系统定期对收录的 URL 执行 HTTP HEAD 请求与响应时间检测，标记异常链接并在文档中生成状态标识，确保参考资源的有效性。

- **版本化变更日志**：每次资源新增、移除或 URL 更新均记录在 CHANGELOG 中，保留完整的历史修改上下文，支持按时间线回溯。

- **社区提交工作流**：外部贡献者可通过标准 GitHub Pull Request 流程提交新资源，需附带分类建议与 50 字以内的摘要说明，由维护者 Review 后合并。

- **结构化元数据输出**：每个条目包含标题、描述、分类标签、添加日期与校验哈希，支持导出为 JSON 或 YAML 格式，便于其他工具链集成。

- **离线文档生成**：基于 MkDocs 构建静态站点，支持将整个资源列表与分类导航生成为可离线浏览的 HTML 文档，适用于内网环境部署。

- **URL 规范化校验**：自动检测并提示 URL 中的协议缺失、大小写不一致、尾部斜杠冗余等问题，引导贡献者按照本项目规定的硬性格式提交。

## 应用场景

- **技术调研阶段的参考源聚合**：当团队需要对某一技术方向（例如国产视频编码方案或在线字幕渲染引擎）进行横向对比时，可通过本项目的分类索引快速获取一批候选链接，减少盲目搜索的时间成本。

- **架构设计文档的外部引用管理**：在撰写系统设计说明书或技术决策记录时，工程师可以直接引用本项目中收录的稳定 URL，并利用变更日志功能确保引用源在后续迭代中可追溯。

- **离线环境下的资源预备**：对于网络隔离的开发测试环境，运维人员可利用本项目的离线文档生成功能，提前将常用技术参考站点打包带入内网，避免临时申请网络权限的流程阻塞。

- **开源项目 README 的外链维护**：开源维护者可将本项目作为上游资源池，从中选取稳定的技术参考链接嵌入自身项目的 README 或文档中，减少直接维护大量外链的负担。

- **技术培训与新手 onboarding 材料组织**：团队培训负责人可以使用本项目的分类体系快速搭建面向新员工的技术阅读清单，确保推荐资源的一致性与可维护性。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，帮助您在本地完成本项目的克隆、依赖安装与静态站点预览。

```bash
# 1. 克隆仓库
git clone https://github.com/terminus-catalog/terminus-catalog.git
cd terminus-catalog

# 2. 安装 Python 依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt

# 3. 运行本地开发服务器
mkdocs serve
# 浏览器访问 http://127.0.0.1:8000 预览站点
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Python | 3.9 及以上 | 用于运行 MkDocs 构建工具及本地校验脚本 |
| pip | 22.0 及以上 | Python 包管理器，用于安装依赖项 |
| MkDocs | 1.5.3 及以上 | 静态站点生成引擎，用于渲染文档与资源列表 |
| mkdocs-material | 9.5.0 及以上 | Material 主题，提供导航与搜索增强功能 |
| PyYAML | 6.0 及以上 | 用于解析资源元数据配置文件 |
| requests | 2.31.0 及以上 | 用于可用性健康检查脚本的 HTTP 请求 |
| Git | 2.30 及以上 | 版本控制，用于克隆及提交变更 |

## 文档导航

| 层面 | 目录路径 | 回答的问题 |
| :--- | :--- | :--- |
| 用户入门 | `docs/quickstart.md` | 如何快速浏览资源分类、如何使用搜索功能、如何提交新资源建议 |
| 维护者手册 | `docs/maintainer-guide.md` | 资源审核标准是什么、健康检查如何配置、如何处理 PR 冲突 |
| 分类体系 | `docs/taxonomy.md` | 当前有哪些一级分类、标签命名规范、分类调整的决策流程 |
| 贡献流程 | `docs/contributing.md` | PR 提交步骤、Commit Message 格式要求、DCO 签署方式 |
| API 集成 | `docs/api-reference.md` | 如何通过 JSON 接口获取资源列表、元数据字段含义、缓存策略 |
| 变更历史 | `CHANGELOG.md` | 每次资源增删改的详细记录与时间戳 |

## 资源列表

以下收录的链接均按照本项目的分类标准进行归集，涵盖多媒体处理、在线播放、字幕资源等多个技术子领域。所有 URL 均保持用户原始输入格式，不做任何协议补全或域名规范化处理。

### 多媒体与字幕资源

- <code>zhongwenzaixianzimumianfeigaoqing.org.cn</code>
- <code>zaixianbofangzhongwenzimu.org.cn</code>
- <code>zhongwenzimuzaixianmianfei.org.cn</code>

### 视频播放与流媒体

- <code>yirenguochanzaixianshipin.org.cn</code>
- <code>gaoqingshipinzaixianguankanw.org.cn</code>
- <code>meinvshipinzaixianguankan.org.cn</code>

### 特定主题视频资源

- <code>jiujiumitaozaixianbofang.org.cn</code>
- <code>yiquerzhongwenzimu.org.cn</code>

### 字幕与配音主题

- <code>zhongwenzimuzhifusiwang.org.cn</code>
- <code>zhongwenzimushaofurenqi.org.cn</code>

## 项目结构

```
terminus-catalog/
├── docs/                           # 文档根目录
│   ├── index.md                    # 首页介绍与快速导航
│   ├── quickstart.md               # 用户快速入门指南
│   ├── maintainer-guide.md         # 维护者操作手册
│   ├── taxonomy.md                 # 分类体系完整定义
│   ├── contributing.md             # 贡献者操作流程
│   ├── api-reference.md            # JSON/YAML 接口文档
│   └── resources/                  # 资源详情页面目录
│       ├── media.md                # 多媒体类资源列表
│       ├── streaming.md            # 流媒体类资源列表
│       └── subtitle.md             # 字幕类资源列表
├── scripts/                        # 工具脚本目录
│   ├── health_check.py             # 链接可用性批量检测脚本
│   ├── normalize_url.py            # URL 格式规范化校验工具
│   └── generate_metadata.py        # 从配置生成 JSON 元数据
├── config/                         # 配置文件目录
│   ├── categories.yaml             # 分类与标签层级定义
│   ├── resources.yaml              # 所有收录 URL 的主数据文件
│   └── maintainers.yaml            # 维护者列表及联系信息
├── tests/                          # 单元测试与集成测试目录
│   ├── test_health_check.py        # 健康检查逻辑测试
│   └── test_metadata_schema.py     # 元数据结构校验测试
├── CHANGELOG.md                    # 版本变更日志
├── LICENSE                         # MIT 许可证文本
├── README.md                       # 本文件
├── mkdocs.yml                      # MkDocs 站点配置文件
└── requirements.txt                # Python 依赖清单
```

## 贡献指南

我们欢迎并鼓励社区成员以多种方式参与本项目，包括但不限于提交新资源、修正已有链接、完善分类体系或改进文档。为确保协作流程清晰高效，请遵循以下步骤：

1.  **提交 Issue 进行讨论**：对于新增资源建议或分类调整，请先在 GitHub Issues 中创建一个类型为 `enhancement` 或 `resource-request` 的 Issue，说明建议理由、参考链接及预期分类路径。对于明显的链接失效修复，可直接进入步骤 2。

2.  **Fork 仓库并创建特性分支**：从主仓库的 `main` 分支 fork 到个人账户，然后本地创建以 `feature/` 或 `fix/` 为前缀的分支，例如 `feature/add-video-encoding-links`。

3.  **修改配置文件并本地验证**：在 `config/resources.yaml` 中按模板格式添加或修改条目。之后运行 `python scripts/normalize_url.py` 校验 URL 格式是否符合硬性规则，运行 `python scripts/health_check.py` 检测新链接的可用性。

4.  **提交 Pull Request 并签署 DCO**：提交 PR 时请填写对应的 Issue 编号，并在 Commit Message 中包含 `Signed-off-by: Your Name <email>` 行，以表示您接受 Developer Certificate of Origin。PR 描述中请列出本次变更的摘要与测试结果。

5.  **等待维护者 Review**：维护者将检查分类准确性、链接稳定性和文档一致性。若需修改，会在 PR 中提出反馈。合并后，变更将自动触发站点重建与部署。

## 常见问题

**问：如果发现某个收录的链接已经失效，应该如何处理？**

答：请先在仓库 Issues 中搜索是否已有相关报告。若无，请创建一个 `bug` 类型的 Issue，附上链接名称、失效时间（如已知）以及访问返回的 HTTP 状态码。维护者会尽快确认并移除或替换该链接。您也可以直接按照贡献指南提交 PR 进行修复，这将是更受推崇的方式。

**问：我提交的新资源链接被拒绝，常见原因有哪些？**

答：拒绝的主要原因包括：链接内容与技术主题无关或存在明显低质量内容（如大量广告弹窗）；链接指向的站点无法稳定访问或存在地域性屏蔽；提交的 URL 格式不符合本项目的硬性规则（例如缺少协议或包含不必要的尾部斜杠）；分类建议与现有体系严重冲突且未提前在 Issue 中讨论。我们建议在提交前仔细阅读 `docs/taxonomy.md` 中的分类定义。

**问：本项目是否提供 JSON 或 API 接口以便其他工具集成？**

答：是的。每次站点构建时，系统会根据 `config/resources.yaml` 自动生成 `docs/api/resources.json` 文件，包含所有条目的完整元数据（标题、分类、添加日期、状态等）。您可以直接通过 `https://terminus-catalog.github.io/api/resources.json` 获取该文件，或通过本地构建生成离线版本。详细字段说明请参阅 `docs/api-reference.md`。

## 许可证

本项目采用 MIT 许可证。您可以自由使用、修改、分发本项目的文档与配置代码，但请保留原始版权声明。具体条款请参阅仓库根目录下的 `LICENSE` 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
