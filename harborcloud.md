# WebScore Navigator

WebScore Navigator 是一个面向体育赛事数据分析师、开发者和技术研究人员的开源外链资源聚合与导航系统。该项目并非一个传统的赛事数据平台，而是一个高度结构化的技术资源索引层，专注于收集、分类和展示特定领域的公开数据查询入口与信息源。

项目目标用户包括需要进行数据对比验证的算法工程师、构建体育数据看板的前端开发者、以及从事网络信息聚合研究的学术人员。WebScore Navigator 通过机器可读的目录结构和标准化的资源描述，解决了数据源分散、链接失效难以追踪、以及资源间关系不透明的问题，帮助用户快速定位可信赖的原始信息节点。

## 功能概览

- **智能资源分类引擎**：依据域名语义和路径特征，对海量外链进行自动归类，支持按运动类型、数据地域和数据粒度进行筛选。

- **链接健康状态探测**：内置异步 HTTP 状态检查器，定期验证收录资源的可访问性，并在管理界面中标注异常节点。

- **结构化元数据提取**：从目标页面的 HTML 结构中尝试提取关键数据表的更新时间和字段定义，辅助用户评估数据时效性。

- **自定义标签体系**：允许用户为每个资源链接添加多个自定义标签，构建符合个人或团队研究习惯的分类维度。

- **快速全文检索**：基于倒排索引实现的对资源标题、描述和标签的毫秒级搜索，支持模糊匹配和布尔操作符。

- **开放 API 端点**：提供 RESTful 风格的 JSON 数据导出接口，便于其他系统或脚本批量获取资源列表及其状态信息。

- **导入与导出机制**：支持 CSV 和 JSON 格式的批量链接导入导出，方便进行团队间数据同步或备份。

## 应用场景

- **赛事数据看板开发**：开发人员在构建实时数据可视化大屏时，可通过 WebScore Navigator 快速发现和对比多个公开数据源的结构与响应速度，选择最适合的后端数据接口。

- **学术研究与数据验证**：体育统计学研究者可以利用本系统汇集的多源链接，交叉验证特定比赛的比分记录或运动员统计数据，提高研究结论的可靠性。

- **技术演示与教学**：在技术培训或开源项目演示中，讲师可使用该导航站展示如何从分散的 Web 资源中整合信息，教授学生关于网络抓取、数据解析和资源监控的实践技巧。

- **个人书签管理替代方案**：对于关注特定体育领域的技术爱好者，本系统可作为高级书签管理工具，提供比浏览器自带书签更强大的组织、搜索和状态监控能力。

## 快速开始

以下步骤将指导您在本地环境中快速启动 WebScore Navigator 实例。

```bash
# 1. 克隆项目仓库
git clone https://github.com/webscore-navigator/webscore-navigator.git
cd webscore-navigator

# 2. 安装项目依赖
# 项目使用 Python 3.9+ 和 pipenv 管理依赖
pip install pipenv
pipenv install --dev

# 3. 初始化本地数据库和配置文件
pipenv run python scripts/init_db.py
pipenv run python scripts/load_default_resources.py

# 4. 启动开发服务器
pipenv run python manage.py runserver --host 0.0.0.0 --port 8080
```

服务启动后，访问 `http://localhost:8080` 即可进入本地导航界面。默认管理员账户为 `admin`，密码在初始化脚本输出中显示。

## 安装要求

在部署 WebScore Navigator 之前，请确保您的环境满足以下依赖要求。

| 依赖项 | 必需版本 | 说明 |
| :--- | :--- | :--- |
| Python | 3.9, 3.10, 3.11 | 核心运行环境，不支持 3.8 以下版本 |
| Pipenv | >= 2023.x | 用于管理虚拟环境和依赖包 |
| SQLite | 内置于 Python 标准库 | 默认使用的轻量级数据库，适用于开发和小规模部署 |
| PostgreSQL | >= 13.0 (可选) | 生产环境推荐使用，需额外配置连接信息 |
| Redis | >= 6.2 (可选) | 用于缓存资源健康检查结果，提升性能 |
| Node.js | >= 18.x (仅前端构建) | 仅当需要修改前端静态资源时必需 |

## 文档导航

为帮助不同角色的用户快速找到所需信息，项目文档按以下层面组织。

| 层面 | 目录路径 | 回答的问题 |
| :--- | :--- | :--- |
| 用户手册 | `docs/user_guide/` | 如何添加、编辑和分类资源链接？如何理解健康状态报告？ |
| 开发者指南 | `docs/developer_guide/` | 项目的整体架构是怎样的？如何扩展一个新的资源解析器？ |
| API 参考 | `docs/api_reference/` | 有哪些可用的 REST API 端点？请求和响应的数据结构如何？ |
| 运维手册 | `docs/ops_guide/` | 如何使用 Docker 进行容器化部署？如何配置生产环境的 PostgreSQL 和 Redis？ |

## 资源列表

