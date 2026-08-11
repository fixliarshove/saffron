# Datalink Resource Aggregator

Datalink Resource Aggregator is a curated, high-availability technical index system designed for developers, researchers, and content archivists who require structured access to specialized international digital resources. The project addresses the common failure modes of link rot, domain drift, and category fragmentation by providing a stable, versioned manifest of domain-level references across multiple cultural and linguistic verticals. Unlike traditional bookmark managers or browser sync services, Datalink operates as a static, auditable catalog that can be deployed locally, mirrored independently, or integrated into larger data pipeline workflows. The target audience includes data journalists performing longitudinal content analysis, localization engineers verifying regional asset accessibility, and infrastructure teams maintaining compliance inventories for external service dependencies. The project does not host, proxy, or modify any third-party content; it solely maintains a deterministic, human-reviewed mapping of domain identifiers to their intended functional categories, with rigorous change tracking and availability probing.

## 功能概览

- **Deterministic Domain Manifest** – Maintains a fixed, version-pinned list of external domain references with SHA-256 checksums for each entry, enabling reproducible environment builds and dependency verification.

- **Category-Based Indexing** – Organizes resources into semantic groups such as regional cultural archives, media asset repositories, and linguistic corpora, with each entry tagged by geographic origin, content type, and update frequency.

- **Availability Health Check** – Integrates a lightweight HTTP HEAD probe that runs on a configurable schedule, reporting response status codes, TLS certificate expiry windows, and redirect chains for every listed domain.

- **Static HTML Generation** – Produces a fully self-contained, responsive HTML dashboard from the manifest data, suitable for serving via any static hosting platform or local file browser without runtime dependencies.

- **Import/Export Adapters** – Supports bidirectional conversion between the internal YAML manifest format and CSV, JSON Lines, and plain-text domain lists, facilitating interoperability with external monitoring tools and spreadsheet applications.

- **Delta Reporting** – Generates human-readable change logs between manifest versions, highlighting newly added domains, removed entries, and modified URL strings with before-and-after diff views.

- **Custom Tagging Engine** – Allows users to attach arbitrary key-value metadata to each domain entry, such as maintenance contact, internal project code, or regulatory classification, without modifying the core schema.

## 应用场景

- **Regional Content Archiving Workflows** – Research teams conducting longitudinal studies on online cultural expression can use the manifest as a stable sampling frame. The versioned nature ensures that repeat crawls or API queries reference the exact same domain set across multiple data collection waves, eliminating a common source of sampling bias.

- **Localization Pipeline Dependency Management** – Localization engineers responsible for fetching media assets or terminology databases from region-specific providers can embed the manifest into their build toolchain. The health check module proactively notifies the team when a referenced domain becomes unreachable, allowing manual fallback or alternative routing before production deployments fail.

- **Compliance Inventory Auditing** – Legal and compliance officers tasked with maintaining an up-to-date roster of external data sources used by internal applications can leverage the manifest as a single source of truth. The delta reporting feature simplifies quarterly audit reviews by clearly delineating which external references changed since the previous review period.

- **Offline-First Development Environments** – Developers working in air-gapped or restricted-network environments can pre-fetch the manifest and use the static HTML dashboard as a local reference catalog. The absence of external API calls during dashboard rendering ensures that the tool remains functional even when the listed domains are unreachable.

## 快速开始

The following procedure assumes a standard Linux or macOS environment with Python 3.9 or later and Git installed. Windows users are advised to use Windows Subsystem for Linux (WSL) or Git Bash with equivalent package dependencies.

```bash
# Clone the repository from the official source
git clone https://github.com/datalink-resource-aggregator/datalink-core.git
cd datalink-core

# Install the required Python dependencies using pip and the provided requirements file
pip install -r requirements.txt

# Generate the initial manifest from the bundled YAML template and verify syntax
python cli.py manifest validate --input manifests/current.yaml

# Run the availability health check against all listed domains (concurrent, timeout 5s per domain)
python cli.py health check --manifest manifests/current.yaml --output reports/health-report.json

# Build the static HTML dashboard into the ./build directory with default theme
python cli.py build html --manifest manifests/current.yaml --output build/ --title "Datalink Resource Catalog"

# Open the generated dashboard in the default web browser (Linux/macOS)
open build/index.html
```

For production deployments, it is recommended to schedule the health check via a cron job or systemd timer and to store historical reports in a dedicated data directory with appropriate retention policies.

## 安装要求

The following table enumerates all mandatory and optional dependencies required for full functionality. All version constraints are expressed as minimum supported versions; later patch releases are expected to be compatible unless otherwise noted in the release notes.

