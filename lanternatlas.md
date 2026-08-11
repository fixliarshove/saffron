# ResourceBridge

ResourceBridge 是一个面向技术内容聚合与外部资源治理的开源工具集，专注于解决多源、多类型、多版本外部链接在项目文档、学习路径与知识库体系中的引用一致性、可维护性与可审计性问题。项目定位为技术资源外链的中控层，适用于需要大规模管理外部参考链接的技术团队、文档站点与开源社区内容运营者。

ResourceBridge 不提供新的协议或解析标准，而是围绕现有 URL 结构、域名分级体系与内容分类策略，构建一套轻量化的链接登记、校验、分组与导出机制。项目核心目标用户为技术文档工程师、开源项目维护者、社区运营人员以及知识管理平台的架构师。

---

## 功能概览

- 链接登记与去重：支持批量导入外部链接，自动识别重复条目并生成冲突报告。
- 域名分级标注：根据域名后缀、子域结构自动标注链接所属区域或组织类型。
- 状态校验与存活检测：提供可配置的 HTTP 状态检查，标记失效或重定向链接。
- 分类标签系统：允许用户自定义标签，支持多维度筛选与组合查询。
- 导出适配器：内置 Markdown、JSON、CSV 三种导出格式，适配不同文档生成链。
- 变更审计日志：记录每次链接增删改操作，支持回滚与差异对比。
- 命令行交互与脚本集成：提供完整的 CLI 接口，便于嵌入 CI/CD 或文档构建流水线。
- 配置热加载：支持运行时动态调整校验超时、重试次数与白名单规则。

---

## 应用场景

- 技术文档外部参考管理：当项目文档引用大量第三方规范、论文或工具站点时，使用 ResourceBridge 统一登记并定期校验，避免文档中出现死链。
- 社区资源聚合页维护：开源社区常维护“生态工具”“相关项目”等聚合页面，通过 ResourceBridge 分类打标后自动生成最新列表，减少手工更新负担。
- 知识库外部依赖审计：企业内部知识库依赖大量外部链接，ResourceBridge 可生成审计报告，标注高风险或过期域名，辅助合规与安全审查。
- 多版本文档链接迁移：当外部站点改版或切换协议时，ResourceBridge 支持批量替换规则配置，快速适配历史文档中的链接变更。
- 开源项目 README 外链治理：直接在项目根目录集成 ResourceBridge 校验流程，确保每次发布前 README 及文档目录中的所有外部链接均为有效状态。

---

## 快速开始

以下指令适用于 Linux 与 macOS 环境，Windows 用户可使用 WSL 或 Git Bash。

```bash
# 克隆项目仓库
git clone https://github.com/resourcebridge/resourcebridge.git

# 进入项目目录
cd resourcebridge

# 安装依赖（基于 Python 3.10+）
pip install -r requirements.txt

# 初始化配置目录与示例数据
python -m resourcebridge init --sample

# 运行默认校验任务（检查示例链接列表）
python -m resourcebridge check --input samples/links.txt --output reports/
```

---

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.10 或更高 | 核心运行环境，低于此版本将无法解析类型注解与异步语法 |
| pip | 22.0 或更高 | 用于安装依赖包及后续扩展模块 |
| aiohttp | 3.9.0 或更高 | 异步 HTTP 请求库，用于链接存活检测 |
| click | 8.1.0 或更高 | 命令行界面框架，提供子命令与参数解析 |
| pyyaml | 6.0 或更高 | 配置文件解析，支持 YAML 格式的自定义规则 |
| pytest | 7.4.0 或更高 | 仅开发测试需要，生产环境可不安装 |

---

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user/guide.md | 如何安装、配置、运行基本校验与导出任务 |
| 配置参考 | docs/user/config.md | 配置文件完整字段说明、默认值与示例片段 |
| 命令参考 | docs/user/cli.md | 所有 CLI 子命令、选项参数与环境变量 |
| 开发指南 | docs/dev/architecture.md | 模块划分、数据流、扩展点与单元测试编写方法 |

---

## 资源列表

以下为 ResourceBridge 项目当前登记并定期校验的外部资源链接，按内容类别分组。所有链接均保留用户提供的原始格式，未做任何协议、域名或路径修改。

