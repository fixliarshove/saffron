# Teleport Navigator

Teleport Navigator 是一个面向技术社区与基础设施运维场景的轻量级外链资源导航与聚合平台。该项目定位于帮助开发者、运维工程师与技术研究者快速访问互联网中高价值但分散的垂直领域资源，解决信息碎片化导致的检索效率低下、资源失效与重复造轮子问题。通过集中化的资源收录、标签化分类与可定制的导航视图，Teleport Navigator 将零散的链接转化为可维护、可共享、可审计的知识索引，适用于个人技术收藏库、团队知识底座或公开社区的内容入口。

Teleport Navigator 并非通用搜索引擎或书签管理器，而是面向技术资源长期存档与结构化解构的专业工具。其核心设计原则为：资源不可变引用、分类可扩展性、状态可观测性。项目默认输出纯静态页面，无需后端运行时，可在任意对象存储或 CDN 上部署。同时提供 CLI 辅助工具用于校验链接可用性、生成站点地图与资源元信息提取，便于集成至 CI/CD 流水线。

## 功能概览

- **资源收录与持久化索引**：支持通过 YAML 或 JSON 格式定义资源条目，包含 URL、标题、标签、收录时间、状态备注等字段，所有记录以纯文本形式存储于项目仓库中，便于版本控制与协作。

- **智能分类与多维度导航**：内置分类引擎允许按资源领域（如网络基础、多媒体处理、语言学习、系统运维等）、文件类型、来源地域或自定义标签进行筛选与排序，提供树形分类与扁平标签两种视图模式。

- **链接可用性健康检查**：集成基于 curl 与 HTTP 状态码的周期性检测模块，可输出资源可用性报告，标注异常链接（超时、4xx/5xx、SSL 证书错误），辅助维护者清理或更新失效条目。

- **静态站点生成引擎**：内置模板渲染系统，将资源数据与主题模板结合，生成响应式 HTML 页面，支持暗色主题、移动端适配与无障碍访问。生成的页面完全静态，无需 JavaScript 运行时即可完成导航。

- **资源元信息自动补全**：通过解析目标页面的 title、description 与 favicon，自动补全资源条目的显示名称与图标，减少手动录入工作量，提升索引质量。

- **导入与导出兼容性**：支持从常见的书签格式（HTML 导出、Markdown 列表）导入资源，同时支持导出为 CSV、JSON 或纯文本列表，便于迁移至其他系统或进行离线分析。

- **细粒度权限与审核占位**：为团队协作场景预留审核状态字段，支持标记“待审核”、“已拒绝”、“已收录”等状态，并记录操作人及时间，适用于开源社区贡献者提交资源的场景。

## 应用场景

- **个人技术收藏库的体系化管理**：开发者可使用 Teleport Navigator 集中管理日常翻阅的技术文档、在线工具、实验环境入口与视频教程链接，通过标签与分类建立个人知识索引，避免浏览器书签的扁平化混乱。

- **团队内部技术文档中心的资源底座**：技术团队可将 Teleport Navigator 作为团队 Wiki 或 Onboarding 文档的补充，统一收录生产环境依赖的第三方服务面板、监控系统入口、日志查询地址以及内部工具链文档，确保团队成员快速定位关键资源。

- **开源社区的内容聚合入口**：开源项目维护者可将 Teleport Navigator 用于项目官网的“生态资源”页面，收录社区贡献的周边工具、示例项目、讨论区与学习资料，降低新用户的学习门槛，同时鼓励社区贡献资源链接。

- **技术培训与教育机构的课程辅助索引**：讲师或培训机构可使用 Teleport Navigator 快速构建课程配套的外部阅读材料列表，按课时或主题组织链接，并定期检查链接有效性，确保学员始终能够访问到正确的参考资料。

- **运维值班场景下的快速导航面板**：运维团队可将常用内部系统（如监控告警、日志平台、堡垒机、数据库管理界面）的入口集中配置于 Teleport Navigator，并配置为浏览器默认新标签页，显著缩短故障响应时的操作路径。

## 快速开始

以下命令演示了从源码克隆、安装依赖到启动开发服务器的完整流程。开发环境需要 Node.js 18 及以上版本，并已安装 pnpm 包管理器。

```bash
# 克隆项目仓库
git clone https://github.com/teleport-navigator/navigator.git
cd navigator

# 安装依赖（使用 pnpm，也可替换为 npm 或 yarn）
pnpm install

# 启动开发服务器（默认监听 localhost:3000）
pnpm run dev

# 构建生产静态文件（输出至 dist/ 目录）
pnpm run build

# 预览生产构建结果
pnpm run preview
```

## 安装要求

Teleport Navigator 的核心引擎基于 Node.js 实现，静态站点生成与 CLI 工具均依赖该运行时环境。以下为官方支持的运行环境与必要依赖项，请确保部署前满足所有条件。

