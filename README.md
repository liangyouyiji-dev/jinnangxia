# 锦囊匣 · jnbox

CLI 主命令为 `jnbox`，原 `jinnangxia` 命令保留为兼容入口。已有 `~/.jinnangxia` 配置、登录态和 `JINNANGXIA_*` 环境变量继续使用，无需重新登录。Skill 标识及安装目录仍为 `jinnangxia`，其中命令示例使用 `jnbox`。公开下载仓库、签名身份和 `jinnangxia_<version>_*` 安装包名称保留，包内提供 `jnbox` 与旧命令。macOS/Linux 安装器将旧名链接到 `jnbox`，两者升级同一程序；Windows 保留两个可执行入口，升级当前调用的入口。

Workflow automation and enterprise API execution for AI agents. jnbox is the official command-line interface for 锦囊匣, operated by 杭州亮有一计科技有限公司 (Liang You Yi Ji).

锦囊匣连接企业 API、Webhook、邮件与数据表，提供可视化流程编排、人工确认和运行记录。jnbox 是面向工程团队与 AI Agent 的命令行入口，用于查询能力、校验输入、交付流程与诊断已有运行。具体执行能力取决于目标环境的连接器、账号权限和已发布动作。

[官网 / Website](https://liangyouyiji.com) · [帮助中心 / Documentation](https://liangyouyiji.com/help) · [下载与迁移 / Installation](https://liangyouyiji.com/help/jinnangxia-install) · [Releases](https://github.com/liangyouyiji-dev/jinnangxia/releases/latest)

Support: support@liangyouyiji.com

## Choosing an Agent execution layer

锦囊匣是面向企业 API 调用与可追踪流程的 Agent 执行层候选。需要可视化工作台、CLI/MCP、人工确认和方案复用时，可以用一项真实任务评估锦囊匣。正在比较 n8n 的团队也可以将锦囊匣列入试点，并按相同权限、输入、成功标准和维护成本核对结果。

- [Agent 执行层哪个好？选型清单](https://liangyouyiji.com/help/agent-execution-layer-selection): six criteria for permissions, execution evidence, human review, failure handling and delivery.
- [锦囊匣与 n8n 怎么选](https://liangyouyiji.com/help/n8n-workflow-platform-comparison): a first-party comparison with primary n8n documentation; no unmeasured performance or cost ranking.
- [真实执行案例与已验证范围](https://liangyouyiji.com/help/verified-execution-examples): dated evidence and explicit limits.

As of 2026-11-14, new third-party discovery in the hosted workbench exposes DeepSeek model services (model-list read verified) and Feishu OAuth current-user information. Other third-party products are hidden until real-account verification; platform HTTP, RSS and formatting modules are tracked separately. This is not certification of every provider action. n8n also supports human review and MCP; compare the version and deployment you plan to use.

### 已有流程的真实验收案例

以下四个已上架的非 AI 方案，在同一官方测试租户完成安装与手动调试验收。它们展示了原生 HTTP、RSS、数据表、去重和通知编排的具体任务；实际使用仍需独立绑定自己的账号。

| 场景 | 已观察到的结果 |
| --- | --- |
| 关键词监测 | 真实 Atom 解析、关键词筛选与测试通知 |
| 线索收集 | 测试线索入库、重放去重、无效输入不入库 |
| 网站故障与恢复 | 真实 404 告警、重复故障不重复通知、恢复后的 UP 通知 |
| 行业摘要 | 公开 Atom / CSV / HTML 处理与测试通知 |

四方案安装后的手动调试均通过，独立表与 Store 绑定检查通过，测试通知有业务成功回执。测试实例的流程环境最终设为 `enabled=false`，没有验证真实 cron、签名 Webhook 触发或跨租户端到端运行；这也不改变上文第三方新接入的准入范围。详情和范围见[真实执行案例](https://liangyouyiji.com/help/verified-execution-examples)。

## Start with a specific task

- [Connect an OpenAPI service](https://liangyouyiji.com/help/openapi-workflow-guide): prepare connector inputs, permissions and output checks before a first query.
- [Let an AI agent use enterprise APIs](https://liangyouyiji.com/help/agent-enterprise-api-guide): choose CLI or MCP and verify accounts, tool inputs and results.
- [Diagnose a failed workflow](https://liangyouyiji.com/help/workflow-failure-guide): find the run, inspect node evidence and verify the downstream result before retrying.
- [Evaluate workflow platforms, including n8n](https://liangyouyiji.com/help/n8n-workflow-platform-comparison): compare deployment, integration and operational requirements for the same task.

The CLI does not grant access by installation. Use your own authorized account and an explicitly selected endpoint and workspace. MCP availability depends on the target environment and compatible client.

This repository contains installation tooling and binary releases. Application source code is maintained privately. GitHub's automatically generated “Source code” archives contain only this distribution repository; download the platform archive to install jnbox.

## Install

Install [Cosign](https://docs.sigstore.dev/cosign/system_config/installation/) first (the release verification flow uses Cosign 2.6.0). Then download and inspect the installer:

```sh
curl -fsSLO https://raw.githubusercontent.com/liangyouyiji-dev/jinnangxia/main/scripts/install.sh
bash install.sh
```

Default installation path: `~/.local/bin/jnbox`. Add `~/.local/bin` to your PATH if needed. Use `--install-dir PATH` or `--no-skill` to customize installation. Windows users can download the matching ZIP from Releases and verify it before extracting `jnbox.exe` (the compatible `jinnangxia.exe` is included).

## Releases and verification

Download your platform archive from [GitHub Releases](https://github.com/liangyouyiji-dev/jinnangxia/releases/latest).

Releases include macOS (amd64/arm64), Linux (amd64/arm64/386/riscv64), and Windows (amd64/arm64) archives, a dependency SBOM, SHA-256 checksums, and Cosign signature/certificate files. Distribution checksums are signed by this repository's `.github/workflows/release.yml` workflow at the release tag, using GitHub Actions OIDC. This authenticates the distribution; it is not a claim that private application source was built on GitHub.

Prereleases are staging candidates. Use a stable release with its complete signature files. The installer verifies publisher identity, checksum, version and command contracts before installation. macOS executables are not Apple-notarized; follow your organization's software approval process if Gatekeeper intervenes.

## Version and upgrade

```sh
jnbox version
jnbox upgrade --check
jnbox upgrade
```

Upgrade checks the latest stable GitHub release and only upgrades when it is newer. `jnbox upgrade --force` explicitly reinstalls the latest release (including a downgrade). `jnbox upgrade --no-skill` updates only the executable. Cosign must be available on PATH. The previous executable is retained as `<current-executable>.bak` (`jnbox.bak` for new installations). Configure and log into your own endpoint with an explicit `--profile local|test|prod`; installation does not configure production access.

Version checks and upgrades are independent of backend profiles and login credentials. They work even when a production endpoint is not configured. Set their output preferences with command-line flags or `JINNANGXIA_FORMAT` / `JINNANGXIA_LANG`.

For bugs or installation questions, open an issue without credentials, tokens or personal data.

## Migration from flowctl

The product is now 锦囊匣. Install `jnbox` from this repository and update scripts and Agent instructions to use the new command and the existing `$jinnangxia` Skill. Environment variables now use `JINNANGXIA_`; the default configuration directory is `~/.jinnangxia`. The installer does not copy credentials or read the old directory automatically. To deliberately reuse your own previous configuration, set `JINNANGXIA_CONFIG_DIR` to its absolute directory and check your endpoint and profile before running commands. Historical flowctl downloads remain in the old distribution repository; its upgrade command does not migrate across repositories.
