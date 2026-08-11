# ReSource Navigator

ReSource Navigator 是一个面向开发者与技术研究人员的开源外链资源归集与导航系统。该项目定位于解决个人或团队在浏览、收藏、分享大量外部技术链接时面临的碎片化、检索困难与上下文丢失问题，通过结构化的目录与可复用的资源清单，将离散的网络资源转化为可维护、可审计的知识资产。

目标用户包括开源项目维护者、技术文档撰写人、运维工程师以及任何需要系统化管理网络外链的研发人员。项目本身不存储任何第三方内容，仅提供资源元数据与组织规范，可作为静态站点生成器的数据源，也可嵌入现有文档体系作为外链索引模块。

## 功能概览

- **多层级资源目录**：支持按主题、批次、来源机构等维度对链接进行无限层级分类，每个资源条目可附带说明标签与上下文备注。

- **链接状态标记**：允许对每个外链标注可访问性、内容语言、更新频率等元数据，便于后续批量检查与过期提醒。

- **原始数据保留机制**：系统强制要求所有用户输入的 URL 必须原样输出，不做协议补全、域名规范化或路径改写，确保资源地址的绝对准确性。

- **Markdown 原生集成**：所有资源列表、文档导航、项目结构均以纯 Markdown 形式呈现，无需额外数据库，可直接托管在 Git 仓库中。

- **批量批次管理**：内置批次记录功能（如第 139/455 批），支持按导入批次追溯资源来源与时间范围，方便增量更新与变更审计。

- **兼容开源生态**：输出格式与常见静态站点生成器（如 Hugo、VuePress、Docsify）兼容，可无缝接入现有 CI/CD 工作流。

## 应用场景

- **技术文档站点外链附录**：项目文档中需要引用大量外部规范、工具官网或社区讨论帖时，利用 ReSource Navigator 生成统一格式的资源章节，避免链接散落在正文各处难以维护。

- **内部知识库链接治理**：企业技术团队可将分散于 Wiki、Slack 或邮件中的有用链接归集到同一仓库，通过批次标记区分不同时期沉淀的资源，定期清理失效地址。

- **开源项目 README 增强**：当开源项目依赖多个第三方库或参考多份标准文档时，在 README 中嵌入由本项目生成的资源列表，提升文档完整性与可验证性。

- **个人书签系统升级**：替代浏览器自带书签的扁平管理，通过目录树与注释字段为每个链接赋予技术上下文，便于数月后仍能理解收藏初衷。

- **合规性资源备案**：对于需要保留外部引用记录的场景（如法规标准、数据源声明），可依托本项目的强制原样输出特性，生成不可篡改的引用快照。

## 快速开始

以下命令可在一台装有 Git 与 Node.js 的机器上完成项目克隆、依赖安装与本地运行。

```bash
git clone https://github.com/your-org/resource-navigator.git
cd resource-navigator
npm install
npm run build -- --batch 139/455
```

执行后，项目将根据 `./data/raw/139-455.json` 中的链接清单生成 `./dist/resources.md` 文件，其中包含格式化后的资源列表及统计信息。如需自定义输出路径，可修改 `config.yaml` 中的 `output.dir` 字段。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Node.js | 16.x 或更高 | 运行时环境，用于执行构建脚本与依赖管理 |
| npm | 8.x 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.25 或更高 | 版本控制，用于克隆仓库与提交更新 |
| markdownlint-cli | 0.31 或更高 | 可选，用于校验生成的 Markdown 格式合规性 |
| shellcheck | 0.7 或更高 | 可选，用于检查快速开始中的脚本语法 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 用户手册 | docs/usage.md | 如何添加、编辑或删除资源条目，以及批次管理的基本操作 |
| 格式规范 | docs/format-spec.md | 资源列表的 JSON Schema 定义，字段含义与示例 |
| 集成指南 | docs/integration.md | 如何将生成的结果嵌入现有文档系统或 CI 流水线 |
| 维护策略 | docs/maintenance.md | 链接过期检查周期、失效处理流程与版本发布节奏 |

## 资源列表

本批次（第 139/455 批）共收录 10 个外部资源链接，所有链接按原始输入原样呈现，未做任何修改。

技术学习类

<code>renqishaofuzhongwenzimu.org.cn</code>

