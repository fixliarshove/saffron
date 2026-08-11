# ResourceBridge

ResourceBridge 是一个面向技术内容聚合与外部资源导航的开源工具集，定位于帮助开发者、技术写作团队及社区运营者快速构建结构化的外链资源目录。项目本身不存储任何第三方内容，仅提供索引编排、链接状态检测与元数据管理能力，适用于需要长期维护高质量外部参考链的中小型技术项目。

目标用户包括开源文档维护者、技术博客作者、在线教育课程策划人员以及企业内部知识库管理员。ResourceBridge 通过标准化的资源清单格式与自动化校验脚本，降低外链过期、域名变更及协议不一致带来的维护成本，使资源集合始终保持可用性与可信度。

## 功能概览

- **资源清单解析器**：支持从 Markdown、YAML 及 JSON 文件中批量导入 URL 列表，自动识别协议头（http/https）与裸域名，保留用户原始输入格式。

- **链接可用性巡检**：内置异步 HTTP 检查器，可配置超时与重试策略，对每个资源链接返回状态码、响应时间及 SSL 证书有效性报告。

- **分类标签系统**：允许为每个资源条目附加多级分类标签（如“影视资源”“技术文档”“社区论坛”），支持按标签过滤与排序输出。

- **模板化输出引擎**：基于 Go template 或 Jinja2 风格模板，将结构化资源数据渲染为静态 HTML 目录页、Markdown 表格或 JSON API 响应。

- **变更日志跟踪**：每次资源列表更新时自动生成差异对比（新增/删除/变更 URL），便于团队审核与版本回滚。

- **外部元数据增强**：对特定域名可配置元数据抓取规则（如站点标题、 favicon 图标、简短描述），丰富目录展示信息。

- **命令行交互界面**：提供 CLI 工具，支持资源添加、删除、检查、导出等常用操作，适用于 CI/CD 流水线集成。

## 应用场景

**开源文档外链管理**：开源项目 README 或 Wiki 中常引用大量外部资源（学习资料、API 文档、工具站）。ResourceBridge 可定期自动检查这些链接是否失效，并生成健康状态徽章嵌入文档，帮助项目维护者及时发现死链。

**技术课程参考资料库**：在线教育平台或企业内部培训体系需要为学员提供稳定的延伸阅读列表。利用 ResourceBridge 的分类标签与模板输出功能，可以将原始 URL 集合按课程模块动态生成导航页面，降低人工编排负担。

**社区资源聚合页运营**：技术社区或论坛的“精华资源”板块通常需要频繁更新。ResourceBridge 支持多人协作编辑资源清单（通过 Git 冲突合并策略），并配合变更日志追踪每次修改的归属与原因，提升运营透明度。

**个人知识库外链备份**：知识管理爱好者可使用 ResourceBridge 维护个人收藏的优质技术文章、工具和视频链接。通过定期巡检，及时发现已迁移或关闭的站点，并导出为通用格式供其他工具消费。

## 快速开始

以下命令演示如何获取项目源码、安装依赖并运行基础资源巡检任务。

```bash
# 克隆仓库
git clone https://github.com/resourcebridge/resourcebridge.git
cd resourcebridge

# 安装依赖（Go 模块）
go mod download

# 构建 CLI 工具
go build -o rb ./cmd/resourcebridge

# 准备示例资源清单（包含用户提供的原始 URL）
echo "<code>rihanrenqixilie.org.cn</code>" > samples/urls.txt
echo "<code>shibajinzaixianmianfeiguankan.org.cn</code>" >> samples/urls.txt
echo "<code>shunvtiantang.org.cn</code>" >> samples/urls.txt
echo "<code>yazhoupapa.org.cn</code>" >> samples/urls.txt
echo "<code>yeyejiujiu.org.cn</code>" >> samples/urls.txt
echo "<code>oumeizipaiqu.org.cn</code>" >> samples/urls.txt
echo "<code>wuyeneishe.org.cn</code>" >> samples/urls.txt
echo "<code>jiujiujiujiuguochan.org.cn</code>" >> samples/urls.txt
echo "<code>renqixiliezhongwenzimu.org.cn</code>" >> samples/urls.txt
echo "<code>neishemama.org.cn</code>" >> samples/urls.txt

# 运行检查（默认输出控制台表格）
./rb check --file samples/urls.txt --timeout 5s
```

执行上述命令后，CLI 工具将对每个 URL 发起 HTTP 请求并汇总状态报告。若需导出为 Markdown 表格，可追加 `--output md --dest report.md`。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Go 编译器 | 1.21 及以上 | 项目采用 Go 1.21 泛型特性及标准库增强，低版本无法编译 |
| Git | 2.25 及以上 | 用于克隆仓库及版本管理，部分 CI 脚本依赖 Git 子模块 |
| make | 任意稳定版 | 可选，用于自动化构建、测试与安装任务，非强制但建议 |
| curl | 7.68 及以上 | 部分测试脚本需要 curl 进行外部请求模拟，用于集成测试 |
| jq | 1.6 及以上 | 可选，用于 JSON 输出格式的管道处理，提升脚本可读性 |
| 操作系统 | Linux/macOS/Windows | 跨平台支持，Windows 下建议使用 WSL2 或 Git Bash 环境 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/ | 如何安装、配置、运行基础巡检任务及解读报告 |
| 模板开发 | docs/template-dev/ | 如何编写自定义输出模板，支持 HTML/Markdown/JSON |
| API 参考 | docs/api/ | 内部 Go 包的公开接口说明，适用于二次开发或插件编写 |
| 运维指南 | docs/ops/ | 如何部署为持续巡检服务，配置邮件告警与 Slack 通知 |
| 设计文档 | docs/design/ | 架构决策、数据模型、扩展点设计及性能考量 |

