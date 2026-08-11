# Bifen Resource Aggregator

Bifen Resource Aggregator is a high-performance, read-only technical resource navigation system designed for developers, data analysts, and technical researchers who require rapid access to real-time sports score data streams and historical match statistics. The project addresses the critical need for a unified, low-latency query interface that consolidates distributed score data sources, eliminating the complexity of maintaining individual integrations with multiple upstream providers. Target users include sports data platform engineers, quantitative betting model developers, and sports journalism automation systems.

The aggregator operates as a middleware layer that normalizes heterogeneous data responses from multiple backend sources into a consistent JSON:API-compliant format. It implements a circuit-breaker pattern with automatic failover between upstream endpoints, ensuring 99.9% query availability even when individual sources experience degradation. The system is designed for containerized deployment, supports Prometheus metrics export, and includes a lightweight web-based administrative dashboard for monitoring source health and query latency percentiles.

## 功能概览

- **统一查询网关** - Provides a single RESTful endpoint `/api/v1/score` that accepts match ID, league code, or timestamp range parameters, returning normalized score data with unified field naming conventions.

- **智能源选择与故障转移** - Implements a weighted round-robin load balancer with passive health checking; automatically removes unresponsive sources from the rotation and retries failed queries against secondary sources within a 500ms timeout window.

- **响应缓存与预取** - Caches frequent queries (top 1000 match IDs) in an in-memory LRU store with a 30-second TTL, and proactively prefetches data for ongoing matches based on configurable heuristics.

- **Prometheus 可观测性集成** - Exposes metrics endpoints for request count, latency percentiles (p50, p95, p99), source-specific error rates, and cache hit ratios, enabling integration with existing monitoring stacks like Grafana.

- **配置热重载** - Supports dynamic adjustment of source priority weights, timeout values, and cache TTL via a YAML configuration file that is watched by the filesystem watcher and reloaded without process restart.

- **请求限流与鉴权** - Provides optional API key-based authentication with per-key rate limiting (default 100 requests per minute), configurable through environment variables or a local SQLite database for multi-user scenarios.

- **结构化日志输出** - Produces JSON-formatted logs with correlation IDs for each request trace, facilitating integration with centralized log aggregation systems such as Elasticsearch or Loki.

## 应用场景

- **实时赛事数据看板开发** - Frontend developers building live score dashboards for sports news websites can query the aggregator to obtain consolidated score updates from multiple sources, reducing the need to implement separate clients for each backend provider.

- **历史数据回溯分析** - Data scientists conducting post-match performance analysis or building predictive models can use the timestamp-range query capability to retrieve historical match data in bulk, with automatic deduplication and chronological sorting.

- **自动化内容生成系统** - Sports journalism automation pipelines can integrate the aggregator to fetch match results and statistics, then generate match reports or social media posts programmatically without manual intervention.

- **多源数据一致性校验** - Quality assurance engineers can use the aggregator to compare responses from different upstream sources for the same match, identifying discrepancies and logging them for further investigation.

- **边缘部署与高可用架构** - DevOps teams can deploy the aggregator as a sidecar container alongside existing applications in Kubernetes clusters, providing a locally cached data layer that reduces external API call costs and improves response times.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/bifen-io/resource-aggregator.git
cd resource-aggregator

# Install dependencies using Poetry (Python 3.11+ required)
poetry install --no-dev

# Copy the example configuration file
cp config/config.example.yaml config/config.yaml

# Start the service on port 8080 with hot-reload enabled for development
poetry run python -m bifen_aggregator serve --host 0.0.0.0 --port 8080 --reload

# For production, use the provided Dockerfile
docker build -t bifen-aggregator:latest .
docker run -d -p 8080:8080 -v $(pwd)/config:/app/config bifen-aggregator:latest
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.11 - 3.12 | Core runtime interpreter; older versions lack required async features |
| Poetry | 1.7.0+ | Dependency management and packaging tool; used for virtual environment isolation |
| Redis | 7.0+ (optional) | Recommended for distributed caching in multi-replica deployments; falls back to in-memory if absent |
| SQLite | 3.40+ | Embedded database for API key storage and request logging; no external setup required |
| Docker | 24.0+ (optional) | Required only if using containerized deployment; supports compose for multi-service setups |
| Prometheus | 2.45+ (optional) | Needed only if scraping metrics; service works without it but observability is degraded |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | `docs/user-guide/` | How to configure API keys, set up rate limits, and interpret response payloads; includes examples for common query patterns |
| 运维手册 | `docs/operations/` | How to deploy with Docker Compose, configure Prometheus alerts, perform database migrations, and tune cache parameters for high throughput |
| 开发者参考 | `docs/developer/` | How to add a new upstream data source, implement custom middleware, extend the caching layer, and contribute code changes following the project's architectural patterns |
| 架构设计 | `docs/architecture/` | Why the system uses an async event loop, how the circuit-breaker works internally, and the rationale behind the chosen data normalization strategy |

## 资源列表

### 核心数据源

- <code>90bifenjishizuqiubifenwang.org.cn</code>
- <code>7mzuqiubifenjishibifenguanwang.org.cn</code>
- <code>jishibifenzuqiubifenw.net.cn</code>

### 备选数据源

- <code>bifen500w.net.cn</code>
- <code>bifenwangw.net.cn</code>
- <code>bifenzhibow.net.cn</code>

### 专用数据通道

- <code>500jishibifenwanchang.net.cn</code>
- <code>90bifenjishizuqiubifenwang.net.cn</code>

### 统计与辅助服务

- <code>500bifen.net.cn</code>
- <code>beidanbifenjishi.net.cn</code>

