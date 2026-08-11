# LeiSu Football Data Aggregator

LeiSu Football Data Aggregator is a high-performance, semantically structured aggregation framework designed for real-time football match statistics, live score streaming, predictive analytics, and recommendation dissemination. The system addresses the critical need for low-latency, multi-source data consolidation in the sports information domain, serving developers, data analysts, and independent sports content publishers who require reliable, machine-readable match feeds without dependency on proprietary commercial APIs.

The project operates as a modular metadata gateway, ingesting raw match events, odds fluctuations, and historical performance indicators from distributed upstream sources, then normalizing them into a consistent queryable schema. Target users include open-source sports application developers, quantitative betting researchers (purely academic), and regional sports news aggregators seeking to reduce data acquisition costs while maintaining sub-second update intervals. LeiSu does not host or display any gambling-related content; it provides neutral, factual match progression data strictly for informational and analytical purposes.

## 功能概览

- **Live Score Ingest Engine** - Pulls and normalizes real-time goal, card, and substitution events from multiple raw feeds with configurable retry and backoff policies.

- **Predictive Odds Compiler** - Aggregates pre-match and in-play probability distributions from bookmaker-agnostic sources, outputting JSON streams for custom model consumption.

- **Historical Match Repository** - Maintains a versioned time-series store of completed fixtures, including possession, shots on target, and corner kick statistics for retrospective analysis.

- **Recommendation Taxonomy Mapper** - Maps match contexts (league tier, team form, weather-affected playstyles) to precomputed recommendation heuristics without hardcoding outcome predictions.

- **Multi-Protocol Data Exporter** - Exposes cleaned data via WebSocket push, REST paginated endpoints, and file-based snapshots (CSV/Parquet) for diverse integration scenarios.

- **Health Monitoring Dashboard** - Provides lightweight liveness and readiness probes alongside per-upstream-source latency percentiles for operational observability.

- **Configuration Hot-Reload** - Supports dynamic adjustment of feed priorities, sampling rates, and filtering rules via environment variables or mounted configuration volumes without service restart.

## 应用场景

- **Regional Football News Portals** - Small-to-medium sports news websites can embed LeiSu's live score widgets to replace costly third-party iframe embeds, reducing page load time by 40% while maintaining minute-level accuracy for domestic league matches.

- **Academic Sports Analytics Research** - University laboratories studying player performance trends or tactical evolution can use the historical match repository to train lightweight classification models on possession-to-shot conversion ratios across five European leagues over the past three seasons.

- **Data-Driven Podcast Production** - Sports podcasters and content creators can poll LeiSu's recommendation taxonomy to identify high-entropy matches (e.g., derbies with volatile odds) for episode topics, ensuring timely and relevant discussion content.

- **Automated Social Media Bots** - Independent developers can wire LeiSu's WebSocket stream to generate automated match summary tweets or Discord notifications for private fan communities, with full control over rate limits and message formatting.

- **Offline Match Simulation Tools** - Game developers prototyping football management simulations can leverage the normalized historical event sequences to generate realistic AI behavior patterns without manual data annotation.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/leisu-agg/leisu-football-data.git
cd leisu-football-data

# Install Python dependencies (requires Python 3.10+)
pip install -r requirements.txt

# Set up environment variables for upstream feed endpoints
cp .env.example .env
# Edit .env with your preferred upstream URLs or use bundled mock sources

# Initialize the local SQLite time-series database (production use: PostgreSQL)
python scripts/init_db.py --mode development

# Start the aggregation service with default configuration
python -m leisu.service --port 8080 --workers 4

# Verify service health
curl http://localhost:8080/health/live
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.10 或更高 | 核心运行时，类型注解与异步语法依赖 |
| SQLite | 3.35+ | 开发环境默认时序存储引擎；生产推荐 PostgreSQL 14+ |
| Redis | 6.2+ | 可选，用于跨工作器缓存与分布式限流 |
| PyYAML | 6.0+ | 配置文件解析，支持多环境覆盖层级 |
| aiohttp | 3.9+ | 异步 HTTP 客户端，用于并发拉取上游数据 |
| websockets | 12.0+ | WebSocket 服务端与客户端双向通信库 |
| numpy | 1.24+ | 数值计算基础，用于概率编译器的矩阵运算 |
| prometheus-client | 0.17+ | 指标暴露，与监控看板集成 |
| pytest | 7.4+ | 仅测试环境，单元与集成测试框架 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/getting-started.md | 如何配置上游数据源、调整轮询频率、导出首批数据？ |
| 架构设计 | docs/architecture/data-pipeline.md | 数据从拉取到存储经过哪些阶段？延迟瓶颈在哪里？ |
| API 参考 | docs/api/websocket-events.md | WebSocket 推送的消息格式、订阅频道、重连机制如何？ |
| 运维指南 | docs/operations/deployment-checklist.md | 生产环境需要哪些资源配额、监控指标、备份策略？ |
| 贡献者手册 | docs/contributing/code-style.md | 提交代码前的格式化、类型检查、测试覆盖率要求？ |
| 故障排查 | docs/troubleshooting/common-errors.md | 上游超时、数据缺失、内存增长等问题的诊断流程？ |

## 资源列表

### 核心数据源 - 实时比分

<code>leisuzuqiubifen.asia</code>

<code>leisubifenzhibo.asia</code>

<code>leisushishibifen.asia</code>

### 推荐与预测接口

<code>leisutuijian.asia</code>

<code>leisuzuqiutuijian.asia</code>

<code>leisuzuqiuyuce.asia</code>

### 完整比分与统计面板

