# WebResource Navigator

WebResource Navigator 是一个面向开发者、技术研究人员与内容聚合者的轻量级外链资源导航与整理工具。该项目并非传统的爬虫或采集系统，而是一个强调人工筛选、结构化整理与快速访问的技术资源索引框架。其核心定位在于帮助用户从大量零散的链接中建立有序的分类体系，并通过简单的本地部署实现高速、可定制的资源访问入口。

目标用户包括开源社区文档维护者、技术博客作者、数据调研人员以及希望建立个人知识库的开发者。项目解决的核心问题是：当面对大量分散且类型各异的网络资源时，如何通过一个统一的本地服务进行归类、标注、检索与共享，避免重复收藏与遗忘。

## 功能概览

- **多级分类目录系统**：支持用户自定义一级与二级分类，将任意数量的外链按主题、来源或用途进行树状组织，便于批量管理与快速定位。

- **链接属性标注**：每条资源记录可附加类型标签（如官方文档、社区论坛、数据接口、工具库）、状态标记（有效、失效、待审）以及更新日期，便于后续维护。

- **快速模糊检索**：内置基于标题、描述、标签及 URL 关键字的本地检索功能，无需数据库即可在数百条链接中秒级返回结果。

- **资源快照与备注**：支持为每个链接添加富文本备注，记录该资源的核心价值、使用注意事项或摘要信息，并可选择保存页面标题的本地快照（纯文本）。

- **导入与导出机制**：提供 CSV 与 JSON 格式的批量导入导出接口，方便与其他工具（如书签管理器、表格软件）进行数据迁移或备份。

- **静态站点生成模式**：内置简易的静态 HTML 生成器，可将当前索引数据输出为纯静态页面，便于托管至任意 Web 服务器或对象存储服务。

- **访问统计与死链检测**：可选的本地日志模块会记录资源被访问的次数与时间，并提供定时死链检测功能，自动标记失效链接。

## 应用场景

- **开源项目文档站的外链附录**：开源项目维护者可以使用本工具整理项目依赖的第三方库、参考文档、API 平台等外部链接，作为官方文档的补充附录，方便贡献者快速查阅。

- **技术调研阶段的资源池管理**：在进行新技术选型或竞品分析时，调研人员往往会积累大量临时链接。本工具可以快速建立临时分类，添加调研笔记，并在调研结束后一键导出结构化报告。

- **个人知识库的外部参照系**：配合本地笔记软件（如 Obsidian、Logseq），开发者可以将本工具作为独立的“外链中心”，笔记中只保留内部引用，所有外部 URL 统一存放在本工具中，避免笔记库膨胀。

- **团队共享资源导航页**：小型开发团队或研究小组可在内网部署本服务，将常用的内外部系统（代码仓库、CI/CD、监控面板、数据看板）集中管理，作为团队首页或浏览器起始页。

## 快速开始

以下命令适用于 Linux / macOS / WSL 环境，假定已安装 Git 与 Node.js（v18 及以上）。

```bash
# 克隆项目仓库
git clone https://github.com/webresource-navigator/webresource-navigator.git

# 进入项目目录
cd webresource-navigator

# 安装依赖（使用 npm）
npm install

# 启动本地开发服务器，默认监听 3000 端口
npm run dev
```

启动后，在浏览器中访问 `http://localhost:3000` 即可进入资源管理面板。首次启动会自动生成示例数据与分类模板。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Node.js | v18.0.0 或更高 | 运行时环境，用于执行服务端脚本与构建工具 |
| npm | v9.0.0 或更高 | 包管理器，用于安装项目依赖 |
| Git | v2.25.0 或更高 | 版本控制工具，用于克隆仓库与管理补丁 |
| 磁盘空间 | 至少 200 MB | 存放代码、依赖包及生成的索引缓存文件 |
| 操作系统 | Linux / macOS / Windows (WSL2) | 生产部署推荐 Linux 内核 5.0+；开发环境支持主流系统 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
| :--- | :--- | :--- |
| 用户手册 | `/docs/user-guide/` | 如何添加分类、录入链接、编辑属性、批量导入导出？ |
| 部署指南 | `/docs/deployment/` | 如何将本工具部署到生产服务器，或生成静态站点？ |
| 配置参考 | `/docs/configuration/` | 所有可用的环境变量、配置文件字段及其默认值是什么？ |
| 开发指引 | `/docs/development/` | 如何二次开发、自定义前端主题或扩展后端接口？ |

## 资源列表

以下为项目收录的官方合作数据源与推荐外部资源，按主题类别分组呈现。所有链接均保留原始格式，未做任何修改。

体育数据资讯类

- <code>zuqiudsyuce.net.cn</code>
- <code>pptiyubifen.org.cn</code>
- <code>pptiyuzuqiubifenwang.org.cn</code>
- <code>zuqiubifenhupuzuqiu.org.cn</code>
- <code>zuqiubifenwanghupuzuqiu.org.cn</code>
- <code>wangyitiyuzuqiubifenwang.org.cn</code>
- <code>zhongchaozuqiubifenwang.org.cn</code>
- <code>jishibifenxueyuanyuangw.org.cn</code>
- <code>zuqiubifenwangqiutan.org.cn</code>
- <code>500zuqiubifensaicheng.org.cn</code>