本系统核心收录的资源链接按类别整理如下。所有链接均保持用户提供的原始格式。

体育比分数据源

- <code>jishibifenzuqiubifenbifenqiutan.net.cn</code>
- <code>lanqiubifenwang.net.cn</code>
- <code>7mbifenjishizuqiubifen.net.cn</code>
- <code>bifenw.com.cn</code>
- <code>bifenwangw.com.cn</code>
- <code>bifenzhibow.com.cn</code>
- <code>7mjishibifenzuqiuw.com.cn</code>
- <code>bifenwangbf.org.cn</code>
- <code>bifenwang365.org.cn</code>
- <code>qiutanzuqiubifen888.org.cn</code>

## 项目结构

项目采用分层架构设计，核心模块与辅助工具分离，便于维护和扩展。

```text
webscore-navigator/
├── manage.py                  # 项目主入口，包含 CLI 命令定义
├── Pipfile                    # 生产与开发环境依赖声明
├── Pipfile.lock               # 依赖版本锁定文件
├── docker-compose.yml         # 容器编排配置（含 PostgreSQL + Redis）
├── Dockerfile                 # 生产环境镜像构建脚本
├── docs/                      # 所有项目文档的根目录
│   ├── user_guide/            # 用户手册，包含界面操作说明
│   ├── developer_guide/       # 开发指南，包含架构设计与插件开发
│   ├── api_reference/         # OpenAPI 规范的接口文档
│   └── ops_guide/             # 部署与运维相关手册
├── src/                       # 项目核心源代码目录
│   ├── core/                  # 核心业务逻辑模块
│   │   ├── resource_manager.py # 资源增删改查与标签管理
│   │   ├── health_checker.py  # 异步链接健康状态检查服务
│   │   └── metadata_extractor.py # 元数据提取抽象类与实现
│   ├── web/                   # Web 界面相关模块
│   │   ├── app.py             # Flask 应用工厂与路由注册
│   │   ├── templates/         # Jinja2 模板文件
│   │   └── static/            # CSS, JavaScript 与图片资源
│   ├── api/                   # RESTful API 实现
│   │   ├── v1/                # API 版本 1 的路由与序列化器
│   │   └── schemas.py         # Pydantic 模型定义
│   └── utils/                 # 通用工具函数集
│       ├── network.py         # 网络请求与超时处理工具
│       └── validators.py      # URL 格式与域名验证函数
├── tests/                     # 单元测试与集成测试目录
│   ├── unit/                  # 针对每个模块的独立测试
│   └── integration/           # 端到端功能测试
├── scripts/                   # 辅助运维与开发脚本
│   ├── init_db.py             # 数据库表结构初始化
│   └── load_default_resources.py # 加载默认资源链接到数据库
└── .env.example               # 环境变量配置模板
```

## 贡献指南

我们欢迎任何形式的贡献，包括但不限于报告问题、提交代码、完善文档或提出新功能建议。请遵循以下流程：

1.  **查阅议题列表**：在提交拉取请求之前，请访问 GitHub Issues 页面，查看是否存在相关或正在进行的讨论，避免重复工作。

2.  **创建功能分支**：从 `main` 分支签出新的功能分支，分支命名应遵循 `feature/简短描述` 或 `fix/问题编号` 的格式。

3.  **编写或更新测试**：对于任何新增代码或缺陷修复，请确保在 `tests/` 目录下添加相应的单元测试，保证代码覆盖率不低于 85%。

4.  **通过本地检查**：提交前，请在本地运行 `pipenv run pytest` 和 `pipenv run flake8` 确保所有测试通过且代码风格符合 PEP 8 规范。

5.  **提交拉取请求**：清晰描述您的更改内容、动机以及可能影响的范围，并关联相关议题编号。

## 常见问题

**问：系统能处理包含非标准端口的 URL 吗？**

答：可以。在资源录入时，系统会尝试解析用户输入的 URL 字符串。只要符合 RFC 3986 标准，包含端口号的链接（例如 `http://example.com:8080/path`）均能被正确存储和访问。健康检查模块也会正确识别端口进行连接测试。

**问：资源健康检查对目标网站有性能影响吗？**

答：影响极小。健康检查模块采用异步并发机制，默认超时设置为 5 秒，且每个检查周期（默认 30 分钟）内对每个资源仅发起一次轻量级的 HEAD 请求，不会对目标服务器造成持续负载。用户可在配置文件中调整检查频率和超时时间。

**问：如何迁移 SQLite 数据库到 PostgreSQL？**

答：项目内置了数据迁移脚本。您只需在 `.env` 环境文件中设置 `DATABASE_URL` 指向您的 PostgreSQL 连接字符串，然后执行 `pipenv run python scripts/migrate_db.py`。该脚本会自动读取 SQLite 数据并完整导入 PostgreSQL，同时保持所有表关系不变。

## 许可证

MIT License

Copyright (c) 2026 WebScore Navigator Contributors

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