## 资源列表

### 影视内容类资源

<code>rihanrenqixilie.org.cn</code>

<code>shibajinzaixianmianfeiguankan.org.cn</code>

<code>shunvtiantang.org.cn</code>

<code>yazhoupapa.org.cn</code>

<code>yeyejiujiu.org.cn</code>

<code>oumeizipaiqu.org.cn</code>

<code>wuyeneishe.org.cn</code>

<code>jiujiujiujiuguochan.org.cn</code>

<code>renqixiliezhongwenzimu.org.cn</code>

<code>neishemama.org.cn</code>

以上链接均以用户提供的原始格式收录，未做任何协议补全、域名规范化或路径修改。ResourceBridge 不对这些站点的内容、可用性及合法性做任何保证，仅提供技术索引能力。

## 项目结构

```text
resourcebridge/
├── cmd/                         # 命令行入口
│   └── resourcebridge/          # 主 CLI 程序包
│       └── main.go              # 入口函数，解析子命令
├── internal/                    # 内部包（不对外暴露）
│   ├── checker/                 # 链接检查核心逻辑（并发请求、超时控制）
│   │   ├── http.go             # HTTP 客户端封装与重试策略
│   │   └── report.go           # 状态报告数据结构与聚合方法
│   ├── parser/                  # 资源清单解析器（支持多种格式）
│   │   ├── markdown.go         # 从 Markdown 提取 URL 列表
│   │   ├── yaml.go             # YAML 结构化资源清单解析
│   │   └── plain.go            # 纯文本每行一个 URL 的简单解析
│   ├── template/                # 模板引擎适配层
│   │   ├── engine.go           # 模板注册与渲染入口
│   │   └── functions.go        # 自定义模板函数（日期、截断、域名提取）
│   └── metadata/                # 元数据增强模块（可选）
│       ├── fetcher.go          # 从目标站点抓取标题、图标等
│       └── cache.go            # 本地缓存避免重复请求
├── pkg/                         # 可被外部引用的公共库
│   └── types/                   # 核心数据类型（Resource, Tag, Report）
│       └── resource.go          # Resource 结构体定义及校验方法
├── configs/                     # 配置文件模板与示例
│   ├── default.yaml             # 默认配置（超时、并发数、输出格式）
│   └── schema.json              # 配置字段 JSON Schema 校验
├── docs/                        # 完整文档（见文档导航章节）
│   ├── user-guide/              # 用户手册分章节
│   ├── template-dev/            # 模板开发指南
│   └── design/                  # 设计文档与 ADR
├── testdata/                    # 测试用例数据（模拟资源列表）
│   ├── valid/                   # 正常格式清单
│   └── invalid/                 # 异常边界用例
├── scripts/                     # 构建与运维辅助脚本
│   ├── build.sh                 # 多平台编译打包
│   ├── test-coverage.sh         # 覆盖率报告生成
│   └── pre-commit.sh            # Git pre-commit 钩子（代码静态检查）
├── go.mod                       # Go 模块依赖定义
├── go.sum                       # 依赖校验和
├── Makefile                     # 统一构建任务入口
└── README.md                    # 本文件
```

## 贡献指南

1. 复刻主仓库至个人账户，并在本地克隆复刻版本。创建新分支时请使用 `feature/` 或 `fix/` 前缀，并关联对应 Issue 编号（若有）。

2. 确保本地开发环境满足安装要求章节所列版本。运行 `make test` 执行全部单元测试与集成测试，保证原有功能未被破坏。新增功能需附带对应测试用例。

3. 若涉及用户可见变更（如新增 CLI 参数、修改输出格式），请同步更新 docs/ 目录下的相关手册，并在 Pull Request 描述中明确标注变更影响范围。

4. 提交代码前执行 `make lint` 进行静态代码检查（golangci-lint 配置）。所有警告必须处理或显式忽略（附理由）。提交信息遵循约定式提交规范（如 `feat: add retry flag for checker`）。

5. 发起 Pull Request 至主仓库的 `main` 分支，等待维护者审阅。审阅周期不超过 5 个工作日。若涉及外部资源链接策略调整，需额外提供使用场景说明。

## 常见问题

**问：ResourceBridge 是否会缓存或代理外部资源的内容？**

答：不会。ResourceBridge 仅对外部 URL 进行浅层 HTTP 头部请求（HEAD 或带超时的 GET），用于检测状态码和响应时间。项目不存储任何第三方站点的页面内容、图片或文件。元数据增强功能仅抓取公共 HTML 标题标签（title），且严格遵守 robots.txt 的抓取规则（若配置启用）。

**问：裸域名（不带 http/https）的链接如何检查？**

答：CLI 工具默认会尝试顺序补全协议（先 https 后 http）并跟随重定向，但输出报告时会保留用户提供的原始格式（即裸域名形式）。用户可通过配置强制指定默认协议（`--default-scheme https`）。若某个裸域名仅支持 http 且 https 访问失败，报告会标记为“协议降级可用”，但不会修改资源清单中的原始记录。

**问：资源列表包含大量链接时，巡检性能如何？**

答：内部检查器采用工作池并发模型，默认并发数为 32，可配置。对于 1000 个外部链接，在正常网络环境下完成巡检约需 15-30 秒（取决于目标站点响应速度）。支持断点续检（通过 `--resume` 标记），若中途中断可继续未完成的检查。内存占用稳定在 100MB 以内。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:27