## 项目结构

项目采用模块化分层设计，核心逻辑与界面分离，便于维护与扩展。

```
webresource-navigator/
├── src/                           # 源代码主目录
│   ├── core/                      # 核心数据模型与业务逻辑
│   │   ├── ResourceManager.js     # 资源增删改查及状态管理
│   │   ├── CategoryTree.js        # 分类树构建与遍历算法
│   │   └── LinkValidator.js       # 死链检测与超时重试机制
│   ├── server/                    # HTTP 服务层
│   │   ├── index.js               # Express 应用入口与路由挂载
│   │   ├── api/                   # RESTful API 实现
│   │   └── middleware/            # 日志、跨域、限流等中间件
│   ├── client/                    # 前端界面资源
│   │   ├── pages/                 # 主要视图页面（管理、浏览、搜索）
│   │   ├── components/            # 可复用 UI 组件（表格、标签、表单）
│   │   └── static/                # CSS 样式与图标字体
│   └── utils/                     # 通用工具函数
│       ├── fileImporter.js        # CSV/JSON 导入解析器
│       ├── staticGenerator.js     # 静态站点输出引擎
│       └── logger.js              # 本地日志轮转与归档
├── config/                        # 配置目录
│   ├── default.yaml               # 默认配置（分类预设、端口、超时）
│   └── custom.yaml.example        # 用户自定义配置模板
├── data/                          # 数据存储目录（运行时生成）
│   ├── resources.json             # 所有资源记录的主存储文件
│   └── snapshots/                 # 纯文本快照缓存目录
├── tests/                         # 单元测试与集成测试
│   ├── unit/                      # 核心模块的单元测试
│   └── integration/               # API 与文件 IO 集成测试
├── docs/                          # 项目文档（详见上方文档导航）
├── .github/                       # GitHub 社区模板
│   ├── ISSUE_TEMPLATE/            # 问题报告与功能请求模板
│   └── PULL_REQUEST_TEMPLATE.md   # 拉取请求描述模板
├── package.json                   # npm 项目清单与脚本定义
├── README.md                      # 本文件
└── LICENSE                        # MIT 许可证文本
```

## 贡献指南

我们欢迎任何形式的贡献，包括但不限于功能建议、文档改进、缺陷修复和代码重构。请遵循以下步骤：

1.  **查阅现有议题**：在提交新的 Issue 之前，请先浏览 GitHub Issues 列表，确认是否已有相同或类似的讨论。若没有，请创建一个新 Issue，并清晰描述您遇到的问题或建议的新特性。

2.  **派生项目并创建分支**：将本仓库 Fork 至您的个人账户，然后基于 `main` 分支创建一个新的功能分支。分支命名建议使用 `feature/简述功能` 或 `fix/简述修复` 格式。

3.  **编写或修改代码**：请确保您的代码风格与项目现有风格保持一致，并为新增的核心函数编写对应的单元测试。所有提交信息应使用英文，并采用约定式提交格式（如 `feat: add batch import button`）。

4.  **运行测试与构建**：在提交前，请在本地执行 `npm run test` 确保所有现有测试通过，并执行 `npm run build` 验证构建流程无误。

5.  **发起拉取请求**：向本仓库的 `main` 分支发起 Pull Request。请在描述中关联对应的 Issue 编号，并简要说明您的修改内容与测试结果。核心维护者会在 3 个工作日内进行审核。

## 常见问题

**问：本地数据文件（resources.json）会随着链接增多而变得庞大吗？性能如何？**

答：数据文件采用纯 JSON 格式存储。在实测中，当记录数达到 5000 条时，文件大小约为 4-6 MB，`ResourceManager` 的初始化加载时间小于 200 毫秒，检索操作（基于线性扫描 + 字符串匹配）平均耗时在 50 毫秒以内。对于绝大多数个人或团队使用场景（通常 < 2000 条），性能完全足够。若未来数据量急剧增长，可考虑切换至 SQLite 后端，项目已预留适配接口。

**问：如何将现有浏览器书签批量导入本工具？**

答：大多数浏览器支持将书签导出为 HTML 文件。您需要先将 HTML 书签文件转换为 CSV 格式（可使用在线工具或电子表格软件），并确保列标题与项目要求的 `title, url, category, description` 对应。然后在本工具的管理界面中，选择“导入”功能，上传转换后的 CSV 文件即可。未来版本计划直接支持 Netscape 书签 HTML 格式的解析。

**问：静态站点生成模式是否支持自定义主题或模板？**

答：当前版本的静态生成器使用内置的 EJS 模板，样式固定为浅色主题。您可以通过修改 `/src/utils/staticGenerator.js` 中的模板字符串来调整 HTML 结构和内联样式。后续大版本将引入独立的主题目录，允许用户通过放置自定义 CSS 文件和模板文件来完全控制输出外观。

## 许可证

MIT License

Copyright (c) 2026 WebResource Navigator Contributors

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

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:35
