# Rime Resource Aggregator

Rime Resource Aggregator 是一个面向中文输入法用户与语言学习者的外链资源导航与元数据索引项目。项目本身不托管任何视频、字幕或内容文件，仅提供结构化链接索引、资源分类与基础元信息描述，便于用户快速定位互联网上分散的中文字幕、影视资料与语言学习素材。

项目定位为技术型资源导航站，主要服务于以下人群：
- 需要查找中文字幕资源的内容消费用户
- 进行日语、英语、中文多语言字幕对照学习的学习者
- 希望快速获取特定类型影视资源索引的开发者与研究人员

项目不依赖任何后端服务，完全基于静态 Markdown 与 JSON 索引构建，可直接部署于任意静态托管服务，也可本地克隆后通过浏览器打开使用。

---

## 功能概览

- **多维度资源索引**：按语言、地区、内容类型对资源链接进行一级分类，支持快速筛选。

- **元数据标签系统**：为每个资源链接附加语言标签（中文、日语、英语）、地区标签（国产、欧美、日本）及内容类型标签（影视、字幕、学习资料）。

- **批量导入与校验**：提供 JSON 格式的链接库导入接口，并自动校验 URL 可访问性及域名格式合法性。

- **静态搜索支持**：基于纯前端 JavaScript 实现关键词搜索，支持按资源名称、标签、描述进行模糊匹配。

- **资源状态标记**：对每个链接标记活跃状态、最后检测时间与响应码，便于用户识别失效资源。

- **自定义分类视图**：支持按“最新更新”、“热门访问”、“字母排序”三种视图模式切换展示。

- **导出功能**：支持将当前筛选结果导出为 CSV 或 JSON 格式，便于二次处理。

- **离线可用**：所有索引数据内嵌于单 HTML 文件，无需网络即可浏览已有资源列表。

---

## 应用场景

**场景一：日常影视字幕查找**
用户通过项目首页的分类导航，快速定位“中文字幕”类别下的资源链接，直接跳转至目标站点获取字幕文件，用于本地播放器加载。

**场景二：多语言对照学习**
语言学习者使用“日语-中文”或“英语-中文”对照标签，筛选出同时包含多语言字幕的资源链接，配合视频播放器进行逐句对照学习。

**场景三：资源可用性巡检**
运维人员或开发者使用项目提供的批量校验脚本，定期对所有收录链接进行 HTTP 状态检测，生成失效报告并更新索引状态。

**场景四：自定义资源收藏集**
研究人员将项目克隆至本地，按自身研究主题（如“欧美影视中的中文使用场景”）新建分类文件，将相关链接整理为私有收藏集。

---

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境。

```bash
# 1. 克隆项目仓库
git clone https://github.com/rime-resource-aggregator/rra.git
cd rra

# 2. 安装依赖（用于本地预览与校验）
npm install -g serve
pip install requests   # 用于校验脚本

# 3. 启动本地静态服务
serve -s public -p 3000

# 4. （可选）执行链接校验
python scripts/check_urls.py --input data/index.json --output reports/status.json
```

执行完成后，在浏览器中访问 <code>http://localhost:3000</code> 即可浏览资源索引页面。

---

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | >= 14.x | 用于本地开发服务器及构建工具 |
| npm | >= 6.x | 包管理器，用于安装 serve 等工具 |
| Python | >= 3.7 | 运行链接校验脚本（可选） |
| requests 库 | >= 2.25 | Python 脚本依赖，用于 HTTP 检测 |
| 现代浏览器 | Chrome 90+ / Firefox 88+ / Edge 90+ | 前端页面渲染与搜索功能支持 |
| Git | >= 2.25 | 克隆仓库及版本管理 |

---

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | docs/user-guide.md | 如何浏览、搜索、筛选资源链接；如何理解标签分类 |
| 维护手册 | docs/maintainer-guide.md | 如何新增链接、更新元数据、运行校验脚本 |
| 开发者文档 | docs/developer-guide.md | 项目目录结构说明、JSON 数据格式规范、API 设计原则 |
| 部署指南 | docs/deployment.md | 如何将项目部署至 Netlify、Vercel 或 GitHub Pages |
| 常见问题 | docs/faq.md | 收录标准、链接失效处理、更新频率等用户常见疑问 |
| 变更日志 | CHANGELOG.md | 按版本记录新增资源、移除失效链接、功能调整 |

---

## 资源列表

### 中文字幕类

- <code>zhongwenzimudibaye.org.cn</code>

- <code>nvyouzhongwenzimu.org.cn</code>

- <code>zhongwenzimurenqishunv.org.cn</code>

- <code>siwarenqizhongwenzimu.org.cn</code>

### 日韩欧美影视类

