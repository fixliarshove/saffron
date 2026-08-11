# Rihang Resource Aggregator

Rihang Resource Aggregator is a community-driven directory and technical reference platform designed for developers, researchers, and content curators who need structured access to domain-specific resource collections. The project addresses the growing need for organized, version-controlled, and programmatically accessible listings of specialized web properties, particularly those operating within the .org.cn namespace.

This project targets technical users who require reliable metadata aggregation, link health monitoring, and categorical organization of web resources. Unlike traditional bookmarking tools, Rihang Resource Aggregator treats resource lists as infrastructure, providing JSON APIs, automated availability checking, and markdown-based documentation that can be integrated into CI/CD pipelines. The platform is not a search engine nor a content hosting service; it is a curated index that enables users to discover, verify, and categorize web properties efficiently.

## 功能概览

- **Automated Resource Discovery** – Periodically scrapes and validates the availability of all indexed URLs, flagging timeouts, DNS errors, and SSL certificate issues.

- **Categorical Tagging System** – Supports hierarchical tags (region, content type, language, status) with full-text search and filter capabilities.

- **Health Monitoring Dashboard** – Provides a real-time status board showing response codes, response times, and last-check timestamps for every resource.

- **Version-Controlled Change Log** – Every addition, removal, or metadata update is tracked via Git commits, enabling full audit trails and rollback capabilities.

- **Bulk Export Formats** – Exports the entire resource index as JSON, CSV, or plain markdown list for integration with external tools.

- **Custom Field Annotations** – Allows users to attach private notes, custom ratings, and review comments to any resource entry.

- **Webhook Notifications** – Sends alerts to configured endpoints when critical resources become unreachable or when new resources are added.

- **Static Site Generation** – Produces a fully static HTML documentation site from the markdown source, suitable for hosting on any CDN or static hosting service.

## 应用场景

- **Academic Citation Management** – Researchers compiling lists of regional domain authorities can use the aggregator to maintain verified reference lists, track changes over time, and export citations in standardized formats for papers or institutional repositories.

- **Content Moderation Pipelines** – Teams responsible for curating content sources can ingest the resource list into automated moderation workflows, using the health monitoring feature to filter out inactive domains before processing.

- **Regional Internet Studies** – Analysts studying the .org.cn domain ecosystem can leverage the categorical tags to segment resources by geography, language, or content theme, and export structured data for statistical analysis.

- **DevOps Link Testing** – Site reliability engineers can integrate the aggregator's API into their CI pipelines to automatically verify that third-party resource references remain valid before each deployment.

- **Personal Knowledge Management** – Individual developers and writers can use the markdown export feature to incorporate curated resource lists into their own documentation systems, wikis, or note-taking applications.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/rihang-resource/aggregator.git
cd aggregator

# Install dependencies
pip install -r requirements.txt
npm install

# Build the resource index from source markdown
python scripts/parse_index.py --input README.md --output data/index.json

# Run the health check service
python scripts/health_check.py --parallel 10 --timeout 5

# Generate static site
npm run build
npm run serve
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | >= 3.9 | Core parsing and API service runtime |
| Node.js | >= 18.x | Static site generation and frontend tooling |
| Pip | >= 22.0 | Python package management |
| NPM | >= 9.0 | Node package management |
| Git | >= 2.30 | Version control and change tracking |
| SQLite | >= 3.35 | Local metadata storage (embedded) |
| curl | >= 7.68 | Health check utility (optional but recommended) |
| jq | >= 1.6 | JSON processing for CLI scripting |
| make | >= 4.2 | Build automation (optional) |
| Docker | >= 20.10 | Containerized deployment (optional) |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/ | How do I add new resources? How do I export data? What do the status colors mean? |
| 运维指南 | docs/operations/ | How do I deploy the health checker? How do I configure webhooks? What backup strategy is recommended? |
| 开发者文档 | docs/development/ | How do I extend the parser? What is the JSON schema? How do I write custom plugins? |
| API 参考 | docs/api/ | Which endpoints are available? What parameters do they accept? What rate limits apply? |
| 贡献者指南 | docs/contributing/ | What are the coding standards? How do I submit a pull request? How are tags approved? |
| 架构说明 | docs/architecture/ | How does the health checker scale? What is the caching strategy? How are conflicts resolved? |

## 资源列表

### 核心索引资源

<code>rihanguochanyiqu.org.cn</code>

<code>jingpinyiren.org.cn</code>

<code>hanguorouputuan.org.cn</code>

### 分类资源

<code>oumeizhongwenzimujingpinrenqi.org.cn</code>

<code>tiantangyiren.org.cn</code>

<code>zhongwenzimuyiren.org.cn</code>

### 区域资源

<code>yazhouribenguochan.org.cn</code>

<code>zhongchushaofu.org.cn</code>