| 依赖 | 必需 | 说明 |
|------|------|------|
| Python 3.9+ | 是 | Core runtime interpreter. Used for all CLI modules, manifest parsing, and health check workers. |
| PyYAML 6.0+ | 是 | YAML manifest parsing and serialization. Required for all operations that read or write the manifest file. |
| aiohttp 3.9+ | 是 | Asynchronous HTTP client for health check probes. Provides connection pooling and timeout control. |
| cryptography 42.0+ | 否 | Required only for TLS certificate expiry analysis in the health check module. If absent, expiry warnings are skipped. |
| pandas 2.0+ | 否 | Required only for CSV export adapter. Enables efficient transformation of manifest data into tabular formats. |
| Jinja2 3.1+ | 否 | Required only for static HTML generation. If absent, the build command produces plain text output only. |
| pytest 8.0+ | 否 | Required only for running the test suite during development or CI pipelines. Not needed for production operation. |
| black 24.0+ | 否 | Optional code formatter used in pre-commit hooks. Does not affect runtime behavior. |
| mkdocs 1.5+ | 否 | Required only for building the project documentation site locally. The documentation is also available online. |
| pre-commit 3.0+ | 否 | Framework for managing git pre-commit hooks. Used to enforce code style and run basic checks before commits. |

## 文档导航

The documentation is organized into four layers reflecting different user personas and interaction depths. Each layer addresses a distinct set of questions relevant to that audience.

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| User Guide | docs/user-guide/ | How do I install the tool? How do I run a health check? How do I generate the HTML dashboard? What do the health check status codes mean? |
| Manifest Reference | docs/manifest-schema/ | What is the structure of the manifest YAML file? Which fields are required? How do I add a new domain entry? How do I version a manifest? |
| Operator Handbook | docs/operator/ | How do I deploy the health check as a scheduled service? How do I configure email alerts for domain failures? How do I backup and restore manifest history? |
| Developer Internals | docs/developer/ | How do I extend the CLI with a new subcommand? How do I write a custom adapter for a new data format? How are health check workers load-balanced? |

## 资源列表

The following domains constitute the complete resource index for project batch 266/455. Each entry is presented exactly as provided in the source data, without normalization, protocol inference, or URL rewriting. Categories are assigned based on the domain naming patterns and known content profiles.

### East Asian Cultural Resource Domains

- <code>ribenrenqizhongwenzimu.org.cn</code>
- <code>ribenyehuashipin.org.cn</code>
- <code>rihanjialeibi.org.cn</code>
- <code>shufuzhongwenzimu.org.cn</code>

### European and American Media Asset Domains

- <code>oumeishunvwangzhan.org.cn</code>
- <code>oumeilingleisetu.org.cn</code>
- <code>ouzhouyazhouzipai.org.cn</code>

### General Entertainment and Reference Domains

- <code>gaohuangzaixianguankan.org.cn</code>
- <code>daxiangjiaomianfei.org.cn</code>
- <code>laosijiwangzhi.org.cn</code>

All listed domains are treated as external, third-party resources over which the project exercises no editorial control. The inclusion of a domain in this manifest does not imply endorsement, affiliation, or validation of its content. Users are responsible for complying with all applicable laws and terms of service when accessing any listed resource.

## 项目结构

The project source tree follows a modular, layered architecture separating core data models, CLI entry points, infrastructure adapters, and presentation layers. Each directory is annotated with its primary responsibility.

