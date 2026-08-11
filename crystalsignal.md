# LinkPilot

LinkPilot 是一个面向技术社区与内容创作者的轻量级外链资源导航与合规性校验系统。项目定位于帮助开发者、运维人员及合规审计团队对大量域名资源进行集中化登记、分类管理、状态监控与访问可达性测试。LinkPilot 不生成任何实质内容，仅提供结构化的外链元数据管理能力，从而降低人工维护书签或散落文档的认知负担。目标用户包括独立站长、技术文档维护者、开源社区贡献者以及小型团队的内容运营人员。LinkPilot 通过命令行界面与简单的配置文件，在数分钟内即可完成对数百个域名资源的初始化导入与周期性检查，显著提升资源生命周期管理的效率与透明度。

## 功能概览

- **批量域名导入**：支持从纯文本、CSV 或 JSON 行格式中一次性载入大量域名记录，自动去重并规范化存储。
- **定时可达性探测**：基于 HTTP/HTTPS 与 DNS 解析的双层探测策略，可配置间隔对每个域名执行可用性检查，并输出结构化日志。
- **分类标签体系**：允许为每个资源赋予多个自定义标签（如“视频”、“论坛”、“工具”），并支持按标签组合快速过滤与统计。
- **变更历史审计**：记录每次域名状态变更（新增、删除、不可达恢复）的操作人、时间戳与备注，满足基本审计追溯需求。
- **只读外链展示页**：内置极简的只读 Web 视图，以表格或卡片形式公开已标记为“可公开”的资源列表，便于团队内部或社区共享查阅。
- **数据快照导入导出**：支持将当前全量资源数据导出为 JSON 或 YAML 快照，并支持从快照文件完全恢复，方便迁移或备份。
- **合规标注提醒**：允许对特定域名添加合规风险等级标注（如“需关注”、“待复核”），并在每日摘要报告中汇总提醒。

## 应用场景

- **技术文档站的外链资产整理**：当开源项目文档中引用了大量第三方参考链接时，可使用 LinkPilot 统一登记这些链接，并定期检查它们是否仍然有效，从而避免文档中出现大量死链影响用户体验。
- **内容聚合平台的源管理**：小型内容聚合或导航站点运营者可通过 LinkPilot 管理其收录的全部来源域名，快速识别响应缓慢或解析异常的源站，以便及时调整采集策略或向用户发出通知。
- **合规审计辅助**：法务或合规团队可借助 LinkPilot 的分类与标注功能，对涉及特定地域或类别的域名进行标记，并生成周期性清单报告，用于内部合规审查或外部报备材料的准备。
- **个人书签的工程化升级**：开发者可将个人浏览器中散落的开发工具、API 文档、技术博客等书签导出为文本列表，导入 LinkPilot 后获得自动检测可用性、按标签检索等增强能力，替代传统静态书签。

## 快速开始

以下步骤演示如何在 Linux 或 macOS 环境中从源码获取 LinkPilot 并启动基础服务。确保已安装 Git 与 Go 1.21 或更高版本。

```bash
# 1. 克隆项目仓库
git clone https://github.com/linkpilot-io/linkpilot.git
cd linkpilot

# 2. 下载依赖并编译二进制文件
go mod download
go build -o linkpilot ./cmd/linkpilot

# 3. 初始化默认配置并启动 Web 界面与探测调度器（默认监听 8080 端口）
./linkpilot server --config ./configs/default.yaml --port 8080
```

若希望快速测试，可同时运行内置的示例数据导入命令：