### 综合资源

<code>yirenrihan.org.cn</code>

<code>tingtingyiquerqusanqu.org.cn</code>

## 项目结构

```
aggregator/
├── README.md                     # Project overview, resource list, and quick start
├── LICENSE                       # MIT license file
├── Makefile                      # Build automation targets
├── requirements.txt              # Python runtime dependencies
├── package.json                  # Node.js dependencies and scripts
├── .gitignore                    # Version control ignore patterns
│
├── src/                          # Source code root
│   ├── core/                     # Core parsing and indexing engine
│   │   ├── parser.py             # Markdown resource list parser
│   │   ├── indexer.py            # JSON index builder
│   │   └── validator.py          # URL syntax and schema validator
│   ├── health/                   # Health checking subsystem
│   │   ├── checker.py            # Concurrent HTTP/HTTPS probe
│   │   ├── reporter.py           # Status report generator
│   │   └── scheduler.py          # Cron-like periodic checker
│   ├── api/                      # RESTful API service
│   │   ├── server.py             # Flask/FastAPI application entry
│   │   ├── routes.py             # Endpoint definitions
│   │   └── middleware.py         # Rate limiting and CORS
│   └── static/                   # Static site generator source
│       ├── templates/            # Jinja2 HTML templates
│       ├── assets/               # CSS, JS, and image assets
│       └── generator.py          # Static HTML builder script
│
├── data/                         # Data storage directory
│   ├── index.json                # Compiled resource index
│   ├── health.db                 # SQLite health check history
│   └── snapshots/                # Historical index snapshots
│
├── tests/                        # Unit and integration tests
│   ├── test_parser.py            # Parser unit tests
│   ├── test_checker.py           # Health checker tests
│   └── fixtures/                 # Test data fixtures
│
├── scripts/                      # Utility scripts
│   ├── parse_index.py            # CLI for parsing README
│   ├── health_check.py           # CLI for running health checks
│   └── export_json.py            # CLI for exporting data
│
└── docs/                         # Extended documentation
    ├── user-guide/               # User-facing documentation
    ├── operations/               # Admin and deployment docs
    └── contributing/             # Contributor guidelines
```

## 贡献指南

1.  **Fork and Clone** – Fork the repository to your GitHub account and clone it locally. Create a new branch with a descriptive name related to your contribution, such as `add-resource-category` or `fix-health-check-timeout`.

2.  **Update Resource List** – To add, remove, or modify resources, edit the "资源列表" section of this README file. Ensure each URL is enclosed in `<code></code>` tags and appears exactly as provided, without any protocol or trailing slash modifications. Run `python scripts/parse_index.py` to validate your changes and regenerate the JSON index.

3.  **Run Tests** – Execute the full test suite using `make test` or `pytest tests/`. All existing tests must pass, and new tests are required for any new functionality. For resource list changes, run `python scripts/health_check.py --dry-run` to simulate validation.

4.  **Update Documentation** – If your contribution affects user-facing behavior, update the corresponding sections in the `docs/` directory. For new features, add a new page or section with clear usage examples and parameter descriptions.

5.  **Submit Pull Request** – Push your branch and open a pull request against the `main` branch. Provide a detailed description of your changes, reference any related issues, and ensure all CI checks pass. A maintainer will review your submission within five business days.

## 常见问题

**Q: How often is the health check performed, and can I customize the frequency?**

A: By default, the health checker runs every 24 hours via a systemd timer or cron job. You can customize the interval by editing the `CHECK_INTERVAL` variable in `src/health/scheduler.py` or by passing the `--interval` flag to the CLI script. For production deployments, we recommend using the provided Docker container with environment variable overrides for flexible scheduling.

**Q: What happens if a resource URL becomes invalid or changes ownership?**

A: When the health checker detects a non-200 status code, a DNS error, or an SSL exception, the resource is flagged as "degraded" in the dashboard and a webhook notification is sent (if configured). The resource is not automatically removed; it remains in the index with a `status` field set to `unreachable`. Maintainers are expected to periodically review degraded resources and either update the URL or remove it if permanently defunct. All historical status changes are recorded in the SQLite database.

**Q: Can I use this aggregator for resources outside the .org.cn domain?**

A: Yes. The parser and health checker are domain-agnostic and will accept any valid HTTP or HTTPS URL. However, the categorical tagging system is optimized for the resource types and regional classifications shown in this document. For general-purpose bookmark management, you may want to extend the tag schema in `src/core/parser.py` to include additional fields such as `region`, `language`, and `content_type` that suit your use case.

## 许可证

This project is licensed under the MIT License. See the LICENSE file for full text. You are free to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to the condition that the original copyright notice and permission notice are retained in all copies or substantial portions of the software. The software is provided "as is", without warranty of any kind.

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