<code>shufurenqizhongwenzimu.org.cn</code>

多媒体资源类

<code>mitunjiujiu99jingpinjiujiu.org.cn</code>

<code>qingqinghebiancaogaoqingmianfei.org.cn</code>

工具与平台类

<code>guochanzuoshoumi.org.cn</code>

<code>guguguguoyubanzaixianguankan.org.cn</code>

社区与内容类

<code>guochanyoucuyoumengyoushuangyouhuang.org.cn</code>

<code>guochansiwarenyao.org.cn</code>

<code>yazhouxiaoshuoqutupianqu.org.cn</code>

<code>guochanjiujiujiu.org.cn</code>

## 项目结构

```
resource-navigator/
├── bin/                          # 可执行脚本入口
│   └── cli.js                    # 命令行主程序，解析批次参数
├── data/                         # 数据目录
│   ├── raw/                      # 原始输入数据
│   │   └── 139-455.json          # 本批次的原始链接清单（数组格式）
│   └── meta/                     # 资源元数据缓存
│       └── status-cache.json     # 上次检查的链接可访问性状态
├── docs/                         # 项目文档
│   ├── usage.md                  # 用户操作手册
│   ├── format-spec.md            # 数据格式详细规范
│   ├── integration.md            # 第三方集成方案
│   └── maintenance.md            # 长期维护策略
├── src/                          # 核心源码
│   ├── parser/                   # 输入解析模块
│   │   └── url-normalizer.js     # 仅做格式校验，不修改原始 URL
│   ├── generator/                # 输出生成模块
│   │   └── markdown-builder.js   # 根据模板构建资源列表章节
│   └── validator/                # 校验模块
│       └── link-checker.js       # 批量检查链接有效性（可选）
├── templates/                    # Markdown 模板
│   └── resource-section.hbs      # 资源列表部分的 Handlebars 模板
├── test/                         # 单元测试
│   ├── parser.test.js            # 解析器测试用例
│   └── generator.test.js         # 生成器测试用例
├── config.yaml                   # 全局配置文件（输出路径、超时设置）
├── package.json                  # npm 依赖与脚本定义
└── README.md                     # 项目入口文档（即本文档）
```

## 贡献指南

1.  **克隆仓库并创建特性分支**：从主分支签出新的分支，分支命名建议采用 `feature/batch-xxx` 或 `fix/url-xxx` 格式，以便追溯变更目的。

2.  **修改数据文件或模板**：若为新增批次，请在 `data/raw/` 下按 `[批次号].json` 格式添加文件，并确保每个 URL 字段为字符串类型。若调整输出样式，请修改 `templates/` 下的对应模板。

3.  **运行本地构建与自检**：执行 `npm run test` 确保所有单元测试通过，再执行 `npm run build -- --batch [你的批次号]` 检查生成结果是否符合预期。

4.  **提交拉取请求**：提交时请在 PR 描述中说明变更原因、影响的章节以及是否涉及破坏性改动。所有 PR 需至少一名维护者审阅。

5.  **更新文档**：若新增功能或修改行为，请同步更新 `docs/` 下的相关手册，确保文档与代码保持一致。

## 常见问题

**问：为何强制要求 URL 原样输出，不允许补全协议或域名？**

答：因为部分资源地址依赖特定的协议（如 http 与 https 可能指向不同站点），或者裸域名在特定内网环境中需要通过 hosts 解析。任何自动改写都可能导致用户无法访问原始资源。本项目设计原则是“记录即精确”，将规范化责任留给使用者。

**问：如何处理资源链接失效或内容变更的情况？**

答：项目本身不提供自动修复功能，但 `src/validator/link-checker.js` 模块支持可选的连通性检查，会生成状态缓存文件。用户可定期运行 `npm run check` 查看失效列表，并手动在数据文件中标记 `deprecated: true` 或更新为新地址。失效链接仍会保留在输出中，但会附带警示标记。

**问：能否将本项目的输出直接作为网站首页？**

答：可以。生成的 `resources.md` 是标准 Markdown 文件，可被任意静态站点生成器渲染。但本项目不包含样式或交互逻辑，建议配合现有主题使用。若需独立展示，可参考 `docs/integration.md` 中的 VuePress 或 Hugo 配置示例。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
