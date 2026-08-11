# ResourceForge

ResourceForge 是一个面向开发者与技术研究人员的开源技术资源聚合与导航系统。该项目定位于解决技术信息碎片化、高质量外链分散、以及开发环境初始化过程中重复检索的问题，通过结构化分类和版本化索引，为用户提供可维护、可扩展的外部资源管理方案。

目标用户包括运维工程师、全栈开发人员、技术调研团队以及开源项目维护者。ResourceForge 本身不存储任何第三方内容，而是通过 Markdown 原生语法和静态站点生成器，将分散的优质技术链接组织为可直接部署的知识库站点，从而降低团队内部信息共享成本，提升技术决策的上下文连贯性。

## 功能概览

- **多级分类导航**：支持按技术领域、使用频率和更新日期对资源进行三级标签过滤，便于快速定位。
- **原始链接保真输出**：系统底层采用纯文本模板引擎，确保用户输入的每一枚 URL 均按原始格式原样渲染，杜绝自动补全协议或域名改写。
- **版本化快照记录**：每次资源列表更新均生成带时间戳的变更日志，支持回溯至任意历史版本的外链集合。
- **依赖环境检测**：内置轻量级 Shell 脚本，自动检测 Node.js、npm、Git 等核心依赖的版本兼容性，并给出明确升级建议。
- **Markdown 驱动渲染**：所有页面内容基于 CommonMark 规范生成，无需数据库，直接编译为静态 HTML，适合托管于任何 Web 服务器或 CDN。
- **外链可用性巡检**：集成定时任务模块（cron 表达式配置），每日凌晨对全部收录 URL 执行 HEAD 请求，标记响应异常条目。
- **自定义元数据扩展**：允许为每条链接附加维护人、所属项目组、预期用途等自定义字段，便于企业级权限管理。

## 应用场景

- **团队技术 onboarding 资料整合**：新成员入职时，可通过 ResourceForge 快速获取公司内部推荐的数据库监控工具、日志分析平台和 API 文档站点，避免零散邮件和聊天记录查找。
- **开源项目 README 外链维护**：开源维护者可将项目依赖的测试环境面板、持续集成状态页和代码质量报告链接统一收纳于 ResourceForge，并同步生成独立的资源清单章节，减少手工更新 README 的负担。
- **技术调研阶段竞品对比**：调研人员在对比多个中间件或云服务时，可将各厂商的官方文档、性能基准测试报告和社区讨论帖集中收录，通过分类标签实现横向快速切换。
- **离线文档站点的外部引用锚点**：在内网部署的文档中心里，使用 ResourceForge 管理所有指向公网的外部引用，当外链失效时仅需更新一处即可全局生效。

## 快速开始

以下步骤适用于 Linux/macOS 环境，Windows 用户建议通过 WSL2 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/your-org/resource-forge.git
cd resource-forge

# 2. 安装 Node.js 依赖（需 Node.js 16.x 及以上）
npm install --production

# 3. 启动开发服务器，默认监听 3000 端口
npm run build
npm start
```

访问 `http://localhost:3000` 即可查看资源导航首页。若需自定义资源列表，请直接编辑 `data/sources.yml` 文件，然后重新执行 `npm run build`。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | 16.x 或 18.x LTS | 运行时环境，用于执行构建脚本和开发服务器 |
| npm | 8.x 或 9.x | 包管理器，用于安装项目依赖 |
| Git | 2.25+ | 版本控制工具，用于克隆仓库和提交变更 |
| curl | 7.68+ | 外链可用性巡检脚本依赖的命令行工具 |
| cronie | 1.5+（Linux）或 launchd（macOS） | 定时任务调度器，用于自动化巡检功能 |

若使用 Docker 部署，则仅需 Docker Engine 20.10+ 及 Docker Compose 2.0+，其余依赖均封装于容器镜像内。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | `/docs/user-guide/` | 如何添加/删除/修改资源条目？分类标签如何自定义？ |
| 运维手册 | `/docs/ops-guide/` | 如何配置巡检频率？如何迁移数据库（JSON 文件）至新服务器？ |
| 开发指南 | `/docs/dev-guide/` | 模板引擎的变量命名规范是什么？如何新增一个页面布局？ |
| API 参考 | `/docs/api-reference/` | 构建工具暴露了哪些 Node.js API？如何通过命令行参数覆盖默认配置？ |
| 故障排查 | `/docs/troubleshooting/` | 构建失败常见原因及解决方案；巡检超时如何调整阈值？ |

## 资源列表

### 足球数据分析类

<code>zuqiutuijianwangzhan.org.cn</code>

<code>zuqiuyucezhuanjia.org.cn</code>

<code>zuqiuyucepingtai.org.cn</code>

<code>zuqiubifenyuce.org.cn</code>

<code>zuqiuzhuanjiayuce.org.cn</code>

<code>zuqiusaishiyuce.org.cn</code>

<code>zuqiuzhuanjiafenxi.org.cn</code>

