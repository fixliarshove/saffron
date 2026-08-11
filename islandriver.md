# VideoLink Hub

VideoLink Hub 是一个面向开发者和内容运营人员的开源技术资源外链聚合平台，专注于视频播放、字幕匹配与流媒体处理相关工具与数据源的整理与分发。项目本身不存储任何媒体文件，仅提供结构化、可机读的外部资源索引，帮助用户快速定位可用的公开视频源、字幕接口及流媒体测试端点。

项目定位为技术资源导航中间件，适用于自动化测试脚本编写、流媒体服务原型验证、内容采集规则调试等场景。目标用户包括后端开发人员、自动化运维工程师、数据采集工程师以及个人视频工具开发者。

## 功能概览

- 结构化外链索引：按内容主题与数据源类型对公开资源链接进行分类整理，支持 JSON 与 YAML 格式导出，便于集成到 CI/CD 或自动化任务中。

- 多协议端点聚合：统一收录 HTTP 与 HTTPS 协议的流媒体测试地址，支持快速切换协议进行连通性验证与延迟测试。

- 字幕接口映射：提供字幕文件（.srt/.ass）的公开下载路径映射，辅助开发者测试字幕解析与时间轴校准逻辑。

- 分辨率与编码标识：对每个视频链接标注预估分辨率（如 720p/1080p）与编码格式（H.264/H.265），方便媒体处理脚本自适应选择。

- 可用性健康检查：内置简单的 HTTP HEAD 请求检查脚本，可定期对收录链接进行可达性探测，并输出状态报告。

- 分类过滤与检索：支持按地区（国产/日韩/欧美）、内容类型（影视/综艺/测试样片）、语言（中文/双语）进行快速过滤检索。

- 外部元数据扩展：允许用户通过自定义标签（tag）和备注字段附加额外信息，如码率、帧率、音轨数量等。

## 应用场景

- 流媒体播放器开发测试：开发人员在构建基于 HTML5 或 ExoPlayer 的播放器时，可使用本项目的链接列表快速获得不同格式、分辨率和编码的测试流，验证播放器的兼容性与缓冲策略。

- 字幕同步算法验证：自然语言处理或音视频对齐算法工程师可利用汇总的字幕源端点，获取大量带时间轴的字幕文件，用于训练或测试字幕-音频对齐模型。

- 自动化监控脚本编写：运维人员可将本项目的链接列表作为输入源，编写周期性健康检查脚本，监控多个第三方视频源的可用性，并在服务降级时触发告警。

- 数据采集规则调试：数据采集工程师在编写爬虫或解析规则时，通过本项目快速获取不同结构、不同响应头的测试链接，用于验证 XPath/正则表达式或 JSONPath 提取逻辑的鲁棒性。

- 教学演示与原型搭建：高校教师或技术培训讲师可利用该资源列表作为教学素材，在课堂中快速搭建流媒体服务演示环境，无需自行寻找分散的测试地址。

## 快速开始