- <code>rihanoumeisetu.org.cn</code>

- <code>ribenshunvshipin.org.cn</code>

- <code>oumeilingleishipin.org.cn</code>

- <code>guochanoumeirihanyiqu.org.cn</code>

### 官方站点类

- <code>ludashiguanfangwangzhan.org.cn</code>

### 其他资源类

- <code>mitaojiujiujiu.org.cn</code>

---

## 项目结构

```
rra/
├── public/                         # 静态资源根目录
│   ├── index.html                  # 主页面，包含全部 UI 与内联 JavaScript
│   ├── css/
│   │   ├── base.css                # 基础样式重置与排版
│   │   ├── layout.css              # 网格、导航、卡片布局
│   │   └── theme.css               # 暗色/亮色主题变量
│   ├── js/
│   │   ├── app.js                  # 主应用入口，初始化渲染与事件绑定
│   │   ├── search.js               # 模糊搜索与过滤逻辑
│   │   ├── tags.js                 # 标签解析与分类聚合
│   │   └── export.js               # CSV/JSON 导出功能
│   └── assets/
│       ├── icons/                  # 分类图标 SVG 文件
│       └── fallback/               # 链接失效时的占位图片
├── data/                           # 索引数据目录
│   ├── index.json                  # 主索引，包含全部链接及元数据
│   └── categories.json             # 分类层级定义与显示名称映射
├── scripts/                        # 工具脚本目录
│   ├── check_urls.py               # 批量 HTTP 状态检测
│   ├── generate_sitemap.py         # 生成静态站点地图 XML
│   └── validate_schema.py          # 校验 index.json 是否符合 JSON Schema
├── docs/                           # 项目文档目录
│   ├── user-guide.md
│   ├── maintainer-guide.md
│   ├── developer-guide.md
│   ├── deployment.md
│   └── faq.md
├── tests/                          # 单元测试目录
│   ├── test_search.js              # 搜索功能测试用例
│   └── test_export.js              # 导出功能测试用例
├── .github/
│   └── workflows/
│       └── ci.yml                  # GitHub Actions 持续集成配置
├── CHANGELOG.md                    # 版本变更记录
├── LICENSE                         # MIT 许可证文件
├── README.md                       # 本文件
└── package.json                    # Node.js 项目配置（仅用于开发工具）
```

---

## 贡献指南

欢迎对本项目进行贡献。请遵循以下步骤：

1. **提交 Issue 讨论**  
   在提交拉取请求之前，请先在 Issues 中描述您希望新增的资源链接、分类调整或功能改进，并等待维护者确认可行性。

2. **克隆仓库并创建分支**  
   将主仓库复刻至您的账户，然后克隆至本地。创建以 `feature/` 或 `fix/` 为前缀的分支，例如 `feature/add-jp-resources`。

3. **修改索引数据或代码**  
   - 若新增资源链接，请编辑 `data/index.json`，确保遵循既有的字段结构（包含 url、name、tags、description、status 等）。
   - 若修改前端功能，请同步更新对应的单元测试文件。

4. **运行本地校验**  
   执行 `python scripts/validate_schema.py` 校验 JSON 格式合法性。执行 `python scripts/check_urls.py` 检测新增链接的可用性。

5. **提交拉取请求**  
   推送分支至您的复刻仓库，并向主仓库提交拉取请求。请在描述中引用相关 Issue 编号，并附上校验脚本的输出摘要。

---

## 常见问题

**问：资源链接无法访问，项目会如何处理？**

答：项目会通过定期运行的自动化校验脚本（每周一次）对所有收录链接进行 HTTP HEAD 请求检测。连续三次检测均返回非 2xx/3xx 状态码的链接将被标记为“失效”，并在索引页面中灰显。失效链接将在下一次版本更新时从活跃索引中移除，但会保留在历史归档文件中供参考。

**问：如何请求新增某个资源链接？**

答：请在本项目的 Issues 中提交新链接请求，并附上以下信息：
- 完整 URL（含协议）
- 资源简要描述（语言、类型、内容概要）
- 推荐分类标签
维护者将在 5 个工作日内审核，若符合收录标准（内容稳定、无版权风险、面向中文用户），将纳入下一版索引。

**问：项目是否提供 API 接口？**

答：项目本身为纯静态站点，不提供运行时 API。但您可以直接读取 `data/index.json` 文件作为数据源，该文件遵循固定 JSON Schema，可视为只读 API。开发者也可基于该 JSON 构建自己的前端应用。

---

## 许可证

本项目采用 MIT 许可证。您可以在遵守许可证条款的前提下自由使用、修改、分发本项目的代码与索引数据。有关详细信息，请参阅项目根目录下的 LICENSE 文件。

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:26