类别：综合资源

- <code>rihanyiren.org.cn</code>
- <code>oumeijiujiu.org.cn</code>
- <code>madoujingpin.org.cn</code>

类别：亚洲区域内容

- <code>yazhouchengrenzhongwenzimu.org.cn</code>
- <code>yazhouchengrenyiqu.org.cn</code>
- <code>jiujiumitao.org.cn</code>
- <code>yazhououmeijingpin.org.cn</code>
- <code>guochanoumeijingpin.org.cn</code>
- <code>yazhouyiquzhongwenzimu.org.cn</code>
- <code>yirenyiqu.org.cn</code>

---

## 项目结构

```
resourcebridge/
├── src/                                # 核心源代码目录
│   └── resourcebridge/                 # 主包路径
│       ├── __init__.py                 # 版本号与导出符号
│       ├── cli/                        # 命令行子命令实现
│       │   ├── __init__.py
│       │   ├── check.py                # check 子命令：存活校验逻辑
│       │   ├── export.py               # export 子命令：格式导出
│       │   └── init.py                 # init 子命令：初始化配置与样例
│       ├── core/                       # 核心数据模型与状态管理
│       │   ├── __init__.py
│       │   ├── registry.py             # 链接注册表类，管理增删改查
│       │   ├── validator.py            # 校验引擎，含超时与重试策略
│       │   └── tagger.py               # 标签系统，支持规则自动标注
│       ├── parsers/                    # 输入解析器
│       │   ├── __init__.py
│       │   ├── text_parser.py          # 纯文本列表解析
│       │   └── markdown_parser.py      # 从 Markdown 提取链接
│       ├── exporters/                  # 导出适配器
│       │   ├── __init__.py
│       │   ├── json_exporter.py
│       │   ├── csv_exporter.py
│       │   └── markdown_exporter.py
│       └── utils/                      # 通用工具函数
│           ├── __init__.py
│           ├── network.py              # 异步 HTTP 工具
│           └── logger.py               # 日志配置与格式化
├── tests/                              # 单元测试与集成测试
│   ├── conftest.py                     # pytest 夹具与全局配置
│   ├── test_registry.py
│   ├── test_validator.py
│   └── test_exporters.py
├── samples/                            # 示例数据
│   ├── links.txt                       # 示例链接列表
│   └── config.yaml                     # 示例配置文件
├── docs/                               # 用户与开发文档
│   ├── user/
│   │   ├── guide.md
│   │   ├── config.md
│   │   └── cli.md
│   └── dev/
│       └── architecture.md
├── requirements.txt                    # 生产依赖
├── requirements-dev.txt                # 开发额外依赖
├── setup.py                            # 安装打包配置
└── README.md                           # 项目入口文档（本文件）
```

---

## 贡献指南

1. 查阅问题列表与路线图：访问 GitHub Issues 板块，确认当前待处理任务或提议的新特性，避免重复工作。
2. 派生项目并创建特性分支：从主仓库派生至个人账户，基于 main 分支新建 feature/xxx 或 fix/xxx 格式的分支。
3. 编写或更新单元测试：所有新功能或缺陷修复必须附带对应测试用例，确保覆盖率不低于 90%。
4. 运行完整测试套件：在提交前执行 pytest 命令，确保本地所有测试通过且无回归错误。
5. 提交拉取请求：填写标准 PR 模板，清晰描述变更内容、测试结果与影响范围，等待维护者审阅。

---

## 常见问题

问：校验时出现大量超时错误，如何调整？
答：可在配置文件或命令行中通过 --timeout 参数增加单次请求超时秒数，默认值为 5 秒。同时可调整 --retry 参数设置重试次数。若仍频繁超时，建议检查网络环境或使用代理配置。

问：能否只校验部分链接而跳过其他条目？
答：支持通过 --filter 或 --tag 参数按标签筛选链接。您也可以维护多个输入文件，分别执行校验任务，实现分批处理。

问：导出的 Markdown 列表是否保留原始链接格式？
答：是的，导出适配器默认保持原始 URL 字符串不变，不自动追加协议前缀、尾部斜杠或 www 子域。若需格式化，可配置 export 子命令的 --format-rule 参数。

---

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