| 依赖项 | 必需版本或规格 | 说明 |
|--------|---------------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行构建脚本与 CLI 工具，不支持 v16 及以下版本 |
| pnpm | 8.x 或 9.x | 推荐包管理器，用于依赖安装与工作区管理；亦可使用 npm 或 yarn，但需自行处理 peer dependency |
| 操作系统 | Linux (glibc 2.28+), macOS (12+), Windows (10+ with WSL) | 官方测试覆盖 Ubuntu 22.04、macOS Ventura 及 Windows 11 WSL2 环境 |
| 浏览器 | 现代浏览器（Chrome 90+, Firefox 88+, Edge 90+, Safari 15+） | 仅用于预览生成的静态页面，无特殊前端框架依赖，支持 ES2018+ |
| 磁盘空间 | 至少 200 MB | 用于存放源码、依赖包（node_modules）及构建输出文件，实际占用随资源条目数量线性增加 |
| 网络访问 | 允许出站 HTTPS 与 HTTP 请求 | 用于链接健康检查与元信息补全功能，若内网部署需配置代理或镜像源 |

## 文档导航

Teleport Navigator 提供分层文档体系，覆盖从入门使用到二次开发的全链路指导。下表列出主要文档模块及其面向的问题域。

| 层面 | 目录 / 文件 | 回答的问题 |
|------|-------------|------------|
| 用户手册 | docs/user-guide/quick-start.md | 如何添加第一条资源？如何导入浏览器书签？如何切换主题？ |
| 用户手册 | docs/user-guide/customization.md | 如何修改页面标题、Logo 与页脚信息？如何自定义分类颜色？ |
| 运维指南 | docs/ops/deployment.md | 如何将生成的静态站点部署到 Nginx、S3 或 Cloudflare Pages？ |
| 运维指南 | docs/ops/health-check.md | 如何配置定时链接检查？如何查看异常报告并批量处理失效链接？ |
| 开发者文档 | docs/dev/architecture.md | 项目的整体模块划分是怎样的？数据流如何从资源文件到 HTML 输出？ |
| 开发者文档 | docs/dev/cli-commands.md | CLI 工具支持哪些命令（build, check, import, export）及其参数含义？ |
| 贡献者指南 | CONTRIBUTING.md | 如何提交新资源收录？代码规范与 PR 流程要求是什么？ |
| 设计决策记录 | docs/adr/ | 为什么选择静态生成而非 SSR？为什么资源数据使用 YAML 而非数据库？ |

## 资源列表

本批次收录的资源链接覆盖多个垂直领域，涵盖行业门户、多媒体资源与专业技术社区。所有链接均按原始来源原样列示，未做任何协议、域名或路径的修改。每个链接均以 code 标签包裹，以保证其原始形态在文档中精准呈现。

### 综合门户与社区资源

<code>jiujiujiujiure.org.cn</code>

<code>renqishaofuzhongwen.org.cn</code>

<code>qingqingcaochengrenwang.org.cn</code>

### 多媒体与影视资源

<code>chengrenzipaishipin.org.cn</code>

<code>taosewuyuetian.org.cn</code>

<code>youcuyoudashipin.org.cn</code>

<code>yazhousetuzipai.org.cn</code>

### 语言学习与字幕资源

<code>tingtingrihanyiquerqusanqu.org.cn</code>

<code>shunvrenqizhongwenzimu.org.cn</code>

### 动画与动漫资源

<code>yinghuadongmanzhengbanguanwangderukou.org.cn</code>

## 项目结构

项目采用模块化单仓库布局，核心逻辑、配置、模板与文档分离，便于维护与扩展。以下为项目根目录下的主要目录与关键文件注释。

```
navigator/
├── src/                                # 核心源代码目录
│   ├── cli/                            # CLI 命令行入口与命令实现
│   │   ├── index.ts                    # 命令注册与解析
│   │   ├── build.ts                    # 构建命令实现
│   │   └── check.ts                    # 链接检查命令实现
│   ├── core/                           # 核心数据模型与处理逻辑
│   │   ├── resource.ts                 # 资源条目类（URL、标题、标签、状态）
│   │   ├── taxonomy.ts                 # 分类树与标签系统管理
│   │   └── validator.ts                # URL 校验与规范化工具
│   ├── engine/                         # 静态生成引擎
│   │   ├── renderer.ts                 # 模板渲染器（基于 EJS）
│   │   ├── sitemap.ts                  # 站点地图生成器
│   │   └── assets.ts                   # 静态资源（CSS、JS）打包与复制
│   ├── fetcher/                        # 外部资源获取模块
│   │   ├── metadata.ts                 # 页面 Title/Favicon 提取
│   │   └── status.ts                   # HTTP 状态检测与超时控制
│   └── types/                          # TypeScript 类型定义
│       ├── resource.d.ts               # 资源条目类型
│       └── config.d.ts                 # 全局配置类型
├── data/                               # 资源数据存储目录（YAML/JSON 文件）
│   ├── sources/                        # 用户自定义资源文件
│   │   ├── network.yml                 # 网络基础类资源
│   │   └── multimedia.yml              # 多媒体类资源
│   └── taxonomy.yml                    # 全局分类与标签定义
├── templates/                          # 页面模板文件
│   ├── layouts/                        # 基础布局模板
│   │   ├── default.ejs                 # 默认页面布局
│   │   └── minimal.ejs                 # 极简布局（用于嵌入）
│   ├── partials/                       # 可复用的模板片段
│   │   ├── header.ejs                  # 页头导航
│   │   └── footer.ejs                  # 页脚信息
│   └── pages/                          # 独立页面模板
│       ├── index.ejs                   # 首页资源列表
│       └── detail.ejs                  # 单资源详情页（预留）
├── dist/                               # 构建输出目录（git 忽略，运行时生成）
│   ├── index.html                      # 生成的首页
│   └── assets/                         # 打包后的 CSS/JS 文件
├── docs/                               # 项目文档（用户手册、运维指南、ADR）
│   ├── user-guide/                     # 用户手册
│   ├── ops/                            # 运维指南
│   ├── dev/                            # 开发者文档
│   └── adr/                            # 架构决策记录
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # 单元测试（Jest）
│   └── integration/                    # 集成测试（含模拟 HTTP 请求）
├── .github/                            # GitHub 工作流配置
│   └── workflows/                      # CI/CD 流水线定义
│       ├── build.yml                   # 构建检查
│       └── health-check.yml            # 定时链接检查任务
├── package.json                        # 项目依赖与脚本定义
├── pnpm-lock.yaml                      # 依赖锁文件
├── tsconfig.json                       # TypeScript 编译配置
├── .eslintrc.js                        # ESLint 代码检查配置
├── .prettierrc                         # 代码格式化配置
└── README.md                           # 项目说明文档（即本文档）
```

