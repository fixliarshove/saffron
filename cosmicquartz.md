# YAS-Index

YAS-Index 是一个面向中文互联网资源聚合与导航的开源项目，定位于对特定主题领域内的多媒体内容网站进行结构化整理、分类归档与访问可用性监测。项目的主要受众为需要系统化查阅该类站点资源的开发者、研究人员及内容消费者，帮助其快速定位可用站点，降低信息检索成本，提升访问效率。

项目本身不存储、不分发、不代理任何第三方内容，仅提供公开站点的元信息与链接整理，遵循互联网资源导航的通用规范。通过自动化的可用性检测与人工维护相结合的方式，确保链接列表的时效性与准确性。

## 功能概览

- **结构化站点目录**：按主题与内容类型对站点进行多级分类，支持通过标签与关键词进行筛选检索。
- **自动化可用性监测**：定时对收录站点进行 HTTP/HTTPS 探活检测，标注访问状态与响应时延。
- **链接变更追踪**：记录站点域名变更、路径调整及协议切换历史，提供变更通知机制。
- **静态页面生成**：基于配置文件一键生成静态导航页面，支持部署至任意 Web 服务器或 CDN。
- **自定义分类标签**：允许用户根据自身需求对站点添加自定义标签与备注，实现个性化管理。
- **访问统计看板**：提供轻量级访问统计面板，展示站点可用率、平均响应时间等关键指标。
- **RSS 订阅输出**：支持生成站点更新状态的 RSS 订阅源，便于用户及时获取变动信息。
- **多格式数据导出**：支持将站点列表导出为 JSON、CSV、Markdown 等多种格式，便于二次开发与数据处理。

## 应用场景

- **主题资源整理与个人知识库构建**：研究人员或内容整理者可以使用 YAS-Index 对特定领域的站点资源进行系统化归档，配合自定义标签与备注功能，构建个人化的主题知识库，便于后续查阅与引用。
- **站点可用性监控与运维辅助**：运维人员或站点管理员可以利用项目的自动化监测功能，定期检查所关注站点的访问状态，及时发现不可用或响应异常的站点，为运维决策提供数据支持。
- **静态导航站快速搭建**：前端开发者或站长可以基于 YAS-Index 的静态页面生成能力，快速搭建一个分类清晰、风格简洁的导航站点，无需从零开始设计数据结构与页面逻辑。
- **数据迁移与平台整合**：当需要将站点列表导入其他系统或平台时，项目提供的多格式数据导出功能（JSON、CSV 等）可以简化数据迁移流程，降低适配成本。

## 快速开始

以下步骤将帮助您在本地环境中快速部署并运行 YAS-Index 服务。

```bash
# 1. 克隆项目仓库
git clone https://github.com/yas-community/yas-index.git
cd yas-index

# 2. 安装项目依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 运行初始化配置与站点检测
python manage.py init --config config/default.yaml
python manage.py check --all

# 4. 启动本地开发服务器
python manage.py serve --port 8080
```

访问本地 `http://127.0.0.1:8080` 即可查看导航界面与监测面板。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 及以上 | 项目核心运行环境，用于执行检测逻辑与后端服务 |
| pip | 22.0 及以上 | Python 包管理工具，用于安装项目依赖 |
| Git | 2.30 及以上 | 用于克隆仓库及版本管理 |
| SQLite | 3.35 及以上 | 默认轻量级数据库，用于存储站点信息与检测记录 |
| curl | 7.68 及以上 | 用于部分检测模块的 HTTP 请求发送（备选方案） |
| cron / systemd | 任意版本 | 用于定时任务配置（生产部署推荐） |
| Docker | 20.10 及以上 | 可选依赖，用于容器化部署 |
| Node.js | 18.0 及以上 | 可选依赖，用于前端静态资源构建（仅开发模式） |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|------|-----------|------------|
| 用户指南 | `docs/user/quickstart.md` | 如何快速上手使用 YAS-Index 的核心功能？ |
| 用户指南 | `docs/user/configuration.md` | 如何自定义配置文件，包括分类、标签与检测参数？ |
| 用户指南 | `docs/user/faq.md` | 常见使用问题与处理建议汇总 |
| 开发者指南 | `docs/developer/architecture.md` | 项目的整体架构设计、模块划分与数据流是怎样的？ |
| 开发者指南 | `docs/developer/api_reference.md` | 后端 API 接口定义与调用示例 |
| 开发者指南 | `docs/developer/contributing.md` | 如何参与项目开发，包括代码规范与提交流程？ |
| 运维指南 | `docs/operator/deployment.md` | 如何将项目部署至生产环境（包括 Docker、Nginx 配置）？ |
| 运维指南 | `docs/operator/monitoring.md` | 如何配置定时检测任务与告警通知？ |

## 资源列表

### 主题分类 - 综合类

- <code>yazhouyiersan.org.cn</code>
- <code>yeyelushipin.org.cn</code>
- <code>shunvshipinwangzhan.org.cn</code>

### 主题分类 - 图像与写真类

- <code>yazhousetutoupai.org.cn</code>
- <code>siwazhifudiyiye.org.cn</code>