<code>zuqiujinriyuce.org.cn</code>

<code>zuqiuyucewang.net.cn</code>

<code>zuqiuhongdanfenxi.net.cn</code>

上述资源按照原始输入顺序逐条收录，未做任何格式修改、协议补全或域名标准化处理。各链接的具体内容分类、标签及最后验证日期可在 `data/sources.yml` 中查看。

## 项目结构

```
resource-forge/
├── src/                                 # 源代码主目录
│   ├── templates/                       # Markdown 及 HTML 模板
│   │   ├── layout.ejs                   # 全局布局模板（含导航栏及页脚）
│   │   ├── index.ejs                    # 首页分类聚合模板
│   │   └── detail.ejs                   # 单条资源详情页模板
│   ├── scripts/                         # 构建与运维脚本
│   │   ├── build.js                     # 核心构建脚本，读取 YAML 生成 Markdown
│   │   ├── checker.js                   # 外链可用性巡检主逻辑
│   │   └── cron-wrapper.sh              # 定时任务封装脚本（含日志轮转）
│   ├── styles/                          # 自定义 CSS 样式（基于 normalize.css）
│   │   ├── main.css                     # 全局样式变量及布局
│   │   └── print.css                    # 打印样式优化
│   └── utils/                           # 通用工具函数
│       ├── logger.js                    # 分级日志输出（error/warn/info/debug）
│       └── validator.js                 # URL 格式校验及去重工具
├── data/                                # 数据存储目录
│   ├── sources.yml                      # 核心资源列表（YAML 格式，用户可编辑）
│   └── archive/                         # 历史版本快照存储区
│       └── 2026-08-10-snapshot.yml      # 按日期命名的自动备份文件
├── dist/                                # 构建输出目录（静态站点，可部署）
│   ├── index.html                       # 编译后的首页
│   ├── resources/                       # 按分类生成的资源列表页面
│   └── assets/                          # 经过哈希命名的静态资源（CSS/JS）
├── tests/                               # 单元测试与集成测试
│   ├── unit/                            # 工具函数与模板渲染测试
│   └── integration/                     # 端到端构建流程测试（含模拟数据）
├── docs/                                # 项目文档（用户手册、运维手册等）
│   ├── user-guide.md
│   ├── ops-guide.md
│   └── dev-guide.md
├── .github/                             # GitHub 社区配置文件
│   ├── ISSUE_TEMPLATE/                  # 问题模板（Bug 报告/功能请求）
│   └── workflows/                       # CI 工作流（构建检查及部署）
│       └── main.yml
├── .env.example                         # 环境变量示例（含巡检时间配置）
├── package.json                         # npm 项目清单及脚本定义
├── README.md                            # 项目主说明文档（即本文档）
└── LICENSE                              # MIT 许可证文本
```

## 贡献指南

1. **分支管理**：请从 `main` 分支创建个人功能分支，命名格式为 `feature/您的用户名-简要描述`（例如 `feature/alice-add-eslint`），禁止直接向主分支提交。
2. **资源条目变更**：若需增删 `data/sources.yml` 中的链接，请确保同时更新该条目对应的 `last_verified` 字段为当前 ISO 日期，并运行 `npm test` 验证格式合法性。
3. **文档同步**：任何影响用户操作流程的变更，必须同步修改 `/docs/` 下对应的手册文件。新增配置项需在 `.env.example` 中添加注释说明。
4. **提交信息规范**：使用语义化提交信息，格式为 `<type>(<scope>): <subject>`，其中 type 包括 feat、fix、docs、chore 等，scope 为影响的模块名称（如 build、checker、templates）。
5. **拉取请求流程**：提交 PR 前请确保本地执行 `npm run lint` 和 `npm test` 全部通过，并在 PR 描述中关联相关 Issue 编号。至少需要一名维护者批准后方可合并。

## 常见问题

**Q: 构建时出现 `Error: Cannot find module 'ejs'` 如何处理？**

A: 此错误表明依赖未完整安装。请首先确认 Node.js 版本符合要求，然后删除 `node_modules` 目录和 `package-lock.json` 文件，重新执行 `npm install`。若仍失败，可尝试使用 `npm cache clean --force` 清理缓存后重试。

**Q: 外链巡检报大量 `403 Forbidden` 是否表示链接失效？**

A: 不一定。部分站点（如带有反爬机制的论坛或 API 网关）会拒绝 HEAD 请求，此时巡检脚本会标记为 `UNREACHABLE`。建议通过 `src/scripts/checker.js` 中的 `--method GET` 参数切换请求方法进行二次验证，或手动在浏览器中访问确认。

**Q: 如何将资源列表迁移到另一台服务器？**

A: 只需打包 `data/` 目录和 `.env` 文件至新服务器，并确保新环境已安装相同版本的 Node.js。执行 `npm install --production` 后，运行 `npm run build` 即可生成静态页面，无需额外迁移数据库。

## 许可证

MIT License

Copyright (c) 2026 ResourceForge Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
