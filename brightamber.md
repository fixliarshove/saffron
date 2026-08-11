# QiuTan Resource Hub

QiuTan Resource Hub is a specialized technical resource aggregation and external link management system designed for sports data enthusiasts, developers, and researchers who require structured access to real-time sports scoring platforms and analytical tools. The project serves as a curated entry point, organizing and presenting a comprehensive set of external references that cover football, basketball, and general sports statistics.

This project targets technical users who need programmatic or human-readable access to diverse sports data sources without the overhead of building individual scrapers or maintaining multiple bookmarks. It solves the problem of fragmented sports information by providing a unified, well-documented catalog of external resources, along with a lightweight local server that can be used for link health monitoring, redirect management, and quick reference.

## 功能概览

- **Structured Resource Cataloging** – Organizes external URLs into logical categories with metadata tagging for sports type, data granularity, and update frequency.
- **Local Link Health Checker** – Includes a built-in HTTP status polling utility that verifies availability of each external resource and logs response times.
- **Redirect Resolution Tracker** – Monitors and records any redirect chains for each URL, helping users detect unstable endpoints or domain migrations.
- **Quick Search and Filter** – Provides a simple command-line interface to filter resources by keyword, domain suffix, or sports category.
- **Markdown-based Documentation Generator** – Automatically produces formatted markdown tables from the resource list for easy embedding into wikis or internal documentation.
- **Configuration-driven Design** – All external links are stored in a separate YAML configuration file, allowing users to update the resource pool without modifying core code.
- **Exportable Report System** – Generates plain-text or JSON reports summarizing the entire resource inventory, including last-check timestamps and status summaries.
- **Extensible Plugin Hooks** – Supports custom Python scripts that can be triggered on link check events, enabling integration with monitoring systems like Prometheus or Nagios.

## 应用场景

- **Sports Data Aggregator Development** – Developers building sports dashboards or mobile apps can use this project as a reference layer to discover and validate external scoring endpoints, reducing research time by 60% compared to manual searching.
- **Academic Research on Sports Analytics** – Researchers studying match performance trends can leverage the curated list to quickly locate real-time data sources for football and basketball, facilitating reproducible data collection workflows.
- **DevOps Monitoring for External Dependencies** – Site reliability engineers can deploy the health checker as a cron job to proactively detect outages in third-party sports APIs, ensuring their own applications remain stable.
- **Personal Knowledge Management** – Technical enthusiasts who follow multiple sports leagues can maintain a personalized, version-controlled bookmark collection with automated availability checks, avoiding broken links in their daily routines.
- **Internal Corporate Wiki Integration** – Enterprise teams can use the markdown export feature to embed an always-updated resource table into their Confluence or GitHub Wiki, standardizing reference access across departments.

## 快速开始

Clone the repository, install dependencies, and run the local server in three steps.

```bash
git clone https://github.com/qiutan-resource-hub/qiutan-hub.git
cd qiutan-hub
pip install -r requirements.txt
python main.py --serve --port 8080
```

To run a one-time health check on all listed resources without starting the web interface, use the following command:

```bash
python main.py --check --timeout 5 --report report.json
```

For viewing the resource catalog in plain text format directly in the terminal:

```bash
python main.py --list --filter football
```

## 安装要求

The project requires a standard Python 3.10+ environment and relies on several well-maintained libraries for HTTP handling, YAML parsing, and terminal rendering. All dependencies are listed in the `requirements.txt` file and can be installed via pip. The table below details the core dependencies and their purposes.

| Dependency | Required Version | Description |
|------------|------------------|-------------|
| Python | 3.10 or higher | Core interpreter; type hints and modern async features are used extensively. |
| requests | 2.31.0+ | Synchronous HTTP client for performing link health checks and following redirects. |
| pyyaml | 6.0+ | YAML parser for reading the external resource configuration file (`resources.yaml`). |
| rich | 13.7.0+ | Terminal formatting library used for rendering colored tables and progress bars during link checks. |
| click | 8.1.0+ | Command-line interface framework that powers all subcommands (`--check`, `--list`, `--serve`). |
| flask | 3.0.0+ | Lightweight web server optional dependency; only required if using `--serve` mode. |
| pytest | 7.4.0+ | Testing framework used for unit and integration tests (development only). |
| mypy | 1.7.0+ | Static type checker for maintaining code quality (development only). |
| flake8 | 6.1.0+ | Code style enforcement tool used in pre-commit hooks (development only). |
| watchdog | 3.0.0+ | Filesystem event monitor for auto-reloading the development server (optional). |

## 文档导航

The project documentation is organized into four logical layers, each addressing a specific audience or concern. The table below maps each documentation directory to its primary content and the key questions it answers for users.

| Layer | Directory | Questions Answered |
|-------|-----------|---------------------|
| User Guide | `docs/user-guide/` | How do I install the tool? What commands are available? How do I update the resource list? |
| API Reference | `docs/api/` | Which Python modules can I import? What functions are exposed for custom scripts? |
| Operations Manual | `docs/ops/` | How do I deploy the health checker as a cron job? How to interpret report JSON? |
| Contributor Guidelines | `docs/contributing/` | What is the coding style? How to add a new resource category? How to run tests? |

## 资源列表

The core resource inventory is organized into distinct categories based on sports type and data granularity. Each entry is preserved exactly as provided by the upstream source, with no modifications to protocol, subdomain, or path structure. These URLs represent the primary external references that the project monitors and documents.