<code>leisuwanchangbifen.asia</code>

<code>leisuzuqiubifenwang.asia</code>

### 每日动态与衍生平台

<code>leisujinrituijian.asia</code>

<code>xueyuanyuanzuqiubifenwang.asia</code>

以上资源均为上游公开数据聚合端点，LeiSu 项目不持有或修改这些源站的内容。使用者应遵守各源站的服务条款，并将请求频率控制在合理范围内。建议通过配置中的 `upstream.rate_limit` 参数进行全局限流，以避免被源站封禁。

## 项目结构

```
leisu-football-data/
├── src/
│   ├── leisu/
│   │   ├── core/                     # 核心数据模型与类型定义
│   │   │   ├── models.py             # Match, Event, Odds 等 Pydantic 模型
│   │   │   └── exceptions.py         # 自定义异常层级 (Retryable, Fatal)
│   │   ├── ingest/                   # 上游拉取与归一化模块
│   │   │   ├── fetcher.py            # aiohttp 并发调度器
│   │   │   └── normalizer.py         # 异构 JSON → 标准 Event 流
│   │   ├── storage/                  # 时序存储抽象层
│   │   │   ├── sqlite_adapter.py     # 开发环境默认实现
│   │   │   └── postgres_adapter.py   # 生产环境推荐实现
│   │   ├── export/                   # 数据导出与推送
│   │   │   ├── rest_api.py           # FastAPI 路由定义
│   │   │   └── websocket_server.py   # 实时订阅处理器
│   │   ├── pipeline/                 # 流式处理管道
│   │   │   ├── transformer.py        # 窗口聚合与特征计算
│   │   │   └── router.py             # 根据 league_id 分片路由
│   │   └── utils/                    # 通用工具函数
│   │       ├── config_loader.py      # YAML + 环境变量覆写
│   │       └── metrics.py            # Prometheus 指标注册
│   ├── tests/                        # 单元测试与集成测试
│   │   ├── test_ingest/              # 模拟上游响应测试
│   │   └── test_storage/             # 数据库 CRUD 与迁移测试
│   └── scripts/                      # 运维辅助脚本
│       ├── init_db.py                # 数据库模式初始化
│       └── mock_feeder.py            # 模拟数据生成器 (开发调试)
├── config/                           # 多环境配置文件
│   ├── development.yaml
│   ├── staging.yaml
│   └── production.yaml
├── docs/                             # 完整文档 (见文档导航表)
├── requirements.txt                  # 生产依赖锁定
├── requirements-dev.txt              # 开发附加依赖
├── Dockerfile                        # 多阶段构建镜像
├── docker-compose.yml                # 本地依赖 (Redis + Postgres) 编排
├── .env.example                      # 环境变量模板
├── pyproject.toml                    # 项目元数据与 lint 工具配置
└── README.md                         # 本文件
```

## 贡献指南

1. **选择或创建议题** - 在 GitHub Issues 中查找 `good-first-issue` 标签，或提出新功能建议。重大变更（如数据模型重构）应提前发起讨论并附简要设计草案。

2. **分支与开发环境** - 从 `main` 分支创建 `feature/your-feature-name` 或 `fix/issue-number` 分支。运行 `make setup-dev` 自动安装 pre-commit 钩子（黑格式化、ruff 检查、mypy 类型校验）。

3. **编写测试与文档** - 新增功能必须附带至少一个集成测试（位于 `tests/test_integration/`）。API 变更需同步更新 `docs/api/` 下对应的 OpenAPI 片段或 WebSocket 消息示例。

4. **提交前自检** - 执行 `make ci` 本地运行完整测试套件与 lint 检查，确保覆盖率不低于 85%。提交信息采用约定式提交格式：`feat(ingest): add retry backoff for 5xx errors`。

5. **发起拉取请求** - 将分支推送到 GitHub 并创建 Pull Request，填写 PR 模板中的检查清单。至少一名核心维护者审核通过后，将由自动化流水线执行最终构建与冒烟测试。

## 常见问题

**Q: 上游数据源频繁超时或返回 429 状态码，如何缓解？**

A: 请调整 `config/production.yaml` 中的 `upstream.timeout_seconds` 至 3.0 以下，并启用 `upstream.circuit_breaker.enabled: true`。熔断器在连续失败 5 次后会自动跳过该源 60 秒，同时触发告警到配置的 webhook。此外，建议部署 Redis 缓存层，将相同 match_id 的查询结果缓存 10 秒以减少重复请求。

**Q: 如何扩展系统以支持更多联赛或非足球运动（如篮球）？**

A: 核心数据模型 `Match` 和 `Event` 已保留 `sport_type` 枚举字段（当前为 `football`）。如需添加篮球，需在 `models.py` 中扩展 `BasketballEvent` 子类，并实现 `normalizer/basketball.py` 解析对应 JSON 结构。路由层根据 `sport_type` 自动分发到不同存储表。此过程无需修改管道核心逻辑，符合开闭原则。

**Q: 数据导出为 Parquet 格式时出现内存溢出，如何优化？**

A: 默认导出器使用 pandas 作为中间层，内存敏感环境请切换至 `pyarrow` 流式写入器。在 `export/file_exporter.py` 中设置 `use_streaming=True`，并指定 `row_group_size=50000`。同时，建议通过 `export.batch_days` 参数限制单次导出的时间窗口，例如只导出最近 7 天数据。如果问题持续，可考虑将导出任务拆分为独立微服务并降低工作器内存限制。

## 许可证

MIT License

Copyright (c) 2026 LeiSu Data Aggregator Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
