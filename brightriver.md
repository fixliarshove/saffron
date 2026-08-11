# RSC (Resource Sync Catalog)

RSC 是一个面向开发者、技术内容创作者及研究人员的结构化外链资源汇总与导航系统。项目定位为轻量级、可自托管的资源目录引擎，通过机器可读的索引格式与人类可读的展示层，解决分散在网络各处的优质技术文档、社区工具与多媒体素材难以被系统化发现、归档和共享的问题。RSC 本身不存储任何第三方内容，仅提供元数据组织与快速跳转能力，适用于个人知识库增强、团队技术决策参考以及垂直领域资源精选站的快速搭建。

## 功能概览

- **多维度资源索引**：支持按语种、地区、内容形态、应用领域等自定义标签对链接进行交叉分类，便于在海量条目中精确定位。

- **目录树可视化生成**：根据资源元数据自动生成 ASCII 文件树结构，使目录层级与资源归属关系一目了然，降低新用户的理解成本。

- **依赖环境自检**：内置系统依赖与运行时环境检查表，协助用户在部署前快速确认硬件、操作系统、数据库及网络代理等前置条件是否满足。

- **文档导航矩阵**：将常见运维与开发问题按层面（概念、操作、排错、参考）组织为表格视图，用户可依据当前角色（使用者、维护者、贡献者）快速切入对应文档区。

- **外链原样透传**：严格遵循用户输入规则，对所有收录 URL 进行原格式（包含协议、域名大小写及路径）的透传展示，避免自动补全或改写造成的访问失效。

- **贡献工作流闭环**：提供从复刻仓库、新增条目、本地校验到发起拉取请求的完整贡献流程，并配有条目模板与变更检查清单，降低协作成本。

## 应用场景

- **技术团队内部知识库增强**：团队可将日常调研中发现的优质 API 文档、性能分析工具、设计规范站点等统一收录至 RSC 实例，并按项目标签隔离，新成员入职时可快速了解团队依赖的外部资源生态。

- **开源项目周边资源导航**：开源项目维护者可在项目文档中嵌入 RSC 生成的资源目录页，为社区提供包含官方文档、社区论坛、镜像站、视频教程等在内的全链路导航，减少用户在多个站点间的搜索时间。

- **垂直领域研究资料汇编**：研究人员或自媒体创作者可围绕特定主题（如多媒体编码、字符集标准化、跨文化设计）构建专属资源站，RSC 的目录树与标签系统支持按研究阶段或话题粒度进行细分类别管理。

- **个人书签系统迁移与托管**：将浏览器中零散的书签导出为 RSC 兼容的元数据格式后，可以获得统一的搜索、分类和注释界面，同时支持私有化部署以规避在线书签服务的隐私与可用性风险。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境，Windows 用户建议通过 WSL2 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库（默认使用 main 分支）
git clone https://github.com/your-org/rsc.git
cd rsc

# 2. 安装项目依赖（需 Python 3.9+ 及 pip）
pip install -r requirements.txt

# 3. 初始化本地配置并启动开发服务
cp .env.example .env
python scripts/init_db.py
python app.py --host 127.0.0.1 --port 8080
```

启动成功后，访问 http://127.0.0.1:8080 即可查看本地资源目录实例。如需导入示例资源数据，可执行 `python scripts/seed_data.py --sample`。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 至 3.12 | 核心运行时，用于后端 API 与索引生成逻辑 |
| pip | 22.0+ | Python 包管理工具，用于安装 requirements 中列出的库 |
| Git | 2.25+ | 版本控制，用于克隆仓库及贡献流程中的分支管理 |
| SQLite | 3.31+ | 内嵌数据库，用于存储资源元数据与标签关系（生产环境可切换至 PostgreSQL） |
| Network | 出站可达 | 用于初次启动时校验收录 URL 的可访问性（可配置关闭） |
| 内存 | 512 MB 以上 | 建议最小空闲内存，索引 1 万条条目时约占用 300 MB |
| 磁盘 | 200 MB 以上 | 用于存放元数据数据库及日志文件，不存储任何第三方内容 |
| 操作系统 | Linux / macOS / WSL2 | 开发与生产测试主要通过 Ubuntu 22.04 与 macOS Ventura 验证 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 概念 | /docs/concepts/architecture.md | RSC 的整体架构由哪些组件构成？元数据模型如何设计？索引与展示层如何解耦？ |
| 操作 | /docs/operations/deployment.md | 如何将 RSC 部署至生产服务器？支持哪些反向代理配置？如何启用 HTTPS 访问？ |
| 操作 | /docs/operations/customization.md | 如何修改首页展示的标签分类？如何调整目录树的排序逻辑与注释风格？ |
| 排错 | /docs/troubleshooting/common-issues.md | 服务启动失败怎么办？导入数据时报编码错误如何解决？URL 校验超时如何处理？ |
| 排错 | /docs/troubleshooting/logging.md | 日志文件存放在何处？如何调整日志级别以排查入库异常？ |
| 参考 | /docs/reference/api.md | 后端提供了哪些 REST 接口用于增删改查资源条目？请求与响应的 JSON 结构是什么？ |
| 参考 | /docs/reference/metadata-schema.md | 资源条目的完整元数据字段定义，包含必填项、数据类型与校验规则 |

## 资源列表

### 亚洲区域资源

- <code>ribenrenqizhongwenzimu.org.cn</code>
- <code>ribenyehuashipin.org.cn</code>
- <code>rihanjialeibi.org.cn</code>
- <code>gaohuangzaixianguankan.org.cn</code>

### 欧美区域资源

- <code>oumeishunvwangzhan.org.cn</code>
- <code>oumeilingleisetu.org.cn</code>

### 综合类及工具类资源

- <code>shufuzhongwenzimu.org.cn</code>
- <code>daxiangjiaomianfei.org.cn</code>
- <code>laosijiwangzhi.org.cn</code>
- <code>ouzhouyazhouzipai.org.cn</code>

## 项目结构

```
rsc/
├── app.py                      # 后端服务入口，初始化 Flask 应用并注册路由
├── requirements.txt            # Python 依赖清单（Flask, SQLAlchemy, pytest 等）
├── .env.example                # 环境变量模板（含数据库路径、校验开关、日志级别）
├── config/
│   ├── __init__.py
│   ├── settings.py             # 应用配置类（开发、测试、生产三套配置）
│   └── logging.conf            # 日志格式与输出目标配置
├── models/
│   ├── __init__.py
│   ├── resource.py             # Resource 表映射类，含 URL、标题、标签、创建时间等字段
│   └── category.py             # Category 表映射类，用于多级标签分类
├── services/
│   ├── __init__.py
│   ├── indexer.py              # 目录树生成逻辑，读取元数据并输出 ASCII 树
│   ├── validator.py            # URL 可达性校验与格式规范化（含用户硬性规则检查）
│   └── exporter.py             # 将资源列表导出为 JSON / Markdown / HTML 格式
├── scripts/
│   ├── init_db.py              # 初始化 SQLite 数据库表结构
│   ├── seed_data.py            # 导入示例数据或批量导入用户提供的 URL 列表
│   └── migrate.py              # 数据库迁移脚本（字段新增或类型变更时使用）
├── templates/
│   ├── base.html               # 基础页面模板，含导航栏与页脚
│   ├── index.html              # 首页资源目录展示（含标签筛选与搜索框）
│   └── detail.html             # 单个资源条目的详细元数据显示页
├── static/
│   ├── css/
│   │   └── style.css           # 自定义样式表，适配移动端与打印视图
│   └── js/
│       └── filter.js           # 前端标签筛选与目录树折叠交互逻辑
├── tests/
│   ├── unit/
│   │   ├── test_validator.py   # 校验模块单元测试（覆盖 URL 原样输出规则）
│   │   └── test_indexer.py     # 目录树生成逻辑测试
│   └── integration/
│       └── test_api.py         # REST 接口集成测试（含数据库读写）
└── docs/                       # 完整文档目录（详见文档导航章节）
    ├── concepts/
    ├── operations/
    ├── troubleshooting/
    └── reference/