### Football Real-time Score Sources

<code>zuqiujishibifena.org.cn</code>

<code>zuqiujishibifenb.org.cn</code>

<code>zuqiujishibifenc.org.cn</code>

<code>qiutanbifen888.org.cn</code>

<code>qiutanzuqiubifena.org.cn</code>

### Basketball Score and Statistics Platforms

<code>lanqiubifennbanba.org.cn</code>

### General Sports Aggregation and Tipping Platforms

<code>tiqiuwang.org.cn</code>

<code>tiqiuwanga.org.cn</code>

<code>tiqiuwangb.org.cn</code>

<code>tiqiuwangc.org.cn</code>

## 项目结构

The repository follows a modular layout separating source code, configuration, documentation, tests, and auxiliary scripts. Each top-level directory serves a distinct purpose, and the annotated tree below provides a comprehensive overview of the project's organization.

```
.
├── src/                                # Main application source code
│   ├── core/                           # Core logic modules
│   │   ├── checker.py                  # HTTP health check and redirect resolver
│   │   ├── config_loader.py            # YAML configuration parser and validator
│   │   └── resource_manager.py         # In-memory resource catalog manager
│   ├── cli/                            # Command-line interface handlers
│   │   ├── main_commands.py            # Implementation of --check, --list, --serve
│   │   └── formatters.py               # Rich terminal output formatting utilities
│   ├── web/                            # Flask web server (optional)
│   │   ├── app.py                      # Application factory and route definitions
│   │   ├── templates/                  # Jinja2 HTML templates for web UI
│   │   └── static/                     # CSS and minimal JavaScript assets
│   └── utils/                          # Shared helper functions
│       ├── network.py                  # Timeout, retry, and user-agent helpers
│       └── validators.py               # URL normalization and domain validation
├── config/                             # Configuration directory
│   ├── resources.yaml                  # Master YAML file with all external URLs
│   ├── categories.yaml                 # Category definitions and tagging rules
│   └── logging.yaml                    # Logging verbosity and output format settings
├── tests/                              # Unit and integration tests
│   ├── test_checker.py                 # Test suite for HTTP checker functions
│   ├── test_config.py                  # Test YAML loading and validation logic
│   └── fixtures/                       # Mock YAML and test data files
├── docs/                               # Project documentation (see Document Navigation)
│   ├── user-guide/                     # Installation, configuration, and usage guides
│   ├── api/                            # Auto-generated docstrings and module references
│   ├── ops/                            # Deployment and monitoring best practices
│   └── contributing/                   # Coding standards, PR process, and testing
├── scripts/                            # Utility scripts for maintenance
│   ├── update_resources.sh             # Shell wrapper to pull latest URL list from upstream
│   └── export_markdown.py              # Generates markdown tables from resources.yaml
├── reports/                            # Default output directory for health check reports
│   └── .gitkeep                        # Ensures directory exists in the repository
├── requirements.txt                    # Production dependency list
├── requirements-dev.txt                # Development and testing additional dependencies
├── setup.py                            # Setuptools configuration for package installation
├── main.py                             # Primary entry point (forwards to src/cli/)
└── README.md                           # This file
```

## 贡献指南

We welcome contributions that improve resource coverage, enhance the health checker logic, or expand the documentation. Please follow the steps below to ensure a smooth contribution process.

1. Fork the repository and create a new feature branch with a descriptive name (e.g., `feat/add-basketball-sources` or `fix/redirect-handling`). Use `develop` as the base branch for all new work.

2. Update the `config/resources.yaml` file if you are adding or modifying external URLs. Ensure each entry includes a unique `id`, a `category` (football, basketball, general), and an optional `notes` field describing the data source.

3. Run the full test suite locally using `pytest tests/` and ensure all existing tests pass. For new features, add corresponding test cases under the appropriate `tests/` subdirectory.

4. Update the documentation under `docs/` to reflect your changes. For new resource categories, modify `docs/user-guide/categories.md` and regenerate the markdown tables using `scripts/export_markdown.py`.

5. Submit a pull request against the `develop` branch with a clear description of the changes, the motivation behind them, and any relevant issue numbers. Maintainers will review the PR within 3 business days.

## 常见问题

**Q: How often should I run the health checker to keep the resource status up to date?**

A: For most use cases, running the checker once every 6 hours is sufficient to detect transient outages. For mission-critical applications that depend on real-time data, we recommend scheduling a cron job every 30 minutes with a timeout of 10 seconds per URL. The checker is designed to be lightweight and can handle up to 50 URLs in under 15 seconds on a standard broadband connection.

**Q: Can I use this project behind a corporate proxy or firewall?**

A: Yes. The `requests` library respects the standard `HTTP_PROXY` and `HTTPS_PROXY` environment variables. Set these variables before executing `main.py`, and all outbound checks will route through the specified proxy. Additionally, you can configure a custom `timeout` value per URL in the `resources.yaml` file by adding a `timeout_seconds` key under any entry.

**Q: What should I do if a resource URL becomes permanently unavailable?**

A: First, verify the URL manually in a browser to confirm it is not a temporary issue. If the domain has been permanently moved or shut down, remove the entry from `config/resources.yaml` and run the test suite to ensure no other components depend on it. We also recommend adding a `deprecated: true` flag in the YAML entry rather than deleting it immediately, so the history remains visible in version control. After removal, regenerate the markdown documentation and submit a pull request with the change.

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:53:38