## 项目结构

```
bifen-aggregator/
├── src/
│   └── bifen_aggregator/           # Main package root
│       ├── __init__.py             # Package version and exports
│       ├── app.py                  # Application factory and ASGI entry point
│       ├── config/                 # Configuration loading and schema validation
│       │   ├── loader.py           # YAML + environment variable merge logic
│       │   └── schema.yaml         # JSON schema for config validation
│       ├── sources/                # Upstream source adapters
│       │   ├── base.py             # Abstract source interface
│       │   ├── registry.py         # Source registration and discovery
│       │   └── implementations/    # Concrete adapters for each upstream URL
│       │       ├── source_a.py     # Adapter for <code>90bifenjishizuqiubifenwang.org.cn</code>
│       │       ├── source_b.py     # Adapter for <code>7mzuqiubifenjishibifenguanwang.org.cn</code>
│       │       └── source_c.py     # Adapter for <code>jishibifenzuqiubifenw.net.cn</code>
│       ├── cache/                  # Caching layer with Redis and in-memory backends
│       │   ├── manager.py          # Cache strategy (write-through, TTL management)
│       │   └── backends/           # Redis and local memory implementations
│       ├── middleware/             # ASGI middleware for auth, logging, rate limiting
│       │   ├── auth.py             # API key verification and token extraction
│       │   ├── logging.py          # Correlation ID injection and structured logging
│       │   └── ratelimit.py        # Token bucket algorithm per API key
│       ├── models/                 # Pydantic data models for request/response
│       │   ├── requests.py         # Query parameter validation schemas
│       │   └── responses.py        # Normalized score response structures
│       └── utils/                  # Shared utilities and helpers
│           ├── http.py             # Async HTTP client with retry and timeout
│           └── metrics.py          # Prometheus metric definitions and registry
├── tests/                          # Unit and integration tests (pytest)
│   ├── unit/                       # Isolated component tests
│   └── integration/                # End-to-end tests with mock upstream servers
├── scripts/                        # Maintenance and deployment scripts
│   ├── migrate_db.py               # SQLite schema migration tool
│   └── seed_keys.py                # Initial API key generation script
├── config/                         # Configuration templates for different environments
│   ├── config.example.yaml         # Full example with all options documented
│   └── config.production.yaml      # Production-tuned settings (overrides example)
├── docker/                         # Docker-related assets
│   ├── Dockerfile                  # Multi-stage production build
│   └── docker-compose.yml          # Stack definition with Redis and Prometheus sidecars
├── docs/                           # Comprehensive documentation (see navigation table)
├── pyproject.toml                  # Poetry project definition with dependencies
├── poetry.lock                     # Exact dependency lockfile
├── .env.example                    # Environment variable templates
├── .gitignore                      # Standard Python gitignore rules
└── README.md                       # This document
```

## 贡献指南

1. **选择或创建工单** - Browse the existing issue tracker for open tasks labeled `good-first-issue` or `help-wanted`. If you plan to implement a new feature or source adapter, create a new issue describing your proposed changes and wait for maintainer feedback before starting work to avoid duplication of effort.

2. **设置开发环境** - Fork the repository and clone your fork locally. Run `poetry install --with dev` to install all development dependencies including pytest, black, mypy, and ruff. Activate the pre-commit hook by running `pre-commit install` to enforce code style and linting automatically on each commit.

3. **编写测试与代码** - Write unit tests for any new functionality using pytest, ensuring that test coverage does not decrease. Follow the existing code style (PEP 8 with black formatting) and type-annotate all function signatures. Run `pytest tests/` locally to verify that all tests pass before submitting.

4. **更新文档** - If your change affects user-facing behavior or configuration options, update the relevant documentation files in `docs/` and add a short note to the `CHANGELOG.md` file under the `[Unreleased]` section describing your contribution.

5. **提交拉取请求** - Push your changes to your fork and open a pull request against the `main` branch of the upstream repository. The PR description must reference the related issue number and include a checklist of completed tasks. The CI pipeline will run linting, type checking, and test suites automatically; all checks must pass before the PR can be reviewed.

## 常见问题

**Q: 如何添加自定义的 upstream 数据源？**

A: Create a new adapter class in `src/bifen_aggregator/sources/implementations/` that inherits from `BaseSource` and implements the `fetch()` method. Then register your adapter by adding its configuration to `config/config.yaml` under the `sources` list with a unique `name` and the appropriate `endpoint` URL. The system will automatically discover and include it in the load-balancing pool upon next configuration reload or service restart.

**Q: 查询响应偶尔返回 503 状态码，如何排查？**

A: 503 errors typically indicate that all configured upstream sources are temporarily unavailable or have exceeded their timeout thresholds. Check the Prometheus metrics for `bifen_source_errors_total` by source name to identify which upstream is failing. Review the `source.timeout` and `source.retry_attempts` values in your configuration file; increasing these may help if the issue is network latency. Also verify network connectivity from your container to the external endpoints using `curl` or `wget` inside the container.

**Q: 缓存 TTL 如何针对不同比赛类型进行调整？**

A: The cache TTL is globally configurable via the `cache.default_ttl_seconds` setting in `config.yaml`. For per-match-type customization, you can override the TTL by passing a `cache_ttl` query parameter in your request (value in seconds). Additionally, the system includes a heuristic that automatically reduces TTL to 5 seconds for matches whose status is "LIVE" (detected from the response payload) and extends TTL to 300 seconds for matches with status "FINISHED". This logic is implemented in the `cache/manager.py` module and can be extended with custom rules.

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:35