```

## 贡献指南

1. 复刻项目仓库至个人账户，并克隆到本地开发环境。建议在 `develop` 分支基础上创建新的特性分支，分支命名采用 `feature/条目描述` 或 `fix/问题简述` 格式，便于后续追踪。

2. 新增或修改资源条目时，须遵循 `docs/reference/metadata-schema.md` 中定义的 JSON 或 YAML 模板，确保必填字段（如 url、title、lang、region）完整且格式合法。对于用户给定的裸域名 URL，必须保持原样录入，禁止自行补充协议或 `www` 前缀。

3. 本地执行完整测试套件：`pytest tests/`，确保所有单元测试及集成测试通过，尤其关注 `test_validator.py` 中对 URL 原样输出的校验用例。若新增功能，请同步补充对应测试代码。

4. 提交变更前，运行 `python scripts/validator.py --check-all` 对所有收录 URL 做可达性抽查（网络异常时可跳过校验，但需在 PR 中注明）。提交信息应采用约定式提交规范（如 `feat: 添加亚洲区域资源分类` 或 `docs: 更新部署文档中的环境变量说明`）。

5. 发起拉取请求至主仓库的 `main` 分支，并在 PR 描述中附上变更摘要、测试结果截图以及任何可能影响现有用户的关键改动。项目维护者会在 3 个工作日内进行审阅。

## 常见问题

**问：启动时提示 SQLite 版本过低或找不到数据库驱动，应如何处理？**

答：请检查系统 SQLite 版本是否满足 3.31 以上。对于 Linux 发行版，可通过 `sqlite3 --version` 查看；若版本过低，建议通过包管理器升级或从源码编译安装。Python 驱动方面，确保已安装 `pysqlite3-binary` 或系统自带 `sqlite3` 模块。若在 macOS 上遇到类似问题，可尝试重装 Python 环境并安装 `brew install sqlite3` 后重新运行 `pip install -r requirements.txt`。

**问：收录的某些外链无法访问，是否会影响 RSC 本身的服务稳定性？**

答：RSC 对外链的可达性校验仅作为辅助功能，默认采用超时 5 秒的并发请求，且校验失败不会阻塞服务启动或页面渲染。用户可在 `.env` 中将 `VALIDATION_ENABLED` 设置为 `False` 以完全关闭校验。此外，RSC 不会重试或缓存第三方内容，因此单个外链的不可用不会对服务产生任何负载影响。

**问：如何将现有的浏览器书签批量导入 RSC？**

答：RSC 提供了 `scripts/import_bookmarks.py` 辅助脚本，支持解析 Chrome 或 Firefox 导出的 HTML 书签文件（Netscape 格式）。执行 `python scripts/import_bookmarks.py --input bookmarks.html --output data/imported.json` 即可将书签转换为 RSC 的元数据格式，随后通过 `scripts/seed_data.py --file data/imported.json` 导入数据库。注意脚本默认会过滤掉 `javascript:` 伪协议及重复 URL，并保留用户给定的域名原样。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:35