```
datalink-core/
├── cli.py                         # Main CLI entry point, dispatches subcommands via argparse
├── requirements.txt               # Production dependencies with pinned versions
├── requirements-dev.txt           # Development and testing dependencies
├── pyproject.toml                 # Project metadata, build configuration, and tool settings
│
├── src/
│   ├── datalink/
│   │   ├── __init__.py
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   ├── manifest.py        # Manifest data classes: DomainEntry, Category, TagSet
│   │   │   └── health.py          # Health check result models: ProbeResult, AggregatedStatus
│   │   ├── parsers/
│   │   │   ├── __init__.py
│   │   │   ├── yaml_loader.py     # PyYAML wrapper with schema validation and error reporting
│   │   │   └── json_adapter.py    # JSON Lines import/export with streaming support
│   │   ├── probes/
│   │   │   ├── __init__.py
│   │   │   ├── http_worker.py     # Async HTTP probe using aiohttp with configurable timeouts
│   │   │   └── cert_checker.py    # TLS certificate extraction and expiry calculation
│   │   ├── renderers/
│   │   │   ├── __init__.py
│   │   │   ├── html_builder.py    # Jinja2-based HTML dashboard generator
│   │   │   └── plain_formatter.py # Plain-text manifest dumper for console output
│   │   └── utils/
│   │       ├── __init__.py
│   │       ├── hash_utils.py      # SHA-256 checksum computation for manifest entries
│   │       └── diff_engine.py     # Version-to-version delta comparison and change summarization
│   │
│   └── tests/
│       ├── unit/                  # Unit tests for models, parsers, and utilities
│       ├── integration/           # Integration tests involving filesystem and network calls
│       └── fixtures/              # Static YAML and JSON samples used in test cases
│
├── manifests/
│   ├── current.yaml               # Active, production manifest with all 10 domain entries
│   ├── archive/                   # Historical manifest versions with date-stamped filenames
│   └── schemas/                   # JSON Schema and custom validators for manifest structure
│
├── reports/                       # Default output directory for health check JSON reports
│   └── .gitkeep
│
├── build/                         # Default output directory for static HTML dashboard
│   └── .gitkeep
│
├── docs/                          # Project documentation in Markdown format
│   ├── user-guide/
│   ├── manifest-schema/
│   ├── operator/
│   └── developer/
│
├── scripts/                       # Utility shell scripts for automation
│   ├── cron-health-check.sh      # Wrapper script for scheduled health check execution
│   └── rotate-reports.sh         # Log rotation and report archival script
│
└── .pre-commit-config.yaml        # Pre-commit hook definitions for code quality checks
```

## 贡献指南

Contributions are welcome in the form of manifest additions, documentation improvements, bug reports, and feature implementations. The project adheres to a standard fork-and-pull-request workflow with automated CI checks. All contributors are expected to follow the code of conduct and to maintain the high standards of reproducibility and clarity that define the project.

1. **Fork the Repository and Set Up the Development Environment** – Fork the main repository on GitHub, clone your fork locally, and run `pip install -r requirements-dev.txt` to install all development dependencies. Activate the pre-commit hooks by running `pre-commit install` to enforce code style and basic linting automatically.

2. **Propose Manifest Changes via Structured Pull Requests** – For any addition, removal, or modification of a domain entry, update the `manifests/current.yaml` file and include a detailed commit message explaining the rationale. Ensure that the `notes` field for each changed entry documents the source of the change, such as a user request, an upstream relocation, or a periodic review finding.

3. **Write Tests for New Functionality or Bug Fixes** – All new CLI subcommands, adapter modules, or rendering logic must include corresponding unit tests under `src/tests/unit/` with at least 80% branch coverage. Integration tests that perform actual network probes should be marked with the `@pytest.mark.network` decorator and are run conditionally in CI.

4. **Update the Documentation and Example Manifests** – Every user-facing feature change must be reflected in the appropriate documentation section under `docs/`. For manifest schema changes, update the accompanying JSON Schema file and provide a migration example. Ensure that the example manifest in `manifests/current.yaml` remains valid and representative.

5. **Submit a Pull Request with a Complete Checklist** – Open a pull request against the main branch of the upstream repository. Fill out the provided PR template completely, including the change type, testing performed, documentation updated, and a self-review checklist. The maintainers will review the submission within 5 business days and may request further modifications before merging.

## 常见问题

**Q: How does the project handle domain changes, such as when a resource moves to a new URL or shuts down entirely?**

A: The project does not automatically rewrite or redirect domain entries. When a domain change is identified either through the health check reporting a persistent failure or through user notification, a maintainer manually updates the manifest entry in a new version commit. The previous entry is moved to the archive with a `deprecated` flag and a `replaced_by` field pointing to the new domain, if applicable. The delta reporting tool then clearly shows this transition in the next version diff. Users are responsible for migrating their own references to the updated entry.

**Q: Can I use this manifest behind a corporate firewall or in an air-gapped environment?**

A: Yes, the manifest is fully static and does not require external network access to read or parse. The health check module is optional and can be disabled by omitting the `probe` subcommand. The HTML dashboard is generated entirely from the local manifest file and does not load any external resources such as CDN-hosted JavaScript or fonts. For air-gapped deployments, simply clone the repository once on a connected machine and transfer the directory to the target environment via removable media.

**Q: How frequently is the manifest updated, and how are updates communicated to users?**

A: The manifest receives routine updates on a quarterly cadence, driven by automated health check reports and manual user submissions. Critical updates, such as the removal of a domain that has been unreachable for more than 90 consecutive days, may be applied out-of-cycle. All changes are recorded in the `CHANGELOG.md` file at the project root and are tagged with semantic version numbers. Users subscribed to the project's release feed on GitHub receive notification of each tagged version. For automated environments, we recommend consuming the latest manifest version via the stable `current.yaml` symbolic link, which always points to the most recent validated revision.

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:26