```bash
# 克隆项目仓库
git clone https://github.com/videolink-hub/videolink-hub.git

# 进入项目目录
cd videolink-hub

# 安装依赖（Python 3.8+ 环境）
pip install -r requirements.txt

# 运行本地索引服务（默认监听 8080 端口）
python serve.py --port 8080

# 执行所有收录链接的健康检查
python check_health.py --output health_report.json
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.8 或更高 | 核心脚本运行环境，用于服务启动与健康检查 |
| pip | 20.0 或更高 | Python 包管理工具，用于安装 requirements.txt 中的依赖 |
| requests | 2.28.0 或更高 | HTTP 请求库，用于执行链接可达性探测 |
| pyyaml | 6.0 或更高 | YAML 格式解析支持，用于配置文件和资源列表的读写 |
| flask | 2.2.0 或更高 | 轻量级 Web 服务框架，提供本地索引查询接口 |
| pytest | 7.0.0 或更高 | 单元测试框架，用于运行项目自测套件（开发环境可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | docs/user_guide.md | 如何安装、配置、启动服务以及调用资源查询 API |
| 资源维护 | docs/maintenance.md | 如何新增、删除或更新外链记录，以及健康检查的周期策略 |
| 开发者指南 | docs/developer.md | 项目目录结构说明、核心模块职责、如何提交 PR 与扩展新分类器 |
| API 参考 | docs/api_reference.md | RESTful 接口定义、请求参数、响应格式与错误码说明 |
| 部署说明 | docs/deployment.md | 生产环境下的容器化部署（Docker）、反向代理配置与性能调优建议 |

## 资源列表

### 中文影视字幕在线资源

<code>zaixianshipinzhongwenzimu1.org.cn</code>

<code>zaixianbofangzhongwenzimu1.org.cn</code>

<code>zhongwenzimuzaixianmianfei1.org.cn</code>

### 国产影视在线播放资源

<code>yirenguochanzaixianshipin1.org.cn</code>

### 高清视频在线观看资源

<code>gaoqingshipinzaixianguankan1.org.cn</code>

### 中文视频在线观看资源

<code>zhongwenshipinzaixianguankan1.org.cn</code>

### 美女视频在线观看资源

<code>meinvshipinzaixianguankan1.org.cn</code>

### 日韩在线免费视频资源

<code>rihanzaixianmianfeishipin.org.cn</code>

### 欧美在线免费视频资源

<code>oumeizaixianmianfeishipin.org.cn</code>

### 中文字幕高清视频资源

<code>zhongwenzimugaoguingshipin.org.cn</code>

## 项目结构

```
videolink-hub/
├── serve.py                        # 本地索引服务入口，启动 Flask 应用
├── check_health.py                 # 健康检查脚本，批量探测链接可达性
├── requirements.txt                # Python 依赖清单
├── config/
│   ├── settings.yaml               # 全局配置（端口、超时、重试策略）
│   └── categories.yaml             # 分类映射定义（地区、类型、标签）
├── data/
│   ├── links.json                  # 主资源索引数据（JSON 格式）
│   ├── links.yaml                  # 资源索引数据（YAML 格式，供人工编辑）
│   └── health_cache.json           # 健康检查结果缓存
├── modules/
│   ├── fetcher.py                  # HTTP 请求封装，含重试与超时逻辑
│   ├── parser.py                   # 链接元数据解析（分辨率/编码推断）
│   ├── validator.py                # URL 格式校验与域名黑名单过滤
│   └── exporter.py                 # 数据导出工具（JSON/YAML/CSV）
├── tests/
│   ├── test_fetcher.py             # 单元测试：fetcher 模块
│   ├── test_parser.py              # 单元测试：parser 模块
│   └── test_validator.py           # 单元测试：validator 模块
├── docs/                           # 完整文档目录（参见文档导航）
│   ├── user_guide.md
│   ├── maintenance.md
│   ├── developer.md
│   ├── api_reference.md
│   └── deployment.md
├── scripts/
│   ├── import_csv.py               # 从 CSV 导入外部链接数据
│   └── generate_report.py          # 生成健康状态 HTML 报告
└── LICENSE                         # MIT 许可证文件
```

## 贡献指南

1. 复刻项目仓库并在本地创建功能分支（如 feature/add-new-category），确保分支名称清晰反映改动目的。

2. 按照 data/links.yaml 的既定格式新增或修改资源记录，每条记录需包含 url、category、tags、resolution、encoding 五个必填字段，并运行 python validator.py 校验格式正确性。

3. 在本地执行 pytest 测试套件，确保所有既有测试用例通过，并为新增功能（如新分类器）补充对应的测试文件。

4. 提交 pull request 到主仓库的 dev 分支，在 PR 描述中附上变更摘要、测试结果截图以及是否影响健康检查脚本的说明。

5. 等待项目维护者 review，必要时根据反馈进行修改，合并后将在下一个发布版本中收录您的贡献。

## 常见问题

Q: 收录的链接无法访问怎么办？

A: 项目维护者会定期执行 check_health.py 脚本，并将结果更新至 health_cache.json。如果您发现某个链接持续不可用，请在 GitHub Issues 中提交报告，或自行通过 PR 移除失效链接。您也可以在本地的 settings.yaml 中调整超时和重试参数，以适应不同的网络环境。

Q: 可以自行添加私有或内网视频源链接吗？

A: 可以。您可以在本地 data/links.yaml 中添加任意合规链接，但请注意这些链接不会随项目公开推送。如果您希望内部分享，建议使用项目的 exporter 工具导出为单独的配置文件并纳入您自己的版本控制。

Q: 如何批量验证所有链接的响应时间？

A: 使用 scripts/generate_report.py 脚本并添加 --benchmark 参数，该脚本会并发请求所有链接并记录响应时间分布，最终生成包含平均延迟、最大延迟和超时率的 HTML 报告，方便您评估整体链路质量。

## 许可证

MIT

> 外链数量: 10 | 生成时间: 2026-08-11 16:54:36