### 主题分类 - 视频与影视类

- <code>nannvwuyeshipin.org.cn</code>
- <code>sirenjiatingyingjuyuan.org.cn</code>

### 主题分类 - 人物与写真类

- <code>oumeishunvwang.org.cn</code>

### 主题分类 - 专题内容类

- <code>rihandaxiangjiao.org.cn</code>
- <code>daxiangjiaoyirenjiujiu.org.cn</code>

## 项目结构

```
yas-index/
├── config/                                 # 配置文件目录
│   ├── default.yaml                        # 默认全局配置，含检测间隔、超时参数
│   ├── categories.yaml                     # 站点分类与标签映射定义
│   └── sites/                              # 站点列表分片配置
│       ├── asia.yaml                       # 亚洲区域站点配置
│       └── other.yaml                      # 其他区域站点配置
├── core/                                   # 核心逻辑模块
│   ├── __init__.py
│   ├── checker/                            # 可用性检测子模块
│   │   ├── http.py                         # HTTP/HTTPS 探活实现
│   │   └── scheduler.py                    # 定时调度与任务队列管理
│   ├── parser/                             # 站点信息解析子模块
│   │   ├── extractor.py                    # 从配置中提取站点元数据
│   │   └── validator.py                    # URL 格式与域名合法性校验
│   └── storage/                            # 数据存储子模块
│       ├── database.py                     # SQLite 数据库连接与 ORM 映射
│       └── repository.py                   # 站点记录与检测结果的增删改查
├── web/                                    # Web 服务与前端资源
│   ├── static/                             # 静态资源文件（CSS、JS、图片）
│   │   ├── css/                            # 响应式布局与主题样式
│   │   └── js/                             # 前端交互逻辑与图表渲染
│   ├── templates/                          # Jinja2 模板文件
│   │   ├── index.html                      # 导航首页，展示分类与站点列表
│   │   └── dashboard.html                  # 监测看板，展示可用率与统计图表
│   └── app.py                              # Flask 应用入口与路由定义
├── scripts/                                # 运维与工具脚本
│   ├── init_db.py                          # 初始化数据库表结构与基础数据
│   ├── run_check.py                        # 手动触发全量检测脚本
│   └── export_data.py                      # 导出站点列表为 JSON/CSV 格式
├── tests/                                  # 单元测试与集成测试
│   ├── test_checker.py                     # 检测模块单元测试
│   ├── test_parser.py                      # 解析模块单元测试
│   └── test_api.py                         # API 接口集成测试
├── docs/                                   # 文档目录（详细内容见文档导航）
├── requirements.txt                        # Python 依赖列表
├── Dockerfile                              # 容器化构建文件
├── LICENSE                                 # MIT 许可证文件
└── README.md                               # 项目说明文档（本文件）
```

## 贡献指南

我们欢迎并感谢所有形式的贡献。请遵循以下步骤参与项目开发：

1. 浏览现有 Issue 列表，选择未被指派的议题，或在提出新议题前搜索是否已有类似讨论。建议先通过 Issue 与维护者沟通确认方向，避免重复工作。
2. 将项目仓库复刻（Fork）至个人账号下，并在本地环境中完成开发环境搭建（参照「快速开始」章节）。请确保代码符合 PEP 8 编码规范，并为新增功能编写对应的单元测试。
3. 在本地分支上进行开发，提交信息请采用语义化格式（如 `feat: 添加新的检测协议支持`、`fix: 修复定时任务时区错误`），确保每次提交逻辑完整且可独立审查。
4. 开发完成后，将分支推送至个人复刻仓库，并向主仓库的 `main` 分支发起拉取请求（Pull Request）。请在请求描述中清晰说明变更目的、影响范围及测试结果。
5. 拉取请求将由维护者进行代码审查，必要时会提出修改意见。合并后，您的贡献将被列入项目贡献者名单（除非您要求匿名）。

## 常见问题

**问：YAS-Index 是否存储或代理所收录站点的内容？**

答：不存储、不代理、不缓存任何第三方内容。项目仅记录站点 URL 及其元信息（如标题、分类、标签），所有内容访问均直接跳转至原始站点。用户应在遵守相关法律法规的前提下使用本项目提供的链接导航服务。

**问：自动化可用性检测的频率是多少？是否会对目标站点造成压力？**

答：默认检测间隔为每 24 小时一次，每次检测仅发送单次 HEAD 请求以获取响应状态码，不下载页面内容，对目标站点的负载影响可忽略不计。用户可通过配置文件自定义检测间隔与超时阈值。

**问：如何添加或移除收录站点？**

答：所有站点数据存储于 `config/sites/` 目录下的 YAML 配置文件中。用户可直接编辑该文件，添加新的站点条目（需提供 URL、分类、标签等信息），或删除已有条目。修改保存后，运行 `python manage.py check --all` 即可重新加载配置并更新数据库。对于频繁的批量更新，建议使用项目提供的 `import` 命令从 CSV 文件批量导入。

## 许可证

MIT License

Copyright (c) 2026 YAS-Index Contributors

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