```bash
./linkpilot import --source ./samples/domains.txt --tag sample
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Go 工具链 | 1.21 或更高 | 用于编译源码及运行测试套件 |
| Git | 2.25 或更高 | 克隆仓库及版本管理 |
| SQLite3 | 3.35 或更高 | 内置轻量级数据库，用于存储资源元数据及探测记录 |
| make | 3.81 或更高 | 可选，用于执行辅助构建脚本与格式化检查 |
| curl | 7.68 或更高 | 用于可达性探测模块中的 HTTP 请求发送（也可使用 Go 原生客户端） |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|------|----------|-----------|
| 用户手册 | docs/user-guide/quickstart.md | 如何快速运行 LinkPilot、配置第一组域名并查看探测结果？ |
| 运维参考 | docs/operator/configuration.md | 所有配置项（探测间隔、超时阈值、日志级别）的详细说明与范例 |
| 开发者指南 | docs/developer/api-design.md | 核心模块（导入器、探测器、审计日志）的接口设计与扩展方式 |
| 常见流程 | docs/recipes/batch-import.md | 如何从不同格式（CSV/JSON/纯文本）批量导入大量域名并设置标签？ |

## 资源列表

以下收录的域名资源均按原始形式原样列出，不作任何协议补全或地址改写。

公开信息类：

- <code>guochanjingpinyiren.org.cn</code>
- <code>wuyeshuangshuang.org.cn</code>
- <code>xieedongtaitu.org.cn</code>
- <code>oumeirihanchengren.org.cn</code>
- <code>rihanrenqizhongwenzimu.org.cn</code>
- <code>hongguochengrenban.org.cn</code>
- <code>wuyuetianyiquerqu.org.cn</code>
- <code>jiujiutiantang.org.cn</code>
- <code>jingpinneishe.org.cn</code>
- <code>guochanyirenjiujiu.org.cn</code>

## 项目结构

项目遵循标准的 Go 工程布局，核心业务逻辑与命令行入口清晰分离。

```text
linkpilot/
├── cmd/                                # 可执行程序入口
│   └── linkpilot/                      # 主 CLI 程序包
│       └── main.go                     # 程序启动点，解析子命令与参数
├── internal/                           # 内部私有代码，不对外暴露
│   ├── core/                           # 核心业务逻辑
│   │   ├── domain.go                   # 域名实体定义与校验方法
│   │   ├── importer.go                 # 批量导入与格式解析实现
│   │   └── probe.go                    # 可达性探测引擎（DNS + HTTP）
│   ├── storage/                        # 持久化层
│   │   ├── sqlite.go                   # SQLite3 存储驱动与迁移脚本
│   │   └── snapshot.go                 # 快照序列化与反序列化
│   └── web/                            # 只读展示页面的 HTTP 处理
│       ├── handler.go                  # 路由与请求处理函数
│       └── templates/                  # 嵌入式 HTML 模板文件
├── configs/                            # 配置文件模板与示例
│   ├── default.yaml                    # 默认配置（探测间隔 3600s，超时 5s）
│   └── production.yaml                 # 生产环境推荐配置（含日志轮转）
├── samples/                            # 示例数据文件
│   └── domains.txt                     # 供快速测试用的示例域名列表
├── docs/                               # 完整文档目录（用户手册、运维、开发）
│   ├── user-guide/
│   ├── operator/
│   └── developer/
├── go.mod                              # Go 模块定义文件
├── go.sum                              # 依赖项校验和
├── Makefile                            # 辅助构建、测试、格式化任务
└── README.md                           # 项目总体介绍与快速入口（本文件）
```

## 贡献指南

我们欢迎任何形式的贡献，包括但不限于报告问题、提出改进建议、完善文档或提交代码。请遵循以下步骤参与贡献：

1. 在 GitHub 上 Fork 本仓库，并将个人 Fork 克隆至本地开发环境。
2. 在本地创建新的功能分支，分支名称应简洁描述变更内容，例如 `feature/add-http-proxy-support`。
3. 进行代码或文档修改时，请遵守项目既有的代码风格（使用 `go fmt` 与 `go vet`），并为新增的导出函数编写必要的注释与单元测试。
4. 提交变更前，确保本地所有测试用例通过（执行 `make test`），并更新相应的文档或示例文件以反映变更。
5. 向主仓库的 `main` 分支发起 Pull Request，在描述中清晰说明变更目的、实现方式及潜在影响，等待维护者审阅。

## 常见问题

**Q：LinkPilot 是否会缓存或代理请求内容？**  
A：不会。LinkPilot 仅执行标准 HTTP HEAD 或 GET 请求（仅探测状态码与响应时间），不缓存任何响应体内容，也不提供代理转发功能。所有探测行为均可在配置中禁用请求体读取。

**Q：探测结果是否影响已导入的域名记录？**  
A：不影响。探测结果仅作为附加状态字段存储，不会自动删除或修改域名记录。用户可根据探测结果手动决定是否移除或标记某条记录，系统不进行任何自动化变更操作。

**Q：支持 Windows 系统部署吗？**  
A：LinkPilot 的 Go 源码可交叉编译为 Windows 可执行文件，但当前官方提供的预编译二进制包与默认配置主要针对 Linux 与 macOS 进行测试与优化。Windows 用户可参考 `docs/operator/windows.md` 中的额外说明进行部署。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