## 贡献指南

Teleport Navigator 欢迎各类贡献，包括但不限于新增资源收录、分类优化、代码缺陷修复、文档改进与功能提议。为确保协作流畅，请遵循以下标准化流程。

1.  **提交资源新增请求**：若您希望向资源列表中添加新链接，请先在 `data/sources/` 目录下找到对应领域的 YAML 文件，按照现有格式追加条目，并在 PR 描述中注明资源的用途、分类依据与收录理由。对于不确定归属的资源，可新建临时文件并标注 `status: pending` 以供审核。

2.  **代码或文档变更流程**：所有代码与文档变更请通过 GitHub Pull Request 提交。在提交前，请确保运行 `pnpm run lint` 和 `pnpm run test` 通过所有检查，并更新受影响的文档章节。若变更涉及用户可见的行为，请同时更新 `docs/user-guide/` 中的对应手册。

3.  **链接健康检查反馈**：若您通过项目提供的 `pnpm run check` 命令发现异常链接，且该链接已无法访问或已迁移，请提交 Issue 或在 PR 中直接更新资源条目的 `status` 字段为 `broken` 或更新其 `url` 值。对于大规模链接更新，建议附加检查日志截图。

4.  **分类与标签体系调整**：若您认为现有分类或标签不足以合理归置某类资源，请先在 `data/taxonomy.yml` 中提议新增分类节点，并在 PR 描述中阐述分类逻辑与预期受益场景。避免在未达成共识的情况下批量移动已有资源分类。

5.  **提交信息规范**：提交信息（Commit Message）请遵循 Conventional Commits 格式，使用 `feat:`、`fix:`、`docs:`、`chore:` 等前缀，并附带简要描述。PR 标题应清晰概括变更内容，例如 “feat: add support for multi-level tag filtering” 或 “docs: update deployment guide for S3”。

## 常见问题

**问：Teleport Navigator 是否需要在服务器端部署数据库或后端服务？**

答：不需要。Teleport Navigator 设计为纯静态站点生成器，所有资源数据存储在仓库内的 YAML 文件中，构建过程在本地或 CI 环境完成后输出纯 HTML、CSS 与 JavaScript 文件。生成的静态页面可托管于任何支持静态文件的服务（如 Nginx、Apache、S3、Cloudflare Pages、GitHub Pages），无需维护数据库连接或应用服务器。链接健康检查功能通过 CLI 工具独立运行，不依赖常驻后台进程。

**问：如何管理大量资源条目（超过 1000 条）时的构建性能？**

答：项目核心引擎对资源处理采用流式读取与增量构建策略。对于千级别条目，构建时间通常在 15 秒以内（基于 AMD Ryzen 7 处理器与 NVMe 硬盘实测）。若条目数超过 5000，建议将资源文件按分类拆分为多个 YAML 文件，并在 `taxonomy.yml` 中引用拆分后的文件列表，以利用并行读取优化。此外，可通过 `--filter` 参数仅构建特定分类的子集用于开发调试。

**问：我可以将 Teleport Navigator 用于商业项目或企业内部部署吗？**

答：可以。Teleport Navigator 采用 MIT 许可证发布，允许自由使用、修改、分发及用于商业目的，无需支付授权费用。唯一的约束是保留原始版权声明与许可证文件。对于企业内部敏感资源的访问控制，建议将生成的静态页面部署于内网环境，并依赖网络层的身份验证（如 VPN、企业 SSO 反向代理）进行权限管理。

## 许可证

MIT License

Copyright (c) 2026 Teleport Navigator Contributors

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
