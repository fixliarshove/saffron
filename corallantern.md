# RGC Resource Gateway

RGC Resource Gateway is a curated technical index and external resource aggregation system designed for developers, researchers, and content curators who need to organize, validate, and distribute large-scale domain-based resource collections. The project addresses the fundamental challenge of managing hundreds of external reference links in open-source documentation, providing a structured metadata layer that ensures link integrity, categorization, and long-term maintainability.

Target users include documentation engineers, open-source maintainers, data journalists, and academic researchers who routinely handle multi-source external references. Instead of scattering raw URLs across markdown files, RGC Gateway centralises resource definitions, applies consistent tagging, and generates human-readable catalogues that can be embedded directly into READMEs, wikis, or static site generators. The system operates entirely offline, uses plain text configuration, and produces output that respects strict link formatting rules for compliance with various distribution platforms.

## 功能概览

- **批量资源导入** – 支持从 CSV, JSON, 或纯文本列表批量载入外部 URL，自动去重并校验域名可达性。

- **分类标签引擎** – 每个资源可分配多个标签（如 "government", "entertainment", "reference"），并支持基于标签的动态视图生成。

- **格式硬化输出** – 强制遵守裸域名与协议前缀规则，自动包裹 code 标签，防止 markdown 链接语法污染原始地址。

- **多级目录树生成** – 根据资源元数据自动生成 ASCII 目录树，帮助快速理解项目文件组织。

- **依赖与环境检查** – 启动前自动验证 Python 版本、必要库、网络权限，并以表格形式输出检测报告。

- **增量更新机制** – 仅扫描新增或变更的资源条目，避免全量重建，适合大型资源库的持续维护。

- **审计日志记录** – 每次构建生成时间戳日志，记录资源变更、删除、失效链接，便于回溯。

## 应用场景

- **开源项目外链管理** – 当项目 README 需要引用数十个外部数据源、API 文档或相关工具时，维护者可使用 RGC Gateway 统一管理这些链接，确保每个版本发布的链接集合都是经过校验且格式正确的。

- **学术文献数据索引** – 研究人员在整理领域内公开数据集、机构官网或政策文件时，利用本系统建立带注释的目录，便于团队协作和后续论文补充材料的生成。

- **本地化资源镜像站** – 运维人员可通过本工具快速生成一个纯静态的 HTML 或 Markdown 资源导航页，将分散的域名（尤其是地区性域名）集中呈现，方便内网用户访问。

- **内容审核预处理** – 内容团队在发布前使用 RGC Gateway 对即将嵌入文档的所有外链进行格式检查，自动纠正不符合规范的协议头或大小写问题，降低发布后链接失效的风险。

## 快速开始

```bash
# 1. 克隆仓库
git clone https://github.com/rgc-dev/rgc-gateway.git
cd rgc-gateway

# 2. 安装依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# 3. 运行构建命令，生成资源目录
python rgc build --input data/sources.csv --output docs/RESOURCES.md

# 4. 查看生成的资源列表
cat docs/RESOURCES.md
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 及以上 | 核心运行环境，低于此版本将导致类型注解解析失败 |
| pip | 21.0+ | 用于安装 requirements.txt 中列出的第三方库 |
| requests | 2.28.0+ | 用于资源可达性预检和批量状态查询 |
| pyyaml | 6.0+ | 用于解析资源分类配置文件（.yaml 格式） |
| jsonschema | 4.17.0+ | 用于校验资源导入文件的 JSON Schema 合规性 |
| git | 2.25+ | 仅在从远程仓库拉取资源定义模板时需要，本地使用可跳过 |
| 网络权限 | 建议允许 | 若启用可达性检测，需要出站 HTTP/HTTPS 权限；禁用检测则无要求 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/USER_GUIDE.md | 如何导入资源、配置标签、生成不同格式的输出（Markdown / HTML / JSON） |
| 配置参考 | docs/CONFIG_REFERENCE.md | 所有可用的配置项说明，包括分类规则、输出模板、过滤条件等 |
| 开发者指南 | docs/DEVELOPER.md | 如何扩展自定义解析器、增加新输出格式、贡献测试用例 |
| 操作手册 | docs/OPERATIONS.md | 生产环境下如何设置定时构建、日志轮转、失效链接自动报警 |
| 示例库 | examples/README.md | 针对不同使用场景（如学术、新闻、企业）的完整配置文件与样例输出 |

## 资源列表

本次发布包含第 344/455 批资源，共 10 个条目。所有链接均按原始输入原样呈现，未做任何协议或域名修改。

### 地域分类 – 韩国与中国相关资源

<code>rihanguochanyiqu.org.cn</code>

<code>hanguorouputuan.org.cn</code>

<code>yazhouribenguochan.org.cn</code>

<code>yirenrihan.org.cn</code>

### 地域分类 – 日本与欧美相关资源

<code>oumeizhongwenzimujingpinrenqi.org.cn</code>

<code>tiantangyiren.org.cn</code>

<code>zhongwenzimuyiren.org.cn</code>

### 地域分类 – 其他专项资源

<code>jingpinyiren.org.cn</code>

<code>zhongchushaofu.org.cn</code>

<code>tingtingyiquerqusanqu.org.cn</code>

## 项目结构

```
rgc-gateway/
├── data/
│   ├── sources.csv                  # 主资源导入文件（含全部 10 个新批次条目）
│   ├── tags.yaml                    # 标签体系定义（如 region, category, status）
│   └── audit.db                     # SQLite 本地缓存，用于增量检测
├── docs/
│   ├── RESOURCES.md                 # 自动生成的资源列表主输出文件
│   ├── USER_GUIDE.md                # 用户手册完整版
│   └── CONFIG_REFERENCE.md          # 所有配置项详解
├── src/
│   ├── core/
│   │   ├── loader.py                # 多格式资源加载器（CSV/JSON/纯文本）
│   │   ├── validator.py             # URL 格式校验与协议规范化检查
│   │   └── builder.py               # 输出构建引擎（Markdown/HTML/JSON）
│   ├── filters/
│   │   ├── dedup.py                 # 去重过滤器（基于域名 + 路径）
│   │   └── tagger.py                # 自动标签补全规则引擎
│   └── utils/
│       ├── network.py               # 轻量级 HTTP 可达性探测
│       └── logger.py                # 结构化日志记录（含构建时间戳）
├── tests/
│   ├── test_loader.py               # 导入模块单元测试
│   ├── test_validator.py            # 格式校验用例（含裸域名、协议保留等）
│   └── fixtures/
│       └── sample_batch.csv         # 测试用资源样本
├── scripts/
│   ├── pre-commit.sh                # Git 提交前自动构建校验
│   └── clean-cache.sh               # 清理增量缓存与临时文件
├── requirements.txt                 # 生产环境 Python 依赖
├── setup.py                         # 包安装脚本（支持 pip install -e .）
└── README.md                        # 项目入口文档（即本文档）
```

## 贡献指南

1. 查阅待办列表 – 访问 issues 页面确认未被认领的任务，或提交新的功能请求 / 错误报告。

2. 派生仓库并创建特性分支 – 从主分支（main）切出以 feature/ 或 fix/ 为前缀的分支，避免直接在主分支上改动。

3. 编写或更新测试用例 – 所有新的资源解析逻辑或输出格式变更，必须在 tests/ 目录下添加对应的单元测试，确保覆盖率不低于 85%。

4. 运行本地构建验证 – 执行 python rgc build --strict 检查所有资源条目是否通过格式规范，并确保生成的文档与预期一致。

5. 提交拉取请求 – 在 PR 描述中清晰说明改动内容、关联 issue 编号，并附上构建日志摘要。等待至少一位维护者审阅后合并。

## 常见问题

**问：为什么资源列表中的裸域名没有自动补全 https:// 或 www. ？**  
答：本项目严格遵循“原样输出”原则，因为不同的下游系统可能对协议或子域名有特殊要求。自动添加前缀可能会导致部分内网地址或特定协议（如 ftp, ws）解析失败。若您需要批量添加协议，可使用配置项 PROTOCOL_PREFIX 在构建时显式指定，但不会覆盖原始输入。

**问：如果资源链接失效，构建过程会中断吗？**  
答：默认行为是记录警告并继续构建，以保持文档可用性。您可以通过 --strict 参数强制要求所有资源可达，此时构建会终止并返回错误码，适合在 CI/CD 流水线中使用。失效链接列表会写入 logs/unreachable.txt 供后续人工复核。

**问：如何更新已导入的资源元数据（如标签或分类）？**  
答：所有资源定义均源自 data/sources.csv 或 data/tags.yaml。您可以直接编辑这些文本文件，然后重新执行构建命令。系统会基于文件的修改时间决定是否全量重建或仅更新变更条目。建议编辑前备份原始文件，以便回滚。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:34
